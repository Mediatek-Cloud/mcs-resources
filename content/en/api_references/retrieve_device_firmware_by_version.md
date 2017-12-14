# Retrieve Compatible Firmware by Version

## Description

Use **HTTPs GET** to retrieve the compatible firmwares for a specified firmware version.


## Request URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares/available/:versionId

```
This API provides a flexibility to query the compatible firmwares for a specified firmware version.

### Query string

Following fields could be constructed and appended to the end of the URL:

| Field Name | Type | Required |Description|
| --- | --- | --- | --- |
| url | string | boolean | append **url=true** to get the download URL in the response.|

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
| results | array | the compatible firmwares list for the specified firmware version, please refer to **/firmware/available** API |
|code| string|http status code|
|message|string|system log message|


**Example:**

Request URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares/available/1
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
            "version": "2"
        },
        {
            "fwid": "Fwnx3ZBxOLCK",
            "name": "firmware_2",
            "description": null,
            "version": "3"
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


