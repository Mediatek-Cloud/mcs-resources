# Command server 格式

此章节将会说明所有command server 的格式，此格式为 command server 发送指令置装置的格式。

**此处使用 UNIX timestamp 时间格式。

装置会从 command server 接收到以下格式的指令，并且使用者可以自行写一段解析程式来处理收到的指令。

以下为一段范例解析程式用来撷取一个 PWM 资料型态指令中的资料通道 ID，资料值，以及频率。

https://gist.github.com/MTK-mcs/e8ee0ad19d5f5755b232


## 事前准备

在装置能接收 MCS 指令前，装置须先和 MCS 平台做相连。


呼叫 RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections to 来取得一组 ip 位置以及连接阜来建立连结。

Command server 回覆格式:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
来打开任意一个 tcp connection，并且传送一个 heartbeat 讯息。

Heartbeat 格式:

```
    deviceId, deviceKey, timestamp

```
当 TCP 长连结建立后，您将可以开始使用 MCS 平台来对您的装置下指令。

指令的形式如下：
```
    deviceId, deviceKey, timestamp, dataChnId, commandValue

```


##  各种资料通道的 command 格式


### 开关

```
deviceId,deviceKey,timestamp,dataChannelId,{0 or 1}

```
0 代表关，1 代表开。

范例：

switch01,, 1

代表将 switch01 资料通道的状态改为开，并且由系统自动带入时间。

### 分类
```
deviceId,deviceKey,timestamp,dataChannelId,{Key Value}
```

### 整数
```
deviceId,deviceKey,timestamp,dataChannelId,{Integer}
```

### 浮点数
```
deviceId,deviceKey,timestamp,dataChannelId,{Float}
```

### 十六进位数
```
deviceId,deviceKey,timestamp,dataChannelId,{Hex value}
```
十六进位数的值为 A-F 以及 0-9。

### 字串
```
deviceId,deviceKey,timestamp,dataChannelId,{string}
```

### GPS
```
deviceId,deviceKey,timestamp,dataChannelId,{latitude},{longitude},{altitude}
```

纬度范围从 -90 至 90。 0 至 90 代表北纬，0 至 -90 代表南纬。

經度範圍從 -180 至 180。 0 至 180 代表東經，0 至 -180 代表西經。

高度範圍從 0 至 20000公尺。

### GPIO
```
deviceId,deviceKey,timestamp,dataChannelId,{0 ot 1}
```
0 代表低，1 代表高。

### PWM
```
deviceId,deviceKey,timestamp,dataChannelId,{value},{period}

```

### 类比
```
deviceId，deviceKey，timestamp，dataChannelId，{value}

```

### 游戏控制器
```
deviceId，deviceKey，timestamp，dataChannelId，{上/下/左/右 值| A/B 键值}
```
