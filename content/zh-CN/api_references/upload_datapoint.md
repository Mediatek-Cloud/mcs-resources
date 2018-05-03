# 上传资料点

## 描述

使用 **HTTPs POST** 来上传资料点

## HTTP 请求
### URL


* **使用 CSV 格式：**

	```
	https://api.mediatek.com/mcs/v2/devices/{deviceId}/datapoints.csv
	```

* **使用 JSON 格式：**

	```
	https://api.mediatek.com/mcs/v2/devices/{deviceId}/datapoints
	```

MCS 单笔上传一次最多五笔资料点。

### 方法（Method）
POST


### 表头（Header）

**1. 存取凭证（Access token）**

* 透过装置上传
	
	```
	deviceKey: {your_device_key}
	```

* 透过您自行开发的应用程式（服务提供者帐号）
	
	```
	appId: {your_appId}
	appSecret: {your_appSecret}
	```

	您可以在个人档案页面中的服务提供者分页，申请取得 appId 以及 appSecret。


**2. Content Type**


* **使用 CSV 格式：**
	
	```
	Content-Type: text/csv
	```

* **使用 JSON 格式：**
	
	```
	Content-Type: application/json 
	```


### 内文（Body）

* **使用 CSV 格式：**

	语法:
	
	```
	{Data_Channel_Id_1},{Timestamp},{Value_1},{Value_2},{Value_3}\n
	
	{Data_Channel_Id_2},{Timestamp},{Value_1}\n
	```

	如欲参考更多详细的资料通道类型之格式，请参考**资料通道格式**章节。

	请注意：*Timestamp* 为非必填栏位。若此栏位为空(请保留逗号)，则 MCS 服务器会在收到此资料点时自动补上当前的时间戳。

	范例：
	
	```
	1,1432538716989,26
	2,,26.34,12,59
	```
	第一行：资料通道 ID 为 ”1“；”1432538716989“ 为上传数据时，装置或您的应用程式产生的时间戳（timestamp）；”26“ 为上传的值。	
	第二行：资料通道 ID 为 ”2“；时间戳（timestamp）的栏位为空，由 MCS 服务器自动补上；”26.34“、”12“ 与 ”59“为上传的数据(此时的资料通道类型为 GPS)。


* **使用 JSON 格式：**

	语法:
	
	每个 JSON 格式的资料点，都包含下列三种的资料：
	
	1. dataChnId
	2. timestamp
	3. values: 表示资料点的值。某些资料通道的值，可能是有多个数据组成。例如 GPS 通道，就包含了经度、纬度与海拔高度。
	
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
	
	资料点1： 资料通道 ID 为 ”1“；”1432538716989“ 为上传数据时，装置或您的应用程式产生的时间戳（timestamp）；”26“ 为上传的值。
	
	資料点2： 资料通道 ID 为 ”2“；时间戳（timestamp）的栏位为空，由 MCS 服务器自动补上；”26.34“、”12“ 与 ”59“为上传的数据(此时的资料通道类型为 GPS)。	

## HTTP 回覆

### 回覆代码
200

### 表头（Header）

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

## 错误回覆

当错误发生时，MCS 服务器会回应非 200 的错误代码。回覆内容包括以下资讯：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 错误代码 |
| message | String | 错误原因|
| description | String | 详细的错误描述 |

**范例:**

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

