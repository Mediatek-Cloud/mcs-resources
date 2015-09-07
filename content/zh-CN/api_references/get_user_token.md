# 取得 User Token

## 描述

使用 **HTTPs POST** 来从 MCS 取得 user token。


## 请求 URL

```
https://mcs.mediatek.com/oauth/login/thirdpart

```
MCS 提供使用者可以申请 user token，让使用者利用取得 user access token。 使用者可以透过此 user access token 从第三方服务利用 MCS APIs 以取得资料。

为了能够利用此 API 来取得使用者 acces token，您需要先在 MCS 网站先申请 AppKeyd 和 AppSecret。您可以在用戶設定頁面中的第三方服務專區，申請取得此兩項資訊。您需要注意，user token 每两周将会过期。


## 动作
HTTPs POST


## 参数
### Header

authorization: `Basic {app key: app secret}.base64'd`

当您取得 AppId 和 AppSecret 之后，您需要使用 64 base 加密此字串：`appKey:appSecret`

您可以使用此连结来执行加密动作：
https://www.base64encode.org/

举例来说，将以下此字串使用 64 base 加密：
 `BuMgS2MPK5Z6nqWhVsyV:o1uBjWTzuqbaMnQzSmDp5UhR6M33NOhb3YL0b1YK`

加密之后，您将会取得： `QnVNZ1MyTVBLNVo2bnFXaFZzeVY6bzF1QmpXVHp1cWJhTW5RelNtRHA1VWhSNk0zM05PaGIzWUwwYjFZSw==`


### 回覆格式

回覆格式是 JSON

## 回覆

### 回覆代码
200

### 回覆 Header

JSON格式:
```
Content-Type:`application/json`
```

### 回覆內容

***回覆格式: JSON***

JSON 格式的回覆内容会包含以下几个栏位：

| 栏位名称 | 格式 |描述|
| --- | --- | --- | --- |
| token | array | user token |
|access token| array|使用者用来存取 MCS APIs 的 user access token, 即为 bearer token|


**范例：**

请求 URL
```
https://mcs.mediatek.com/oauth/login/thirdpart
```

請求 Header
```
Authorization: `Basic QnVNZ1MyTVBLNVo2bnFXaFZzeVY6bzF1QmpXVHp1cWJhTW5RelNtRHA1VWhSNk0zM05PaGIzWUwwYjFZSw==`
```


请求內容
```
{
    "email": "MCSuser@mediatek.com",
    "password": "123456789"
}
```

回覆內容

```
{
"apiVersion": "0.0.1",
"code": 200,
"message": "Request has succeeded",
"token": "***",
"access_token": "***"
}

```
## 错误回覆

当错误发生时，回覆代码为非 200 之其他代码。回覆内容为 JSON 格式并会包括以下资讯：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 错误代码 |
| message | String | 错误描述 |

**范例：**

```
{
    "apiVersion": "0.0.1",
    "code": 500,
    "message": "Invalid or missing client_id parameter",
    "statusCode": 500,
    "options": {}
}
```


