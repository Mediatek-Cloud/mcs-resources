# Report Device Firmware

## Description

Use **HTTPs PUT** to report the firmware of the device to MCS.


## Request URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares

```
To report the current firmware the device is using to the MCS. Please note that for MCS to get the firmware, you have to implement this API in your device to report the device firmware.

## Action
HTTPs PUT


## Parameters
### Header


deviceKey: `device_key_here`

Content-Type:`application/json`


### Body
#### For JSON format

```
{
    "version": "fw_version"
}
```

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
| fwId | string | the firmware ID the device reported using |
|code| string|http status code|
|message|string|system log message|


**Example:**

Request URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares
```

Request Header

deviceKey: `g06jBWOtB0kqHk2B`

Content-Type:`application/json`

Request Body
```
{
    "version": "v1"
}
```

Response Body

```
{
    "apiVersion": "2.8.0",
    "code": 200,
    "message": "Request has succeeded",
    "fwId": "FAa6B540CMmJ"
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
