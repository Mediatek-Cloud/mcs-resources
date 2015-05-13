# 上傳資料點

## 描述

使用 **HTTPs POST** 來上傳資料點

## 請求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/datapoints

```

API請求默認值為json格式，如欲使用csv格式，請在API請求URL最後端加上`.csv`。

## 動作
HTTPs POST

## 參數

### Header

**Token**

若是裝置：

```
deviceKey: `device_key_here`
```
若是使用者：
```
Authorization: Bearer `{token}`
```

**Content Type**

JSON 格式:
```
Content-Type:`application/json`
```

Comma Separated Value (CSV) 格式:
```
Content-Type:`text/csv`
```


### 內容

#### CSV 格式:

語法:

*:Data_Channel_Id_1, :Timestamp, :Value_1, :Value_2, :Value_3\n*

*:Data_Channel_Id_2, :Timestamp, :Value_1\n*

如欲參考更多詳細的資料通道類型之格式，請參考以下連結
[here](api_references#data_channel_format).

請注意：若您不需要上傳裝置的時間點,則您可保持*:Timestamp*為空(但保留逗號)，此時時間點則會由MCS所收到資料點的時間。


範例：
```
1,946684800,26
2,,26.34,12,59
```
第一行：資料通道ID為1，並且給予時間點，26為上傳的值(此時的資料通道類型為整數)。

第二行：資料通道ID為2，並且不給予時間點，26.34為上傳的值(此時的資料通道類型為浮點數)。


#### JSON 格式

語法:

每個JSON格式的資料點，都包含下列三種型態的資料：

*dataChnId, timestamp, values*

Values是資料點的值，大部分情況下代表一個值。但也有例外，例如GPS資料就會有三個值。

```
{
   "datapoints":[
      {
         "dataChnId":"1",
         "timestamp":946684800,
         "values":{
            "value":"26"
         }
      },
      {
         "dataChnId":"2",
         "timestamp":946684800,
         "values":{
            "latitude":"26.34",
            "longitude":"12",
            "altitude":"59"
         }
      }
   ]
}

```

資料點1： 資料通道ID為1，並且給予時間點，26為上傳的值(此時的資料通道類型為整數)。

資料點2： 資料通道ID為2，並且給予時間點，緯度26.34，經度12，高度59，為上傳的值(此時的資料通道類型為GPS)。

請注意，我們在此使用的unix timestamp miniseconds時間值，若須轉換成可讀格式，您可以使用以下連結：
http://www.epochconverter.com/

## 回覆

### 回覆代碼
200

### 回覆 Header

Content-Type:`application/json`

### 回覆內容

**範例:**

請求 URL：
```
https://api.mediatek.com/mcs/v2/devices/d1234567890/datapoints
```

請求內容：

```
1,946684800,26
2,,26.34,12,59
```

回覆內容：

```
{
    "results": "success"
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
    "results": "None of the data points is valid.",
    "descriptions": [
        "The type of uploaded data point for data channel test01 is not matched to Switch"
    ]
}
```
