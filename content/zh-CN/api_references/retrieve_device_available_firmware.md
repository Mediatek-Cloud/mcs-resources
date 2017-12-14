# 取得与此装置相容的固件列表


## 描述

使用 **HTTPs GET** 從 MCS 平台取得该装置可使用的所有固件列表。


## 请求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares/available

```
取得装置所有可使用的固件列表。

若您已将装置的固件版本回报至 MCS 平台，您可以使用此 API 获取相容的固件资讯，包含固件的下载网址。若您未曾回报装置的固件版本，其回传的固件资讯为无版本相容性限制的所有固件资讯。

### 查詢參數
可將下列參數帶入請求 URL  

| Field Name | Type | Required |Description|
| --- | --- | --- | --- |
| url | 字串 | 布林值 | 为非必要的参数。加上 **url=true** 後，伺服器將會回傳各固件的下載網址|

## 动作
HTTPs GET


## 参数
### Header


deviceKey: `device_key_here`

Content-Type:`application/json`


### 回覆格式
回覆格式為 JSON

## 回覆

### 回覆代码
200

### 回覆 Header
JSON 格式：
```
Content-Type:`application/json`
```

### 回覆內容

***JSON 格式***

JSON 格式的回覆内容会包含以下几个栏位：

|栏位名称|格式|描述|
| --- | --- | --- | --- |
| results | array | 该装置所有可使用的固件列表，其中包含以下资讯 <br> 1. fwid: 固件 ID <br> 2. name <br> 3. description <br> 4. version <br> 5. URL: 固件的下载网址 (需在请求中加入 **url=true** 的查询参数) |
|code| string|http 状态代码|
|message|string|系统讯息|


**范例：**

请求 URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares/available
```

请求 Header

deviceKey: `g06jBWOtB0kqHk2B`

Content-Type:`application/json`


回覆內容

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


## 错误回覆

当错误发生时，回覆代码为非 200 之其他代码。回覆内容为 JSON 格式并会包括以下资讯：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 错误代码 |
| message | String | 错误描述 |

**范例：**

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

