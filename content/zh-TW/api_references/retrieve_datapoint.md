# 讀取資料點

## 描述

使用 **HTTPs GET** 來取得裝置上傳的資料點

## HTTP 請求
### URL

您可以透過指定 URL 中資源路徑與查詢參數來讀取特定資料通道中的資料點。

* **資源路徑**

	| 資源名稱 | 型別 | 是否必填 | 描述 |
	| --- | --- | --- | --- |
	| 裝置 ID | 字串 | 必填 | 您需在 URL 中指定你所要獲取資料的裝置 ID |
	| 資料通道 ID | 字串 | 必填 | 您需在 URL 中指定你所要獲取資料的資料通道 ID |


* **查詢參數**

	| 參數名稱 | 型別 | 是否必填 | 描述 |
	| --- | --- | --- | --- |
	| start | 數字 | 選填 | 查詢起始時間 |
	| end | 數字 | 選填 | 查詢中止時間 |
	| limit | 整數 | 選填 | 要回傳的資料點數目 ( 默認值 = 1 ) |
	| offset | 整數 | 選填 | 第幾筆開始的資料點 |
	| order | 字串 | 選填 | 資料預設是按照時間戳，由新到舊回傳，您也可透過指定 "asc" 或 "desc" 改變順序  |
	
	
MCS 可將您請求的數據回傳成 JSON 或是 CSV 格式，您可藉由 HTTP 請求中的資源名稱來指定回傳的格式。

每次請求最多只能讀取 1000 筆資料點。

* **獲取 JSON 格式的數據**

	```
	https://api.mediatek.com/mcs/v2/devices/:deviceId/datachannels/:datachannelId/datapoints?start=:startTime&end=:endTime&limit=:limit&offset=:offset
	
	```

* **獲取 CSV 格式的數據**

	若您希望數據以 CSV 的格式回傳，請在資源名稱的最後加上 `.csv`，變成 `datapoints.csv`

	```
	https://api.mediatek.com/mcs/v2/devices/:deviceId/datachannels/:datachannelId/datapoints.csv?start=:startTime&end=:endTime&limit=:limit&offset=:offset
	
	```

**範例**

* 讀取最新一個資料點並以 JSON 格式回傳：

	```
	https://api.mediatek.com/mcs/v2/devices/:deviceId/datachannels/:datachannelId/datapoints
	```

* 讀取最新一個資料點並以 CSV 格式回傳：

	```
	https://api.mediatek.com/mcs/v2/devices/:deviceId/datachannels/:datachannelId/datapoints.csv
	```

* 讀取一段時間範圍內的資料點：

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sxxxx/datachannels/my_data_channel/datapoints?limit=1000&start=1524107855148&end=1524550447427
	```

請注意，若您只使用開始時間（start）和結束時間（end）參數，系統只會回覆您此區間內的最後一筆資料。若您希望取得此區間內的更多資料點，您可以使用 **limit** 來定義您想取得此區間內的幾筆資料點。


* 限制您要讀取的資料點數目，MCS 只會回傳最新的 N 筆資料:

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sxxxx/datachannels/my_data_channel/datapoints?limit=10	
	```


### 方法（Method）
GET


### 表頭（Header）

**存取憑證**

* 透過裝置讀取數據

	```
	deviceKey: your_device_key
	```
* 透過您自行開發的應用（服務提供者帳號）

	```
	appId: your_appId
	appSecret: your_appSecret
	```


## 回覆

### 回覆代碼
200

### 表頭（Header）

* **JSON 格式：**

	```
	content-type: text/html
	```

* **CSV 格式：**
	
	```
	content-type: application/json	
	```
	
### 內文（Body）

* **JSON 格式：**

	回應的內文為 JSON 的格式，請求的數據位於 **dataChannels** 物件下的 **dataPoints** 陣列中。


**dataChannels 物件**

| 欄位名稱 | 格式 | 描述|
| --- | --- | --- | --- |
| dataChnId | 字串 | 資料通道 ID |
| isOverflow | 布林 | 要求的資料點是否超過數目限制|
| dataPoints | JSON 物件陣列 | 資料點 |


**dataPoints 陣列**

| 欄位名稱 | 格式 | 描述|
| --- | --- | --- | --- |
| createdAt | 數字 | 以 Unix timestamp 格式紀錄的資料點建立時間|
| values | JSON 物件 | 資料點的值 |


**範例:**

* **以 JSON 格式回傳**

	```
	{
	    "apiVersion": "2.18.3",
	    "code": 200,
	    "message": "Request has succeeded",
	    "deviceId": "DL6sxxxx",
	    "dataChannels": [
	        {
	            "dataChnId": "my_data_channel",
	            "isOverflow": false,
	            "dataPoints": [
	                {
	                    "recordedAt": 1524550447427,
	                    "values": {
	                        "value": 35
	                    }
	                },
	                {
	                    "recordedAt": 1524119075906,
	                    "values": {
	                        "value": 30
	                    }
	                }
	            ]
	        }
	    ]
	}
	```

* **以 CSV 格式回傳**

	```
	my_data_channel,1524119075906,35
	my_data_channel,1524550447427,30
	```



## 錯誤回覆

當錯誤發生時，回覆代碼為非 200 之其他代碼。回覆內容為 JSON 格式並會包括以下資訊：


| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| code | 整數 | 錯誤代碼 |
| message | 字串 | 錯誤描述 |



**範例:**

* **以 CSV 格式回傳**

	```
	404,channel not found
	```
	
* **以 JSON 格式回傳**	
	
	```
	{
	    "apiVersion": "2.18.3",
	    "code": 404,
	    "message": "channel not found",
	    "errors": [
	        {
	            "code": 404,
	            "message": "404 Not Found"
	        }
	    ],
	    "statusCode": 404,
	    "options": {}
	}
	```

