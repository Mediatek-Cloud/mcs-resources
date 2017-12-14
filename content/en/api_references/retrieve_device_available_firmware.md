# Retrieve Device Available Firmware


## Description

Use **HTTPs GET** to retrieve the available firmwares for this device from MCS.


## Request URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares/available

```
To retrieve the available firmwares for this device. 

If this device has reported its firmware version to MCS platform, this API provides a list of firmwares which are compatible with the current version. If the device hasn't reported any firmware yet, then, only the firmwares without any compatibility limitation are listed.

### Query string

Following fields could be constructed and appended to the end of the URL:

| Field Name | Type | Required |Description|
| --- | --- | --- | --- |
| url | string | boolean | An optional parameter. Append **url=true** to get the download URL in the response.|



## Action
HTTPs GET


## Parameters
### Header

deviceKey: `device_key_here`

Content-Type:`application/json`


### Return format
The return format is in JSON format

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
| results | array | the available firmware list for the device, and it includes <br> 1. fwid: The firmware ID <br> 2. name <br> 3. description <br> 4. version <br> 5. URL: The firmware download URL (If there is a query string, **url=true**, in the request) |
|code| string|http status code|
|message|string|system log message|


**Example:**

Request URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares/available
```

Request Header

deviceKey: `g06jBWOtB0kqHk2B`

Content-Type:`application/json`


Response Body

```
{
    "apiVersion": "2.8.0",
    "code": 200,
    "message": "Request has succeeded",
    "results": [
        {
            "fwid": "FAdJBknrDsOM",
            "name": "hello firmware",
            "description": null,
            "version": "1"
        },
        {
            "fwid": "Fwnx3ZBxOLCK",
            "name": "firmware_2",
            "description": null,
            "version": "2"
        }
    ]
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
    "code": 401,
    "message": "401 Unauthorized",
    "errors": [
        {
            "code": 401,
            "message": "401 Unauthorized"
        }
    ],
    "results": "you dont have permission!",
    "statusCode": 401,
    "options": {}
}
```

