# 讀取裝置資訊

## 描述

使用 **HTTPs GET** 來讀取裝置資訊

## 請求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId

```

## 動作
HTTPs GET

## 參數

### Header

Authorization: `Bearer '{token}'`

Content-Type:`application/json`


## 回覆

### 回覆代碼
200

### 回覆 Header

Content-Type:`application/json`

### 回覆內容

***回覆格式: JSON***

JSON格式的回覆會包含以下幾個欄位：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| deviceId | String | Device ID |
| deviceKey | String | Device Key |
| name | String | 裝置名稱 |
| description | String | 裝置描述 |
| product | Object | 產品原型 |
| dataChannels | Object Array | 資料通道 |
| fw | Object | 韌體資訊 |
| trustIpRange | String Array | 可連至MCS的信賴網域範圍 |
| lastIp | String | 最後一次收到裝置資料點的網域位址 |
| deviceImageURL | String | 裝置圖片 URL |
| isHeartbeating | Bool | 裝置是否在線 |
| isVerified | Bool | 裝置是否已被驗證註冊 |
| isActive | Bool | 裝置是否已註冊 |
| isTest | Bool | 是否為測試裝置 |
| activatedAt | Number | 裝置註冊時間 |
| deactivatedAt | Number | 裝置註銷時間 (若裝置已註冊且未被註銷，則此值的默認值為null) |
| tags | Object Array | 裝置標籤 |
| privilege | String | 裝置使用者權限 |

**資料詳情**

**產品原型**

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| prodId | String | 產品原型 ID |
| prodVersion | String | 產品原型版本 |
| name | String | 產品原型名稱 |
| description | String | 產品原型描述 |
| displayConfigs | Object Array | 一個JSON格式的物件，定義資料通道將如何呈現 |
| chip | String | 產品原型所使用的晶片類型 |


**資料通道**

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| dataChnId | Number | 資料通道 ID |
| isAvailable | Bool | Is the device normal |
| name | String | 資料通道名稱|
| channelType | Object | 資料通道類型 |
| isHidden | Bool | 資料通道是否對使用者隱藏 |
| isControllable | Bool | 此資料通道是否為控制類型 |
| description | String | 資料通道描述 |
| unitType | Object | 資料通道單位值 |
| format | String | 資料通道格式 |


**韌體**

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| fwId | String | 韌體 ID |
| name | String | 韌體名稱 |
| description | String | 韌體描述 |
| version | Number | 韌體版本 |

**顯示設定**

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| displayType | Number  | 如何顯示 |
| displayOrder | Number | 不同元件的顯示順序 |
| dataChnIds | Number Array | 被設定為顯示的資料通道ID |

**標籤**

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| tagId | Number | 標籤 ID |
| name | String | 標籤名稱 |



**範例： **

請求 URL
```
https://api.mediatek.com/mcs/v2/devices/d1234567890

