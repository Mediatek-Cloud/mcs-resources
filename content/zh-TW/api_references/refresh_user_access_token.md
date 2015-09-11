# 重新取得 User Access Token

## 描述

使用 **HTTPs POST** 來從 MCS 重新取得 user access token。


## 請求 URL


```
http://mcs.mediatek.com/oauth/login/thirdparty/refresh

```

使用者可以使用 user access token 來從第三方服務使用 MCS APIs 存取資料。

為了使用此 API 取得 user access token，您需要先有 user token。您需要注意，此 user acces token 使用期限為一個小時。



## 動作
HTTPs POST


## 參數
### Header

authorization: `Basic {app key: app secret}.base64'd`

當您取得 AppKey 和 AppSecret 之後，您需要使用 64 base 加密此字串：`appKey:appSecret`

您可以使用此連結來執行加密動作：
https://www.base64encode.org/

舉例來說，將以下此字串使用 64 base 加密：
 `BuMgS2MPK5Z6nqWhVsyV:o1uBjWTzuqbaMnQzSmDp5UhR6M33NOhb3YL0b1YK`

加密之後，您將會取得： `QnVNZ1MyTVBLNVo2bnFXaFZzeVY6bzF1QmpXVHp1cWJhTW5RelNtRHA1VWhSNk0zM05PaGIzWUwwYjFZSw==`


### 回覆格式

回覆格式是 JSON

## 回覆

### 回覆代碼
200

### 回覆 Header

JSON格式:
```
Content-Type:`application/json`
```

### 回覆內容

***回覆格式: JSON***

JSON 格式的回覆內容會包含以下幾個欄位：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- | --- |
| token | array | user token |
|access token| array|使用者用來存取 MCS APIs 的 user access token|
|Timezone| array |使用者時區|
|User Image url| array| 使用者圖像 url|
|nick name| array| 使用者暱稱|
|email| array| 使用者電子郵件地址|
|language| array|使用者設定之語言|
|plan|array|使用者帳戶類型|


**範例：**

請求 URL
```
http://mcs.mediatek.com/oauth/login/thirdparty/refresh
```

請求 Header
```

authorization: Basic QnVNZ1MyTVBLNVo2bnFXaFZzeVY6bzF1QmpXVHp1cWJhTW5RelNtRHA1VWhSNk0zM05PaGIzWUwwYjFZSw==

```

請求內容
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


## 錯誤回覆

當錯誤發生時，回覆代碼為非 200 之其他代碼。回覆內容為 JSON 格式並會包括以下資訊：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 錯誤代碼 |
| message | String | 錯誤描述 |

**範例：**

```
{
    "apiVersion": "0.0.1",
    "code": 500,
    "message": "Invalid or missing client_id parameter",
    "statusCode": 500,
    "options": {}
}
```

