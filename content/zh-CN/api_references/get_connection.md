# 取得连结


## 描述

使用**HTTPs GET** 来设置装置和 MCS Command server 之间的连线


## 请求 URL

设置装置和 MCS Command server 之间的连线:

```
https://api.mediatek.com/mcs/v2/devices/:deviceId/connections

```

设定装置和 Command server 之间的 TCP 长连结，装置首先需要呼叫 RESTful API `Get connection` 来取得一组 ip 位置以及连接阜来建立 TCP 长连结。 MCS 将会回覆 ip 地址和连接阜信息给装置。

Command server 回覆格式:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```

当装置收到覆 ip 地址和连接阜后，装置会发出一个 heartbeat 给 command server 来验证。装置也会每 120 秒发送一次 heartbeat 给 command server 来确保连线。


Heartbeat 格式:

```
    deviceId, deviceKey,timestamp

```
此处使用 UNIX timestamp 时间格式。若您不希望在心跳中传送实际的时间戳，您可以直接在时间戳栏位输入 0 为其值，系统将自动带入系统时间。

当 TCP 长连结建立后，您将可以透过 MCS 平台对装置下指令。

指令格式:
```
{
    deviceId,deviceKey,timestamp,dataChnId,commandValue
}

```

## 动做
HTTPs GET


## 参数
### Header


Content-Type:`application/json` or `text/csv`


deviceKey: `device_key_here`


### 回覆格式
回覆格式可以有 JSON 或是 CSV 两种

JSON:

请 求url 结尾为 *connections*


CSV:

请求 url 结尾为 *connections.csv*


## 回覆

### 回覆代码
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

### 回覆内容

***回覆格式: JSON***

JSON 格式的回覆内容会包含以下几个栏位：

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

当错误发生时，回覆代码为非 200 之其他代码。回覆内容为 JSON 格式并会包括以下信息：

| 栏位名称 | 格式 |描述|
| --- | --- | --- |
| code | Integer | 错误代码 |
| url | String | API 错误页面 url|
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
