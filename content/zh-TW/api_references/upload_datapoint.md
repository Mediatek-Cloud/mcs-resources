# 上傳資料點

## 描述

使用 **HTTPs POST** 來上傳資料點

## HTTP 請求
### URL


* **使用 CSV 格式：**

	```
	https://api.mediatek.com/mcs/v2/devices/{deviceId}/datapoints.csv
	```

* **使用 JSON 格式：**

	```
	https://api.mediatek.com/mcs/v2/devices/{deviceId}/datapoints
	```

MCS 單筆上傳一次最多五筆資料點。

### 方法（Method）
POST


### 表頭（Header）

**1. 存取憑證（Access token）**

* 透過裝置上傳
	
	```
	deviceKey: {your_device_key}
	```

* 透過您自行開發的應用程式（服務提供者帳號）
	
	```
	appId: {your_appId}
	appSecret: {your_appSecret}
	```

	您可以在個人檔案頁面中的服務提供者分頁，申請取得 appId 以及 appSecret。


**2. Content Type**


* **使用 CSV 格式：**
	
	```
	Content-Type: text/csv
	```

* **使用 JSON 格式：**
	
	```
	Content-Type: application/json
	```


### 內文（Body）

* **使用 CSV 格式：**

	語法:
	
	```
	{Data_Channel_Id_1},{Timestamp},{Value_1},{Value_2},{Value_3}\n
	
	{Data_Channel_Id_2},{Timestamp},{Value_1}\n
	```

	如欲參考更多詳細的資料通道類型之格式，請參考**資料通道格式**章節。

	請注意：*Timestamp* 為非必填欄位。若此欄位為空(請保留逗號)，則 MCS 服務器會在收到此資料點時自動補上當前的時間戳。

	範例：
	
	```
	1,1432538716989,26
	2,,26.34,12,59
	```
	第一行：資料通道 ID 為 ”1“；”1432538716989“ 為上傳數據時，裝置或您的應用程式產生的時間戳（timestamp）；”26“ 為上傳的值。	
	第二行：資料通道 ID 為 ”2“；時間戳（timestamp）的欄位為空，由 MCS 服務器自動補上；”26.34“、”12“ 與 ”59“為上傳的數據(此時的資料通道類型為 GPS)。


* **使用 JSON 格式：**

	語法:
	
	每個 JSON 格式的資料點，都包含下列三種的資料：
	
	1. dataChnId
	2. timestamp
	3. values: 表示資料點的值。某些資料通道的值，可能是有多個數據組成。例如 GPS 通道，就包含了經度、緯度與海拔高度。
	
	```
	{
	   "datapoints":[
	      {
	         "dataChnId":"1",
	         "timestamp":1432538716989,
	         "values":{
	            "value":"26"
	         }
	      },
	      {
	         "dataChnId":"2",
	         "timestamp":1432538716989,
	         "values":{
	            "latitude":"26.34",
	            "longitude":"12",
	            "altitude":"59"
	         }
	      }
	   ]
	}	
	```
	
	資料點1： 資料通道 ID 為 ”1“；”1432538716989“ 為上傳數據時，裝置或您的應用程式產生的時間戳（timestamp）；”26“ 為上傳的值。
	
	資料點2： 資料通道 ID 為 ”2“；時間戳（timestamp）的欄位為空，由 MCS 服務器自動補上；”26.34“、”12“ 與 ”59“為上傳的數據(此時的資料通道類型為 GPS)。	

## HTTP 回覆

### 回覆代碼
200

### 表頭（Header）

* **使用 CSV 格式：**
	
	```
	content-type: text/html
	```

* **使用 JSON 格式：**
	
	```
	Content-Type: application/json
	```

### 內文（Body）

* **使用 CSV 格式：**
	
	```
	Success.
	```
	
* **使用 JSON 格式：**
	
	```
	{
	    "results": "success"
	}
	```

## 錯誤回覆

當錯誤發生時，MCS 服務器會回應非 200 的錯誤代碼。回覆內容包括以下資訊：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 錯誤代碼 |
| message | String | 錯誤原因|
| description | String | 詳細的錯誤描述 |

**範例:**

* **使用 CSV 格式：**
	
	```
	400,None of data points uploaded success.
	```
	
	
* **使用 JSON 格式：**
	
	```
	{
	    "apiVersion": "2.18.3",
	    "code": 400,
	    "message": "None of data points uploaded success.",
	    "errors": [
	        {
	            "code": 400,
	            "message": "400 Bad Request"
	        }
	    ],
	    "results": "",
	    "descriptions": [
	        "There is no such data channel displays_boolean for this device."
	    ],
	    "statusCode": 400,
	    "options": {}
	}
	```

