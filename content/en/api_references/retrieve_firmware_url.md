# Retrieve Firmware URL

## Description

Use **HTTPs GET** to retrieve the firmware download url that the device want to download.


## Request URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares/:fwId/url

```
To retrieve the firmware url this device wants to download.

## Action
HTTPs GET


## Parameters
### Header


deviceKey: `device_key_here`

Content-Type:`application/json`


### Return format
The return format is in json format

## Response

### Response Code
200

### Response Header
For JSON response:
```
Content-Type:`application/json`
```

### Response Body

***Data Format: JSON***

The response body will construct in JSON format with the following fields:

| Field Name | Type | Description|
| --- | --- | --- | --- |
| url | array | the firmware download url |
|code| string|http status code|
|message|string|system log message|


**Example:**

Request URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares/FAdJBknrDsOm/url
```

Please be noted, you can get the **firmware id** by calling the **retrieve device available firmware** API.

Request Header

deviceKey: `g06jBWOtB0kqHk2B`

Content-Type:`application/json`


Response Body

```
{
    "apiVersion": "2.8.0",
    "code": 200,
    "message": "Request has succeeded",
    "url": "https://s3-ap-southeast-1.amazonaws.com/mtk.linkit/firmwares/PvFn1zENgBei/firmware1.bin"
}

```


## Error Response


When error is incurred, the response code will be non-200 and the response body will construct in JSON format with the following fields:

| Field Name | Type |Description|
| --- | --- | --- |
| code | Integer | Error Code |
| message | String | Error Description |

**Example:**

```
{
    "apiVersion": "2.8.0",
    "code": 404,
    "message": "404 Not Found",
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

