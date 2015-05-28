# 注册装置

## 描述

使用 **HTTPs POST**来注册装置

## 请求 URL

```
https://api.mediatek.com/mcs/v2/devices

```

## 动作
HTTPs POST

## 参数

### Header

Authorization: Bearer '{token}'

### 请求内容
JSON格式的请求内容会包含以下几个栏位：

| 栏位名称 | 格式 | 是否必填 |描述|
| --- | --- | --- | --- |
| prodId | String | Yes | 产品原型 ID |
| name | String | Yes | 装置名称 |
| isTest | Bool | Yes | 是否为测试装置 |
| description | String | No | 装置描述 |
| serial | String | No | 开发者可定义是否使用序号。若 isTest 为真，则不需要。 |
| deviceImageURL | String | No | 装置图片url |




## 回覆

### 回覆代码
200

### 回覆 Header

Content-Type:`application/json`
### 回覆内容

***回覆格式: JSON***

JSON 格式的回覆内容会包含以下几个栏位：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| deviceId | String | Device ID |
| deviceKey | String | Device Key |
| chipName | String | 晶片名称 |

**范例 **

请求 URL
```
https://api.mediatek.com/mcs/v2/devices
```

请求内容

```
{

         "prodId":"b1234567890",
         "name":"My 2nd device",
         "isTest":false,
         "serial":"mtk-01234",
         "deviceImageURL":"/device/mydevice.jpg"

}
```

回覆内容

```
{

         "deviceId":"d1234567890",
         "deviceKey":"0987654321d",
         "chipName":"MT7681"

}
```

回覆内容

## 错误回覆
当错误发生时，回覆代码为非 200 之其他代码。回覆内容为 JSON 格式并会包括以下资讯：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 错误代码 |
| url | String | API错误页面url|
| description | String | 错误描述 |

**范例:**

```
{
  "results": {
    "code": 1002,
    "url": "http://mcs.mediatek.com/api_errorcode?code=1002",
    "description": "You do not have access right to this API"
  }
}
```
