# Report Device Firmware Version

## Description

Use **HTTPs PUT** to report the current firmware version of the device to MCS.


## Request URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares

```
The device is able to report its current firmware version to MCS platform by using this API. Please note: The reported version must be one of the uploaded firmwares on MCS platform.

This API could be used by device to report its initial firmware version when it boots up for the first time and then keep this firmware information updated when the firmware upgrade is done. This could be a useful information for device management.

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
| fwId | string | the firmware ID of this reported version |
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
