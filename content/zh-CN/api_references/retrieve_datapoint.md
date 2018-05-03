# 读取资料点

## 描述

使用 **HTTPs GET** 来取得装置上传的资料点

## HTTP 請求
### URL

您可以透过指定 URL 中资源路径与查询参数来读取特定资料通道中的资料点。

* **资源路径**

| 资源名称 | 型别 | 是否必填 | 描述 |
| --- | --- | --- | --- |
| 装置 ID | 字串 | 必填 | 您需在 URL 中指定你所要获取资料的装置 ID |
| 资料通道 ID | 字串 | 必填 | 您需在 URL 中指定你所要获取资料的资料通道 ID |


* **查询参数**

| 参数名称 | 型别 | 是否必填 | 描述 |
| --- | --- | --- | --- |
| start | 数字 | 选填 | 查询起始时间 |
| end | 数字 | 选填 | 查询中止时间 |
| limit | 数字 | 选填 | 要回传的资料点数目 ( 默认值 = 1 ) |
| offset | 数字 | 选填 | 第几笔开始的资料点 |
| order | 字串 | 选填 | 资料预设是按照时间戳，由新到旧回传，您也可透过指定 "asc" 或 "desc" 改变顺序  |
	
MCS 可将您请求的数据回传成 JSON 或是 CSV 格式，您可藉由 HTTP 请求中的资源名称来指定回传的格式。

每次请求最多只能读取 1000 笔资料点。

* **获取 JSON 格式的数据**

	```
	https://api.mediatek.com/mcs/v2/devices/{deviceId}/datachannels/{datachannelId}/datapoints?start={startTime}&end={endTime}&limit={limit}&offset={offset}
	```

* **获取 CSV 格式的数据**

	若您希望数据以 CSV 的格式回传，请在资源名称的最后加上 `.csv`，变成 `datapoints.csv`

	```
	https://api.mediatek.com/mcs/v2/devices/{deviceId}/datachannels/{datachannelId}/datapoints.csv?start={startTime}&end={endTime}&limit={limit}&offset={offset}
	```

**范例**

* 读取最新一个资料点并以 JSON 格式回传：

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sA7iSx/datachannels/my_data_channel/datapoints
	```

* 读取最新一个资料点并以 CSV 格式回传：

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sA7iSx/datachannels/my_data_channel/datapoints.csv
	```

* 读取一段时间范围内的资料点：

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sA7iSx/datachannels/my_data_channel/datapoints?limit=1000&start=1524107855148&end=1524550447427
	```

请注意，若您只使用开始时间（start）和结束时间（end）参数，系统只会回覆您此区间内的最后一笔资料。若您希望取得此区间内的更多资料点，您可以使用 **limit** 来定义您想取得此区间内的几笔资料点。


* 限制您要读取的资料点数目，MCS 只会回传最新的 N 笔资料:

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sA7iSx/datachannels/my_data_channel/datapoints?limit=10	
	```


### 方法（Method）
GET


### 表头（Header）

**存取凭证**

* 透过装置读取数据

	```
	deviceKey: {your_device_key}
	```
* 透过您自行开发的应用（服务提供者帐号）

	```
	appId: {your_appId}
	appSecret: {your_appSecret}
	```


## 回覆

### 回覆代码
200

### 表头（Header）

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

	回应的内文为 JSON 的格式，请求的数据位于 **dataChannels** 物件下的 **dataPoints** 阵列中。


**dataChannels 物件**

| 栏位名称 | 格式 | 描述|
| --- | --- | --- | --- |
| dataChnId | 字串 | 资料通道 ID |
| isOverflow | 布林 | 要求的资料点是否超过数目限制 |
| dataPoints | JSON 物件阵列 | 资料点 |


**dataPoints 陣列**

| 栏位名称 | 格式 | 描述 |
| --- | --- | --- | --- |
| createdAt | 数字 | 以 Unix timestamp 格式纪录的资料点建立时间 |
| values | JSON 物件 | 资料点的值 |


**范例:**

* **以 JSON 格式回传**

	```
	{
	    "apiVersion": "2.18.3",
	    "code": 200,
	    "message": "Request has succeeded",
	    "deviceId": "DL6sA7iSx",
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

* **以 CSV 格式回传**

	```
	my_data_channel,1524119075906,35
	my_data_channel,1524550447427,30
	```


## 错误回覆

当错误发生时，回覆代码为非 200 之其他代码。回覆内容为 JSON 格式并会包括以下资讯：

| 栏位名称 | 格式 | 描述 |
| --- | --- | --- |
| code | 整数 | 错误代码 |
| message | 字串 | 错误描述 |



**范例:**

* **以 CSV 格式回传**

	```
	404,channel not found
	```
	
* **以 JSON 格式回传**	
	
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

