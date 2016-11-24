# 讀取資料點

## 描述

使用 **HTTPs GET** 來取得裝置回傳的資料點


## 請求 URL

讀取特定資料通道中的資料點：

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/datachannels/:datachannelId/datapoints?start=:startTime&end=:endTime&limit=:limit&offset=:offset

```

API 請求默認值為 JSON 格式，如欲使用 CSV 格式，請在 API 請求 URL 最後端加上`.csv`。
使用此 API，您可以選擇您要的資料範圍：

* 只讀取最後一個資料點：
```
https://api.mediatek.com/mcs/v2/devices/:deviceId/datachannels/:datachannelId/datapoints
```


* 讀取一段時間範圍內的資料點：
```
在請求url尾端加上`?start=:startTime&end=:endTime`
```

請注意，若您只使用開始時間和結束時間，系統只會回覆您此區間內的最後一筆資料。若您希望取得此區間內的更多資料點，您可以使用 **limit** 來定義您想取得此區間內的幾筆資料點。


* 限制您要讀取的資料點數目 (舉例來說, 如果您輸入 limit=5, 則您會讀取前五筆資料點):
```
在請求url尾端加上 `?limit=:limit`
```



您亦可以將以上四種方式混合使用。

### 查詢字串
下面幾種查詢方式亦可以使用

| 欄位名稱 | 格式 | 是否必填 |描述|
| --- | --- | --- | --- |
| start_time | Number | Optional | 查詢起始時間 |
| end_time | Number | Optional | 查詢中止時間 |
| limit | Number | Optional | 要回傳的資料點數目 ( 默認值 = 1 ) |
| offset | Number | Optional | 第幾筆開始的資料點 |

**請注意：**

1.
使用 limit 查詢最後 *n (n=數目)* 的資料點時，將不能指定 *start_time* 與 *end_time*時。

2.　當您指定 *start_time* 和 *end_time* 時，若還是有使用設定回傳資料點數目，此時，此回傳資料點數目的查詢將會被忽略。


**每次請求最多只能讀取 1000 筆資料點**


## 動作
HTTPs GET

## 參數

### Header

Device Key
```
deviceKey: `device_key_here`
```

### 回覆格式
您能選擇回覆 JSON 或是 CSV 格式

JSON:

請求 url 結尾為 *datapoints*


CSV:

請求 url 結尾為 *datapoints.csv*



## 回覆

### 回覆代碼
200

### 回覆 Header
JSON 格式:
```
Content-Type:`application/json`
```
CSV 格式:
```
Content-Type: `text/csv`
```

### 回覆內容

***資料格式: JSON***

若使用 JSON 回覆格式，則會包含以下欄位：

| 欄位名稱 | 格式 | 描述|
| --- | --- | --- | --- |
| dataChannels | Object Array | 含有資料點的資料通道 |

**資料詳情**

**資料通道**

| 欄位名稱 | 格式 | 描述|
| --- | --- | --- | --- |
| dataChnId | Number | 資料通道 ID |
| isOverflow | Bool | 要求的資料點是否超過數目限制|
| dataPoints | Object Array | 資料點 |


**資料點**

| 欄位名稱 | 格式 | 描述|
| --- | --- | --- | --- |
| createdAt | Number | 以 Unix timestamp 格式紀錄的資料點建立時間|
| values | Object | 資料點的值 |

請注意，我們在此使用的 unix timestamp miniseconds 時間值，若須轉換成可讀格式，您可以使用以下連結：
http://www.epochconverter.com/

**範例：**

請求 URL：
```
https://api.mediatek.com/mcs/v2/devices/a1234567890/datachannels/10001/datapoints?start=946684800&end=946784800

```

JSON 格式的回覆內容：

```
{
    "deviceId": "DXLQwmnN",
    "dataChannels": [
        {
            "dataChnId": "test01",
            "isOverflow": false,
            "dataPoints": [
                {
                    "recordedAt": 1432538716989,
                    "values": {
                        "value": "HI"
                    }
                }
            ]
        }
    ]
}
```

CSV 格式的回覆內容：

```
test_data_channel,1432538716989,100
```



## 錯誤回覆

當錯誤發生時，回覆代碼為非 200 之其他代碼。回覆內容為 JSON 格式並會包括以下資訊：


| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 錯誤代碼 |
| url | String | API 錯誤頁面 url|
| description | String | 錯誤描述 |



**範例：**

```
{
    "results": "you dont have permission!"
}
```

