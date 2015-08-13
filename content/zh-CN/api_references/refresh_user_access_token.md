# 重新取得 User Access Token

## 描述

使用 **HTTPs POST** 來從 MCS 重新取得 user access token。


## 请求 URL


```
http://mcs.mediatek.com/oauth/login/thirdpart/refresh

```

使用者可以使用 user access token 来从第三方服务使用 MCS APIs 存取资料。

为了使用此 API 取得 user access token，您需要先有 user token。您需要注意，此 user acces token 使用期限为一个小时。



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

| 栏位名称| | 格式 |描述|
| --- | --- | --- | --- |
| token | array | user token |
|access token| array|使用者用來存取 MCS APIs 的 user access token|
|Timezone| array |使用者时区|
|User Image url| array| 使用者图像 url|
|nick name| array| 使用者昵称|
|email| array| 使用者电子邮件地址|
|language| array|使用者设定之语言|
|plan|array|使用者帐户类型|


**范例：**

请求 URL
```
http://mcs.mediatek.com/oauth/login/thirdpart/refresh
```

请求 Header
```
authorization: ` QnVNZ1MyTVBLNVo2bnFXaFZzeVY6bzF1QmpXVHp1cWJhTW5RelNtRHA1VWhSNk0zM05PaGIzWUwwYjFZSw==`
```

请求內容
```
{
    "token": "***"
}
```

回覆內容

```
{
    "apiVersion": "0.0.1",
    "code": 200,
    "message": "Request has succeeded",
    "results": {
        "access_token": "***",
        "userImageURL": "profile/1234567890.jpg",
        "timezone": "Asia/Taipei",
        "email": "mcsuser@mediatek.com",
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
