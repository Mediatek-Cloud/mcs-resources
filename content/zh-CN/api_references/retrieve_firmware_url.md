# 取得固件 URL

## 描述

使用 **HTTPs GET** 来取得您的装置欲更新之特定固件下载 url。


## 请求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares/:fwId/url

```
来取得您的装置欲更新之特定固件下载 url。

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
JSON 格式
```
Content-Type:`application/json`
```

### 回覆內容

***JSON 格式***

JSON 格式的回覆内容会包含以下几个栏位：

|栏位名称|格式|描述|
| --- | --- | --- | --- |
| url | array | 固件下载 url |
|code| string|http 状态代码|
|message|string|系统讯息|


**范例：**

请求 URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares/FAdJBknrDsOm/url
```

请注意，您可以呼叫**取得装置所有固件资讯** API 以取得 **firmware id**。

请求 Header

deviceKey: `g06jBWOtB0kqHk2B`

Content-Type:`application/json`


回覆內容

```
{
    "apiVersion": "2.8.0",
    "code": 200,
    "message": "Request has succeeded",
    "url": "https://s3-ap-southeast-1.amazonaws.com/mtk.linkit/firmwares/PvFn1zENgBei/firmware1.bin"
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