https://api.mediatek.com/mcs/v2/devices/d1234567890,d1234567891
```


回覆內容

```
{
   "results":[
      {
         "deviceId":"d1234567890",
         "deviceKey":"1234567890d",
         "deviceName":"My 1st device",
         "deviceDescription":"Livingroom Smart Plug 1",
         "product":{
            "prodId":"a1234567890",
            "prodVersion":"1",
            "name":"MediaTek Smart Plug",
            "description":"Monitors Power Usag",
            "displayConfigs":[
               {
                  "displayType":2,
                  "displayOrder":1,
                  "dataChnIds":[
                     100004,
                     100006
                  ]
               },
               {
                  "displayType":1,
                  "displayOrder":2,
                  "dataChnIds":[
                     100009
                  ]
               }
            ],
            "chip":"MT7688"
         },
         "dataChannels":[
            {
               "dataChnId":10001,
               "isAvailable":true,
               "name":"My 1st Data Channel",
               "channelType":{
                  "dataChnTypeId":1,
                  "name":"float"
               },
               "isHidden":false,
               "isControllable":false,
               "description":"My first data channel on MCS 2.0",
               "unitType":{
                  "unitTypeId":2,
                  "name":"°C"
               },
               "format":{
                  "lowerbound":0.0,
                  "upperbound":100.0,
                  "interval":0.5,
                  "defaultValue":5.0
               },
               "comps":[
                  {
                     "compId":1,
                     "name":"MTK Camera"
                  },
                  {
                     "compId":2,
                     "name":"MTK Thermometer"
                  }
               ]
            },
            {
               "dataChnId":10002,
               "isAvailable":true,
               "name":"My 2nd Data Channel",
               "channelType":{
                  "dataChnTypeId":2,
                  "name":"swtich"
               },
               "isHidden":false,
               "isControllable":true,
               "description":"My second data channel on MCS 2.0",
               "format":{
                  "options":[
                     {
                        "name":"low",
                        "value":"1"
                     },
                     {
                        "name":"medium",
                        "value":"2"
                     },
                     {
                        "name":"high",
                        "value":"3"
                     }
                  ]
               }
            }
         ],
         "fw":{
            "fwId":"f1234567890",
            "name":"Appliance Firmware 2.0",
            "description":"",
            "version":0.5
         },
         "trustIpRange":[
            "*.*.*.*"
         ],
         "lastIp":"140.112.106.1",
         "deviceImageURL":"http://img.mediatek.com/img003.jpg",
         "isHeartbeating":true,
         "isVerified":true,
         "isActive":true,
         "isTest":false,
         "activatedAt":946684800,
         "deactivatedAt":0,
         "tags":[
            {
               "tagId":20,
               "name":"Smart Home"
            },
            {
               "tagId":59,
               "name":"Energy"
            }
         ],
         "deviceNtCritGrps":[
            {
               "ntfCritGrpId":1,
               "name":"Continuous Operating Time"
               "ntfMthTypeId":1,
               "ntfMthTypeName":"email"
            }
         ],
         "privilege":"Owner"
      },
      {
         "deviceId":"d1234567891",
         "deviceKey":"1987654321d",
         "name":"My 2nd device",
         "description":"Livningroom Smart Plug 2",
         "product":{
            "prodId":"a1234567890",
            "name":"MediaTek Smart Plug",
            "description":"Monitors Power Usage",
            "displayConfigs":[
               {
                  "displayType":2,
                  "displayOrder":1,
                  "dataChnIds":[
                     100004,
                     100006
                  ]
               },
               {
                  "displayType":1,
                  "displayOrder":2,
                  "dataChnIds":[
                     100009
                  ]
               }
            ],
            "chip":"MT7688"
         },
         "dataChannels":[
            {
               "dataChnId":10001,
               "isAvailable":true,
               "name":"My 1st Data Channel",
               "channelType":{
                  "dataChnTypeId":1,
                  "name":"float"
               },
               "isHidden":false,
               "isControllable":false,
               "description":"My first data channel on MCS 2.0",
               "unitType":{
                  "unitTypeId":2,
                  "name":"°C"
               },
               "format":{
                  "lowerbound":0.0,
                  "upperbound":100.0,
                  "interval":0.5,
                  "defaultValue":5.0
               },
               "comps":[
                  {
                     "compId":1,
                     "name":"MTK Camera"
                  },
                  {
                     "compId":2,
                     "name":"MTK Thermometer"
                  }
               ]
            },
            {
               "dataChnId":10002,
               "isAvailable":true,
               "name":"My 2nd Data Channel",
               "channelType":{
                  "dataChnTypeId":2,
                  "name":"swtich"
               },
               "isHidden":false,
               "isControllable":true,
               "description":"My second data channel on MCS 2.0",
               "format":{
                  "options":[
                     {
                        "name":"low",
                        "value":"1"
                     },
                     {
                        "name":"medium",
                        "value":"2"
                     },
                     {
                        "name":"high",
                        "value":"3"
                     }
                  ]
               }
            }
         ],
         "fw":{
            "fwId":"f1234567890",
            "name":"Appliance Firmware 2.0",
            "description":"",
            "version":0.3
         },
         "trustIpRange":[
            "*.*.*.*"
         ],
         "lastIp":"140.112.106.2",
         "deviceImageURL":"http://img.mediatek.com/img003.jpg",
         "isHeartbeating":false,
         "isVerified":true,
         "isActive":true,
         "isTest":false,
         "activatedAt":946684800,
         "deactivatedAt":0,
         "tags":[
            {
               "tagId":20,
               "name":"Smart Home"
            },
            {
               "tagId":59,
               "name":"Energy"
            }
         ],
         "privilege":"Viewer"
      }
   ]
}
```
## 錯誤回覆

當錯誤發生時，回覆代碼為非200之其他代碼。回覆內容為JSON格式並會包括以下資訊：

| 欄位名稱 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 錯誤代碼 |
| url | String | API錯誤頁面url|
| description | String | 錯誤描述 |


**範例**

```
{
  "results": {
    "code": 1002,
    "url": "http://mcs.mediatek.com/api_errorcode?code=1002",
    "description": "You do not have access right to this API"
  }
}
```
