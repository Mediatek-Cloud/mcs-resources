# API 參考手冊

MediaTek Cloud Sandbox (MCS) 提供一系列的 RESTful APIs 讓您能夠便利的使用 MCS 服務，例如上傳和讀取資料點，或是透過 TCP socket 對裝置下指令。MCS 亦能儲存照時間排序的資料數列，並以圖表化形式呈現。


## 請求網址（Request URL）

MCS 提供的各個服務皆位於此網址（URL）之下。

```
https://api.mediatek.com/mcs/v2/
```

您可透過在請求網址（URL）當中指定**資源 ID** 來使用該資源所提供的服務。以底下的請求為例，我們透過指定裝置與資料通道的 ID（deviceID 與 dataChannelID）來使用 datapoints 相關的服務。

```
https://api.mediatek.com/mcs/v2/devices/{deviceID}/datachannels/{dataChannelID}/datapoints.csv
```

**範例**

以下為獲取 **datapoints** 的完整請求（需將 {variable} 換成您的真實數據），在後續的章節中會有更詳細的描述。

```
curl -X GET \
  https://api.mediatek.com/mcs/v2/devices/{deviceID}/datachannels/{dataChannelID}/datapoints.csv \
  -H 'devicekey: {deviceKey}' \
```

## 請求方法（Request Method）

The MediaTek Cloud Sandbox (MCS) 提供以下幾種 API 請求方法：

* **GET** - 用來取得資源狀態。

* **POST** - 用來建立資源。

* **PUT** - 用來更新資源狀態。

* **DELETE** - 用來刪除資源。


## 請求表頭（Request Header）
###1. 存取授權憑證（Access Token）

所有的 API 請求皆須被授權，因此您必須在請求表頭當中帶入授權憑證，才有權限存取對應的資源，進行對應的操作。MCS 開放的授權憑證主要有兩種：

* **服務提供者（service provider）帳號**：
	
	如果您是自行開發應用程式，包括手機 App 或網站應用，您可以在個人檔案頁面中的服務提供者分頁，申請取得 appId 以及 appSecret，使用此憑證存取 MCS 開放的所有 APIs。接著在所有 MCS 服務請求表頭（request header）中帶入 **appID** 與 **appSecret** 資訊。
	
	```
	appId: {your_appId}
	appSecret: {your_appSecret}
	```

* **裝置金鑰（device key）**:

	如果您開發的是裝置端的應用，且只需要使用裝置相關的服務 APIs，例如上傳與獲取資料點等，則您可直接使用裝置 ID 與金鑰作為認證。您可以在裝置詳情頁面中找到裝置 ID 與金鑰，接著在所有 MCS 服務請求表頭（request header）中帶入 **deviceKey** 資訊。
		
	```
	deviceKey: {your_device_key}
	```
	由於裝置 ID 已用於請求網址（request URL）中，用以指定所要存取的資源，因此不需再帶入表頭中。
	
###2. 內文格式（content-type）
您必須在請求表頭中加上 **content-type** 這個欄位讓 MCS 服務知道請求的內文格式並進行後續的處理與運算。

* `content-type: application/json` 表示內文為 JSON 格式。
* `content-type: text/csv` 表示內文為 CSV 格式。

## 請求內文（Request Body）

MCS 所支援的請求內文為 **JSON** 或 **CSV** 格式，不同的 APIs 服務所需要的參數皆不同，因此詳細的請求內容會在個別的 APIs 章節中介紹。

## 參數（Parameter）

以下介紹幾個在使用 MCS APIs 時會用到的參數、格式以及代表意義。

* **時間戳（timestamp）**

	時間戳是用來記錄一個資源被創建或更新的時間點，像是上傳資料點當時的時間、產品原型被建立的時間等等。在 MCS 系統中，時間是用 **Unix Epoch** 格式來表示，時間單位為毫秒（millisecond）。若您需要將 Unix Epoch 時間轉換成可讀性較高的常規表示法，可參考 [http://www.epochconverter.com/](http://www.epochconverter.com/)，例如：
	
	> *Timestamp in milliseconds: 1524720177000*
	> 可轉換成
	> *Human time (GMT): Thursday, April 26, 2018 5:22:57 AM*
	
* **資源 ID**

	每次當一個產品原型、測試裝置、資料通道或是韌體檔案被建立後，都會有一個獨特的 ID 被指派給該資源。這個獨特的 ID 是不可編輯的，您可透過它存取該資源。
	
	舉例來說，如欲從 MCS 取得某一資料通道的上傳數據，您必須先知道此資料通道 ID 以及所屬的測試裝置 ID，並將其帶入 HTTP 請求中以指定所要存取的資源。以下為三個 MCS 主要的資源類型。
	
	1. **資料通道**：一個資料通道是一個能夠傳送從裝置回傳的資料至 MCS 平台，或是能夠將指令從 MCS 平台傳達至裝置的通道。簡單來說，資料通道是一個雲和裝置之間單方向或是雙方向的溝通管道。MCS 提供了許多 APIs 讓使用者能夠快速的存取資料通道上的資料點。
	
	2. **裝置**：在 MCS 平台上有兩種種類的裝置，其中第一種是測試裝置。測試裝置為在商品上市前，開發者可以用來測試開發結果的裝置。第二種裝置為商轉後大量給終端使用者實際使用的裝置。MCS 提供了許多 APIs 讓開發者和其他使用者能夠快速的存取資料通道上的資料點，或是遠端控制裝置狀態。
	
	3. **產品原型**：產品原型是您將來要交付的終端商品。MCS 提供了許多 APIs 讓使用者能夠使用。開發者能在產品原型頁面中開發產品，例如新增資料通道並建立測試裝置來測試確保之後商轉功能。

## 回覆代碼（Response Code）

Mediatek Cloud Sandbox (MCS) 使用標準 HTTP 狀態來表達 API 請求的成功與否。以下是您呼叫 MCS API 有可能遇到的 HTTP 狀態：

**200 OK** - 請求成功。

**201 Created**- 請求成功，並且新資源已建立。

**202 Accepted** - 請求成功，但尚未完成。

**204 No Content** -請求成功，但伺服器無回應任何內容。通常是刪除特定資源的請求回覆。

**400 Bad Request** - 伺服器無法處理請求，由於客戶端給的參數錯誤。

**401 Unauthorized** - 無提供授權或授權失敗。需要提供授權的 header。

**403 Forbidden** -伺服器拒絕對一個不合格的請求做回覆。

**404 Not Found** - 請求的資源不存在。

**405 Method Not Allowed** - 請求的方法不支援。

**500, 502 Server Error** - MCS伺服器錯誤。
