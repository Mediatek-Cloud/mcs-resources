# Device Activation

## Description

Use **HTTPs GET** to activate the device.


## Request URL
```
https://api.mediatek.com/mcs/v2/devices/activate/:activationCode

```
To activate the device.

## Action
HTTPs GET


## Parameters
### Header

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

| Field Name | Type | Description |
| --- | --- | --- | --- |
| code | string | http status code |
| deviceKey | string | the deviceKey |
| deviceId | string | the deviceId |
| chipname | string | the device name |
| message | string | system log message |


**Example:**

Request URL
```
https://api.mediatek.com/mcs/v2/devices/activate/edb4b2eil152
```

Request Header


Content-Type:`application/json`


Response Body

```
{
    "apiVersion": "2.10.1",
    "code": 200,
    "message": "Request has succeeded",
    "deviceId": "JU5z4yVF",
    "deviceKey": "yQGymH0IRWFSVC37",
    "chipName": "Device for IoT prototype"
}

```


## Error Response


When error is incurred, the response code will be non-200 and the response body will construct in JSON format with the following fields:

| Field Name | Type |Description |
| --- | --- | --- |
| code | Integer | Error Code |
| message | String | Error Description |

**Example:**

```
{
    "apiVersion": "2.10.1",
    "code": 400,
    "message": "Wrong activate Code.",
    "errors": [
        {
            "code": 400,
            "message": "400 Bad Request"
        }
    ],
    "statusCode": 400,
    "options": {}
}
```


