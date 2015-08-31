# 取得韌體 URL

## Description

使用 **HTTPs GET** 來取得您的裝置欲更新之特定韌體下載 url。


## 請求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/firmwares/:fwId/url

```
來取得您的裝置欲更新之特定韌體下載 url。

## 動作
HTTPs GET


## 參數
### Header


deviceKey: `device_key_here`

Content-Type:`application/json`


### 回覆格式
回覆格式為 JSON

## 回覆

### 回覆代碼
200

### 回覆 Header
JSON 格式
```
Content-Type:`application/json`
```

### 回覆內容

***JSON 格式***

JSON 格式的回覆內容會包含以下幾個欄位：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- | --- |
| url | array | 韌體下載 url |
|code| string|http 狀態代碼|
|message|string|系統訊息|


**範例：**

請求 URL
```
https://api.mediatek.com//mcs/v2/devices/DAWfOAsi/firmwares/FAdJBknrDsOm/url
```

請注意, 您可以呼叫**取得裝置所有韌體資訊** API 以取得 **firmware id**。

請求 Header

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

