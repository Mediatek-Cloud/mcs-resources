# 啟用裝置

## 描述

使用 **HTTPs GET** 來啟用裝置


## 請求 URL
使用以下 API 來啟用您的裝置

```
https://api.mediatek.com/mcs/v2/devices/activate/:activationCode

```

## 動作
HTTPs GET


## 參數
### Header

Content-Type:`application/json`


### 回覆格式
回覆格式是 JSON 格式

## 回覆

### 回覆代碼
200

### 回覆 Header
JSON 格式：
```
Content-Type:`application/json`
```

### 回覆內容

***回覆格式： JSON***

JSON格式的回覆內容會包含以下幾個欄位

| 欄位名稱 | 資料型態 | 描述 |
| --- | --- | --- | --- |
| code | String | http 狀態碼 |
| deviceKey | String | The device key |
| deviceId | String | The device ID |
| chipname | String | 設備名稱 |
| message | String | 系統日誌 |


**範例：**

請求 URL
```
https://api.mediatek.com/mcs/v2/devices/activate/edb4b2eil152
```

請求 Header

Content-Type:`application/json`


回覆內容

```
{
    "apiVersion": "2.10.1",
    "code": 200,
    "message": "Request has succeeded",
    "deviceId": "JU5z4yVF",
    "deviceKey": "yQGymH0IRWFSVC**",
    "chipName": "Device for IoT prototype"
}

```


## 錯誤回覆


當有錯誤發生時，回傳非 200 之其他回覆代碼。回覆內容為 JSON 格式並包含以下資訊：

| 欄位名稱 | 資料型態 | 描述 |
| --- | --- | --- |
| code | Integer | 錯誤代碼 |
| message | String | 錯誤說明 |

**範例：**

```
{
    "apiVersion": "2.10.1",
    "code": 400,
    "message": "Wrong activate Code.",
    "errors": [
        {
            "code": 400,
            "message": "400 Bad Request"
        }
    ],
    "statusCode": 400,
    "options": {}
}
```


