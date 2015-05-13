# 取得連結


## 描述

使用 **HTTPs GET** 來設置裝置和MCS Command server之間的連線


## 請求 URL

設置裝置和MCS Command server之間的連線:

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/connections

```
設定裝置和Command server之間的TCP長連結，裝置首先需要呼叫RESTful API `getConnection`來取得一組ip位置以及連接阜來建立TCP長連結。MCS將會回覆ip地址和連接阜資訊給裝置。

Command server 回覆格式:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
當裝置收到覆ip地址和連接阜後，裝置會發出一個heartbeat給command server來驗證。裝置也會每120秒發送一次heartbeat給command server來確保連線。


Heartbeat 格式:

```
    deviceId, deviceKey, timestamp

```

當TCP長連杰建立後，您將可以透過MCS平台對裝置下指令。

指令格式:
```
{
    deviceId, deviceKey, timestamp, dataChnId, commandValue
}

```

## 動做
HTTPs GET


## 參數
### Header


Content-Type:`application/json` or `text/csvt`


deviceKey: `device_key_here`


### 回覆格式

回覆格式可以有JSON或是CSV兩種

JSON:

請求url結尾為 *connections*


CSV:

請求url結尾為 *connections.csv*


## 回覆

### 回覆代碼
200

### 回覆 Header

JSON格式:
```
Content-Type:`application/json`
```
CSV格式:
```
Content-Type: `text/csvt`
```

### 回覆內容

***回覆格式: JSON***

JSON格式的回覆內容會包含以下幾個欄位：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- | --- |
| ip | array | command server ip位置|
|port|Integer|command server 提供給裝置連接的連接阜|


**範例：**

請求 URL
```
https://api.mediatek.com/mcs/v2/devices/a1234567890/connections
```

請求內容

```
{
   "ip": xxx.xxx.xxx.xxx,
   "port":443

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
    "description": "You dont have permission"
  }
}
```
