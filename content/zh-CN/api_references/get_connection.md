# 取得连结


## 描述

使用**HTTPs GET** 来设置装置和MCS Command server之间的连线


## 请求 URL

设置装置和MCS Command server之间的连线:

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/connections

```

设定装置和Command server之间的TCP长连结，装置首先需要呼叫RESTful API `getConnection`来取得一组ip位置以及连接阜来建立TCP长连结。 MCS将会回覆ip地址和连接阜资讯给装置。

Command server 回覆格式:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```

当装置收到覆ip地址和连接阜后，装置会发出一个heartbeat给command server来验证。装置也会每120秒发送一次heartbeat给command server来确保连线。


Heartbeat 格式:

```
    deviceId, deviceKey, timestamp

```

当TCP长连结建立后，您将可以透过MCS平台对装置下指令。

指令格式:
```
{
    deviceId, deviceKey, timestamp, dataChnId, commandValue
}

```

## 动做
HTTPs GET


## 参数
### Header


Content-Type:`application/json` or `text/csvt`


deviceKey: `device_key_here`


### 回覆格式
回覆格式可以有JSON或是CSV两种

JSON:

请求url结尾为 *connections*


CSV:

请求url结尾为 *connections.csv*


## 回覆

### 回覆代码
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

### 回覆内容

***回覆格式: JSON***

JSON格式的回覆内容会包含以下几个栏位：

| 栏位名称 | 格式 |描述|
| --- | --- | --- | --- |
| ip | array | command server ip位置|
|port|Integer|command server 提供给装置连接的连接阜|


**范例：**

请求  URL
```
https://api.mediatek.com/mcs/v2/devices/a1234567890/connections
```

请求内容

```
{
   "ip": xxx.xxx.xxx.xxx,
   "port":443

}
```


## 错误回覆

当错误发生时，回覆代码为非200之其他代码。回覆内容为JSON格式并会包括以下资讯：

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
    "description": "You dont have permission"
  }
}
```
