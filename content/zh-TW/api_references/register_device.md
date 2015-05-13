# 註冊裝置

## 描述

使用 **HTTPs POST**來註冊裝置

## 請求 URL

```
https://api.mediatek.com/mcs/v2/devices

```

## 動做
HTTPs POST

## 參數

### Header

Authorization: Bearer '{token}'

### 請求內容

JSON格式的請求內容會包含以下幾個欄位：

| 欄位名稱 | 格式 | 是否必填 |描述|
| --- | --- | --- | --- |
| prodId | String | Yes | 產品原型 ID |
| name | String | Yes | 裝置名稱 |
| isTest | Bool | Yes | 是否為測試裝置 |
| description | String | No | 裝置描述 |
| serial | String | No | 開發者可定義是否使用序號。若isTest為真，則不需要。 |
| deviceImageURL | String | No | 裝置圖片url |




## 回覆

### 回覆代碼
200

### 回覆 Header

Content-Type:`application/json`

### 回覆內容

***回覆格式: JSON***

JSON格式的回覆內容會包含以下幾個欄位：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| deviceId | String | Device ID |
| deviceKey | String | Device Key |
| chipName | String | 晶片名稱 |

**範例：**

請求 URL
```
https://api.mediatek.com/mcs/v2/devices
```

請求內容

```
{

         "prodId":"b1234567890",
         "name":"My 2nd device",
         "isTest":false,
         "serial":"mtk-01234",
         "deviceImageURL":"/device/mydevice.jpg"

}
```

回覆內容

```
{

         "deviceId":"d1234567890",
         "deviceKey":"0987654321d",
         "chipName":"MT7681"

}
```

## 錯誤回覆
當錯誤發生時，回覆代碼為非200之其他代碼。回覆內容為JSON格式並會包括以下資訊：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 錯誤代碼 |
| url | String | API錯誤頁面url|
| description | String | 錯誤描述 |

**範例:**

```
{
  "results": {
    "code": 1002,
    "url": "http://mcs.mediatek.com/api_errorcode?code=1002",
    "description": "You do not have access right to this API"
  }
}
```
