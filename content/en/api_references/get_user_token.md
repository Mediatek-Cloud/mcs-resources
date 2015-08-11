# Get User Token

## Description

Use **HTTPs POST** to get the user token from MCS.


## Request URL

```
https://mcs.mediatek.io/oauth/login/thirdpart

```
To get the user token from MCS to allow you to apply for the user access token to access the MCS APIs from your own third party service.

To use this API to get the user access token, you have to first apply for the AppId and AppSecret from the MCS web console. You can find the apply link in the service provider section in the user profile page. The user token will expire every two weeks.


## Action
HTTPs POST


## Parameters
### Header

authorization: `Basic {app key: app secret}.base64'd`

After you get the AppId and AppSecret, you have to encode the string `appId:appSecret` to get the authorization code.

You can use the following link to do the encoding:
https://www.base64encode.org/

For example, you encode the following string using base 64: `AuMgS2MPK5Z6nqWhVsyV:o1uBjWTzuqbaMnQzSmDp7UhR6M33NOhb5XL0b1YK`

and you will get `QXVNZ1MyTVBLNVo2bnFXaFZzeVY6bzF1QmpXVHp1cWJhTW5RelNtRHA3VWhSNk0zM05PaGI1WEwwYjFZSw==`


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
|access token| array|the user access token to MCS API, also known as the bearer token|


**Example:**

Request URL
```
https://mcs.mediatek.io/oauth/login/thirdpart
```

Response Body

```
{
"apiVersion": "0.0.1",
"code": 200,
"message": "Request has succeeded",
"token": "***",
"access_token": "***"
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
