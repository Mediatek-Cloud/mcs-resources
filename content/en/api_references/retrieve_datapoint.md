# Retrieve data points

## Description

Use **HTTPs GET** to retrieve data point values of a device.

## Request
### URL

You can retrieve the data points by specifying the following parameters in the request URI and query string.

* **Resource path**
	
| Resource Name | Type | Required |Description|
| --- | --- | --- | --- |
| device ID | String | Mandatory | You need to specify the device ID for which you would like to get data in the request URL |
| data channel ID | String | Mandatory | You need to specify the data channel ID for which you would like to get data in the request URL |


* **Query string**

	Following fields should be constructed and appended to the end of the URL:
	
| Field Name | Type | Required |Description|
| --- | --- | --- | --- |
| start | Number | Optional | Start Timestamp of the query period |
| end | Number | Optional | End Timestamp of the query period |
| limit | Number | Optional | number of the data points to be returned ( Default = 1 ) |
| offset | Number | Optional | offset of the data points being retrieved |
| order | String | Optional | The data is sorted in descending order of timestamp. You also can "asc" or "desc" to define the order by your own.  |
	

MCS service can return data points in either JSON or CSV format, you can specify the format in the resource name of the HTTP request.

The maximum number of returned data points for each data channel is 1000.

* **Retrieve data points in JSON format**

	```
	https://api.mediatek.com/mcs/v2/devices/{deviceId}/datachannels/{datachannelId}/datapoints?start={startTime}&end={endTime}&limit={limit}&offset={offset}
	```

* **Retrieve data points in CSV format**

	If you would like to retrieve the data points in CSV format, please add `.csv` in the resource name.
	
	```
	https://api.mediatek.com/mcs/v2/devices/{deviceId}/datachannels/{datachannelId}/datapoints.csv?start={startTime}&end={endTime}&limit={limit}&offset={offset}
	```

**Examples**

* To get the latest data point in JSON format:

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sA7iSx/datachannels/my_data_channel/datapoints
	```
	
* To get the latest data point in CSV format:

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sA7iSx/datachannels/my_data_channel/datapoints.csv
	```

* To get the data points within a time frame:

	```
	https://api.mediatek.com/mcs/v2/devices/DL6sA7iSx/datachannels/my_data_channel/datapoints?limit=1000&start=1524107855148&end=1524550447427
	```
	
	You have to use **start**, **end** and also **limit** to identify how many data points within a specified  time frame you would like to retrieve.
	If there is no **limit** parameter, MCS service only returns the latest data point of that period. 


* To limit the number of data points. MCS service only returns the latest N data points.
	
	```
	https://api.mediatek.com/mcs/v2/devices/DL6sA7iSx/datachannels/my_data_channel/datapoints?limit=10	
	```

### Method
GET

### Header

**Access token**

* Retrieved by device	

	```
	deviceKey: {your_device_key}
	```

* Retrieved by your own App (Service provider account)

	```
	appId: {your_appId}
	appSecret: {your_appSecret}
	```
	You can get the appId and appSecret under the Service provider section in the Profile page.


## Response

### Response Code
200

### Header

* **For JSON format:**

	```
	content-type: text/html
	```

* **For CSV format:**
	
	```
	content-type: application/json	
	```

### Body

* **For JSON format:**

	The response body is constructed in JSON format and the data points are wrapped in the **dataPoints** array under **dataChannels** object. 

**dataChannels object**

| Field Name | Type | Description|
| --- | --- | --- | --- |
| dataChnId | String | Data Channel ID |
| isOverflow | Bool | Is the number of queried data points more than maximum number|
| data points | Object Array | All the data points that matches your query criteria |


**dataPoints Array**

| Field Name | Type | Description|
| --- | --- | --- | --- |
| recordedAt | Number | Unix timestamp of the data point|
| values | Object | The values of a data point |


**Example:**

* **Response in JSON format**

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

* **Response in CSV format**

	```
	my_data_channel,1524119075906,35
	my_data_channel,1524550447427,30
	```



## Error Response

When error is incurred, the response code will be non-200 and the response body will construct in JSON format with the following fields:

| Field Name | Type |Description|
| --- | --- | --- |
| code | Integer | Error code |
| message | String | General error message |


**Example:**

* **For CSV format:**

	```
	404,channel not found
	```
	
* **For JSON format:**	
	
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
