# 啟用裝置

## 描述

使用 **HTTPs GET** 來啟用裝置


## 請求 URL
使用以下API來啟用您的裝置

```
https://api.mediatek.com/mcs/v2/devices/activate/:activationCode

```

## 動作
HTTPs GET


## 參數
### Header

Content-Type:`application/json`


### Return Type
The return format is in json format

## 回覆

### 回覆代碼
200

### 回覆 Header
For JSON response:
```
Content-Type:`application/json`
```

### 回覆內容

***回覆格式: JSON***

JSON格式的回覆內容會包含以下幾個欄位

| 欄位名稱 | 資料型態 | 描述 |
| --- | --- | --- | --- |
| code | String | http status code |
| deviceKey | String | The deviceKey |
| deviceId | String | The deviceId |
| chipname | String | The device name |
| message | String | System log message |


**範例:**

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
    "deviceKey": "yQGymH0IRWFSVC37",
    "chipName": "Device for IoT prototype"
}

```


## 錯誤回覆


當有錯誤發生時，回傳非200之其他回覆代碼。回覆內容為JSON格式並包含以下資訊：

| 欄位名稱 | 資料型態 | 描述 |
| --- | --- | --- |
| code | Integer | Error Code |
| message | String | Error Description |

**範例:**

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


