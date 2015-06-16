# 读取装置信息

## 描述

使用 **HTTPs GET** 来读取装置信息


## 请求 URL

```
https://api.mediatek.com/mcs/v2/devices/:deviceId

```

## 动作
HTTPs GET

## 参数

### Header

Authorization: `Bearer '{token}'`

Content-Type:`application/json`


## 回覆

### 回覆代码
200

### 回覆 Header

Content-Type:`application/json`
### 回覆内容

***回覆格式: JSON***

JSON格式的回覆会包含以下几个栏位：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| deviceId | String | Device ID |
| deviceKey | String | Device Key |
| name | String | 装置名称 |
| description | String | 装置描述 |
| product | Object | 产品原型 |
| dataChannels | Object Array | 资料通道 |
| fw | Object | 韧体信息 |
| trustIpRange | String Array | 可连至MCS的信赖网域范围 |
| lastIp | String | 最后一次收到装置资料点的网域位址 |
| deviceImageURL | String | 装置图片 URL |
| isHeartbeating | Bool | 装置是否在线 |
| isVerified | Bool | 装置是否已被验证注册 |
| isActive | Bool | 装置是否已注册 |
| isTest | Bool | 是否为测试装置 |
| activatedAt | Number | 装置注册时间 |
| deactivatedAt | Number | 装置注销时间(若装置已注册且未被注销，则此值的默认值为null) |
| tags | Object Array | 装置标签 |
| privilege | String | 装置使用者权限 |

**资料详情**

**产品原型**

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| prodId | String | 产品原型 ID |
| prodVersion | String | 产品原型版本 |
| name | String | 产品原型名称 |
| description | String | 产品原型描述 |
| displayConfigs | Object Array | 一个JSON格式的物件，定义资料通道将如何呈现 |
| chip | String | 产品原型所使用的晶片类型 |

**资料通道**

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| dataChnId | Number | 资料通道 ID |
| isAvailable | Bool | 资料是否可用 |
| name | String | 资料通道名称|
| channelType | Object | 资料通道类型 |
| isHidden | Bool | 资料通道是否对使用者隐藏 |
| isControllable | Bool | 此资料通道是否为控制类型 |
| description | String | 资料通道描述 |
| unitType | Object | 资料通道单位值 |
| format | String | 资料通道格式 |


**韧体**

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| fwId | String | 韧体 ID |
| name | String | 韧体名称 |
| description | String | 韧体描述 |
| version | Number | 韧体版本 |

**显示设定**

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| displayType | Number | 如何显示 |
| displayOrder | Number | 不同元件的显示顺序 |
| dataChnIds | Number Array | 被设定为显示的资料通道ID |

**标签**

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| tagId | Number | 标签 ID |
| name | String | 标签名称 |



**范例： **

请求 URL
```
https://api.mediatek.com/mcs/v2/devices/d1234567890

https://api.mediatek.com/mcs/v2/devices/d1234567890,d1234567891
```


回覆内容

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

## ## 错误回覆

当错误发生时，回覆代码为非 200 之其他代码。回覆内容为 JSON 格式并会包括以下信息：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 错误代码 |
| url | String | API错误页面url|
| description | String | 错误描述 |


**范例**

```
{
  "results": {
    "code": 1002,
    "url": "http://mcs.mediatek.com/api_errorcode?code=1002",
    "description": "You do not have access right to this API"
  }
}
```
