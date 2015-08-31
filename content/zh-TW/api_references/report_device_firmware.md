# 回報裝置韌體

## 描述

使用 **HTTPs PUT** 來向 MCS 平台回報裝置使用之韌體。


## 請求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares

```
向 MCS 平台回報裝置正在使用的韌體。請注意，您必須將此功能自行編碼於您的裝置中，方可使用。


## 動作
HTTPs PUT


## 參數
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
回覆格式為 JSON

## 回覆

### 回覆代碼
200

### 回覆 Header
JSON 格式：
```
Content-Type:`application/json`
```

### 回覆內容

***JSON 格式***

JSON 格式的回覆內容會包含以下幾個欄位：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- | --- |
| fwId | string | 裝置所回報的韌體 ID|
|code| string|http 狀態代碼|
|message|string|系統訊息|


**範例：**

請求 URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares
```

請求 Header

deviceKey: `g06jBWOtB0kqHk2B`

Content-Type:`application/json`

請求內容
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


## 錯誤回覆

當錯誤發生時，回覆代碼為非 200 之其他代碼。回覆內容為 JSON 格式並會包括以下資訊：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 錯誤代碼 |
| message | String | 錯誤描述 |

**範例：**

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
