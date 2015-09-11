# Refresh User Access Token

## Description

Use **HTTPs POST** to refresh the user access token from MCS.


## Request URL


```
http://mcs.mediatek.com/oauth/login/thirdparty/refresh

```
To get the user access token from MCS to access the MCS APIs from your own third party service.

To use this API to get the user access token, you have to first get the user token from MCS. The user access token will expire every hour.


## Action
HTTPs POST


## Parameters
### Header

authorization: `Basic {app key: app secret}.base64'd`

After you get the AppKey and AppSecret, you have to encode the string `appKey:appSecret` to get the authorization code.

You can use the following link to do the encoding:
https://www.base64encode.org/

For example, you encode the following string using base 64: `BuMgS2MPK5Z6nqWhVsyV:o1uBjWTzuqbaMnQzSmDp5UhR6M33NOhb3YL0b1YK`

and you will get `QnVNZ1MyTVBLNVo2bnFXaFZzeVY6bzF1QmpXVHp1cWJhTW5RelNtRHA1VWhSNk0zM05PaGIzWUwwYjFZSw==`

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
| token | array | the user token |
|access token| array|the user access token to MCS API|
|Timezone| array |User timezone|
|User Image url| array| User image url|
|nick name| array| User nick name|
|email| array| User email address|
|language| array|User setting language|
|plan|array|User account plan|


**Example:**

Request URL
```
http://mcs.mediatek.com/oauth/login/thirdparty/refresh
```

Request Header
```
        "nickname": "MCS User",
        "language": "zh-TW",
        "plan": {
            "name": "Free plan",
            "deviceCount": 10,
            "dataPointCount": 100000,
            "emailCount": 100
        },
        "token": "***"
    }
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
    "apiVersion": "0.0.1",
    "code": 500,
    "message": "Invalid or missing client_id parameter",
    "statusCode": 500,
    "options": {}
}
```

