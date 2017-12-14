# 取得與此裝置相容的韌體列表


## 描述

使用 **HTTPs GET** 從 MCS 平台取得該裝置可使用的所有韌體列表。


## 請求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares/available

```
取得裝置所有可使用的韌體列表。

若您已將裝置的韌體版本回報至 MCS 平台，您可以使用此 API 獲取相容的韌體資訊，包含韌體的下載網址。若您未曾回報裝置的韌體版本，其回傳的韌體資訊為無版本相容性限制的所有韌體資訊。


### 查詢參數
可將下列參數帶入請求 URL  

| Field Name | Type | Required |Description|
| --- | --- | --- | --- |
| url | 字串 | 布林值 | 非必要的参数。加上 **url=true** 後，伺服器將會回傳各韌體的下載網址|

## 動作
HTTPs GET


## 參數
### Header


deviceKey: `device_key_here`

Content-Type:`application/json`


### 回覆格式
回覆格式為 JSON

## Response

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
| results | array | 該裝置所有可使用的韌體列表，其中包含以下資訊 <br> 1. fwid: 韌體 ID <br> 2. name <br> 3. description <br> 4. version <br> 5. URL: 韌體的下載網址 (需在請求中加入 **url=true** 的查詢參數)  |
|code| string|http 狀態代碼|
|message|string|系統訊息|


**範例：**

請求 URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares/available
```

請求 Header

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

