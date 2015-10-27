# 回报装置固件

##描述

使用 **HTTPs PUT** 来向 MCS 平台回报装置使用之固件。


## 请求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares

```
向 MCS 平台回報裝置正在使用的固件。請注意，您必須將此功能自行編碼於您的裝置中，方可使用。


## 动作
HTTPs PUT


## 参数
### Header

deviceKey: `device_key_here`

Content-Type:`application/json`


### 內容
####JSON 格式

```
{
    "version": "fw_version"
}
```
### 回覆格式
回覆格式为 JSON

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
| fwId | string | 装置所回报的固件 ID|
|code| string|http 状态代码|
|message|string|系统讯息|


**范例：**

请求 URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares
```

请求 Header

deviceKey: `g06jBWOtB0kqHk2B`

Content-Type:`application/json`

请求內容
```
{
    "version": "v1"
}
```

回覆內容

```
{
    "apiVersion": "2.8.0",
    "code": 200,
    "message": "Request has succeeded",
    "fwId": "FAa6B540CMmJ"
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
