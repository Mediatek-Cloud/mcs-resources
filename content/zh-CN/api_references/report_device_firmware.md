# 回报装置固件版本

##描述

使用 **HTTPs PUT** 来向 MCS 平台回报装置的固件版本。


## 请求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares

```
装置可使用此 API 向 MCS 平台回报当前正在使用的固件版本。请注意，回报的版本号码，必须是先前已经上传至 MCS 平台的固件之一。

首次启用装置时，可透过呼叫此 API 来回报装置固件资讯，以方便后续装置版本的管理。此外，当装置完成固件更新时，亦可用来更新 MCS 平台上此装置的固件资讯，同时代表更新成功。


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
| fwId | string | 装置回报的固件版本所对应到的固件 ID|
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
