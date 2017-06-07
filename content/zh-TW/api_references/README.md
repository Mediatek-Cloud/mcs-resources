# API 參考資料集

MediaTek Cloud Sandbox (MCS) 提供一系列的 RESTful API 讓您能夠便利的使用，例如上傳和讀取資料點，或是透過 TCP socket 對裝置下指令。MCS 亦能儲存照時間排序的資料數列，並以圖表化形式呈現給您。


## Request URL

您可以透過以下網址來呼叫 MCS API：

```
https://api.mediatek.com/v2
```

## 參數

跟在連接點後的參數用來在 URL 路徑內，定義特定的資源：

```
https://api.mediatek.com/v2/devices/{deviceId}/retrieveDataPoints

```

在上方的範例中，您可以看到 deviceId 在 URL 中被定義了。在任何的 API 請求中，不是以 URL 形式傳送的參數，都必須定義以 JSON 或是 CSV 格式包裝。您必須定義一個`content -Type` header 為`application/json` 或是 `text/csv`。


## 客戶端錯誤

Mediatek Cloud Sandbox (MCS) 使用標準 HTTP 狀態來表達 API 請求的成功或是錯誤。以下是您呼叫 MCS API 有可能遇到的 HTTP 狀態：

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


## HTTP 請求方式

The MediaTek Cloud Sandbox (MCS) 提供以下型式的 API 請求方式：


**GET** - 用來取得資源狀態。

**POST** - 用來建立資源。

**PUT** - 用來更新資源狀態。

**DELETE** - 用來刪除資源。



## 授權

所有的 API 請求皆須被授權。您必須有一個 header `Authentication` 為您的 Bearer token。如果未提供此授權碼，系統則會回覆您無授權訊息。


## 資源 ID

每次當一個產品原型，資料通道，或是測試裝置被建立後，都會有一個獨特的 ID 被指派給該資源。這個獨特的 ID 是不可編輯的，且您將再存取此資源時用到。您無法存取您無 ID 的資源。

舉例來說，如欲從 MCS 取得某一資料通道的資料，您必須擁有此資料通道以及所述測試裝置的資源 ID。


## 資源

以下是您使用 MCS 時，會時常使用到的詞彙：

### 資料通道

一個資料通道是一個能夠傳送從裝置回傳的資料至 MCS 平台，或是能夠將指令從 MCS 平台傳達至裝置的通道。簡單來說，資料通道是一個雲和裝置之間單方向或是雙方向的溝通管道。

MCS 提供了許多 API 讓使用者能夠快速的存取資料通道上得資料點。

### 裝置

在 MCS 平台上有兩種種類的裝置，其中第一種是測試裝置。測試裝置為在商品上市前，開發者可以用來測試開發結果的裝置。第二種裝置為商轉後大量給終端使用者實際使用的裝置。

MCS 提供了許多 API 讓開發者和其他使用者能夠快速的存取資料通道上的資料點，或是遠端控制裝置狀態。

### 產品原型

產品原型是您將來要交付的終端商品。MCS 提供了許多 API 讓使用者能夠使用。開發者能在產品原型頁面中開發產品，例如新增資料通道並建立測試裝置來測試確保之後商轉功能。


