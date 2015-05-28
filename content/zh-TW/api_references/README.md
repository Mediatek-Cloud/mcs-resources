# API 參考資料集

MediaTek Cloud Sandbox (MCS)提供一系列的RESTful API讓您能夠便利的使用，例如上傳和讀取資料點，或是透過TCP socket對裝置下指令。MCS亦能儲存照時間排序的資料數列，並以圖表畫形式呈現給您。


## 連接點

所有的MCS RESTful API皆以以下形式呈現：

```
https://api.mediatek.com/v2
```

## 參數

跟在連接點後的參數用來在URL路徑內，定義特定的資源：

```
https://api.mediatek.com/v2/devices/{deviceId}/retrieveDataPoints

```

在上方的範例中，您可以看到deviceId在URL中被定義了。在任何的API 請求中，不是以URL形式傳送的參數，都必須定義以JSON或是CSV格式包裝。您必須定義一個`content -Type` header 為`application/json` 或是 `text/csv`。


## 客戶端錯誤

Mediatek Cloud Sandbox (MCS) 使用標準HTTP狀態來表達API請求的成功或是錯誤。以下是您呼叫MCS API有可能遇到的HTTP狀態：

**200 OK** - 請求成功。

**201 Created **- 請求成功，並且新資源已建立。

**202 Accepted** - 請求成功，但尚未完成。

**204 No Content** -請求成功，但伺服器無回應任何內容。通常是刪除特定資源的請求回覆。

**400 Bad Request** - 伺服器無法處理請求，由於客戶端給的參數錯誤。

**401 Unauthorized** - 無提供授權或授權失敗。需要提供授權的header。

**403 Forbidden** -伺服器拒絕對一個不合格的請求做回覆。

**404 Not Found** - 請求的資源不存在。

**405 Method Not Allowed** - 請求的方法不支援。

**500, 502 Server Error** - MCS伺服器錯誤。


## HTTP 請求方式

The MediaTek Cloud Sandbox (MCS) 提供以下型式的API請求方式：


**GET** - 用來取得資源狀態。

**POST** - 用來建立資源。

**PUT** - 用來更新資源狀態。

**DELETE** - 用來刪除資源。



## 授權

所有的API請求皆須被授權。您必須有一個header `Authentication` 為您的Bearer token。如果未提供此授權碼，系統則會回覆您無授權訊息。


## API Key

每次當一個產品原型，資料通道，或是測試裝置被建立後，都會有一個獨特的Key被指派給該資源。這個獨特的Key是不可編輯的，且您將再存取此資源時用到。您無法存取您無此Key值的資源。

開發者可以定義哪種API Key將在哪些HTTP請求方式中被需要。舉例來說，如欲從MCS取得某一資料通道的資料，您必須擁有此資料通道以及所述測試裝置的API Key。


## 資源

以下是您使用MCS時，會時常使用到的詞彙：

### 資料通道

一個資料通道是一個能夠傳送從裝置回傳的資料至MCS平台，或是能夠將指令從MCS平台傳達至裝置的通道。簡單來說，資料通道是一個雲和裝置之間單方向或是雙方向的溝通管道。

MCS提供了許多API讓使用者能夠快速的存取資料通道上得資料點。

### 裝置

在MCS平台上有兩種種類的裝置，其中第一種是測試裝置。測試裝置為在商品上市前，開發者可以用來測試開發結果的裝置。第二種裝置為商轉後大量給終端使用者實際使用的裝置。

MCS提供了許多API讓開發者和其他使用者能夠快速的存取資料通道上的資料點，或是遠端控制裝置狀態。

### 產品原型

產品原型是您將來要交付的終端商品。MCS提供了許多API讓使用者能夠使用。開發者能在產品原型頁面中開發產品，例如新增資料通道並建立測試裝置來測試確保之後商轉功能。


