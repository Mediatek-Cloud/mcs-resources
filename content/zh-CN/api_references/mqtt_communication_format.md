# MQTT 沟通格式

此章节将会说明所有 MQTT 沟通格式，此格式为当装置有订阅主题,或是欲传送资讯至 MQTT Broker 时，所会接收或是发送的格式。


## 事前准备

终端装置必须先连结至 MCS MQTT Broker 并且订阅或是发布至一个主题，之后才可和 MCS 做讯息交换。


## 设定连线

MQTT 伺服器： mqtt.mcs.mediatek.com

连接阜： 1883(未加密) 或 8883(加密)

请注意， 当您使用加密阜时，MCS 使用**伺服器端加密**方式。

## 订阅 & 发布

当您连结上 MCS MQTT 伺服器后，您可以订阅整个装置或是个别资料通道的讯息；或是发布讯息至特定资料通道。

当要**订阅**特定资料通道时，订阅主题的格式如下：

```
mcs/:deviceId/:deviceKey/:dataChnId
```

或是可订阅特定装置下全部资料通道：

```
mcs/:deviceId/:deviceKey/+
```

当要**发布**时, 发布主题的格式如下：

```
mcs/:deviceId/:deviceKey/:dataChnId
```
或是要发布装置下一个或多个数据信道:

```
mcs/:deviceId/:deviceKey
```


## MQTT 订阅和发布数据格式

一般发布数据的格式为:

```
timestamp,dataChnId,value
```

其中timestamp使用UNIX时间戳格式
如果省略如下所示的时间戳值，则MCS将在收到时自动为该数据点建立时间戳。

```
,dataChnId,value
```
当针对特定的dataChnId发布资料
```
mcs/:deviceId/:deviceKey/:dataChnId
```
您也可以省略dataChnId

```
,,value
```

当使用发布装置下一个或多个数据信道的格式时，您不可以省略dataChnId，但同时您可以在一次的发布里发布多个数据点:

```
timestamp,dataChnId1,value1
timestamp,dataChnId2,value2
.
.
.
```

以下是针对不同数据信道型态的范例:


### 开关

```
timestamp,dataChnId,{0 or 1}

```
0 代表关，1 代表开。

范例：

, switch01, 1

代表将 switch01 资料通道的状态改为开，并且由系统自动带入时间。

### 分类
```
timestamp,dataChnId,{Key Value}
```
Key value 的值将会对应至您所设定的 Key name。

### 整数
```
timestamp,dataChnId,{Integer}
```

### 浮点数
```
timestamp,dataChnId,{Float}
```

### 十六进位数
```
timestamp,dataChnId,{Hex value}
```
十六进位数的值为 A-F 以及 0-9。

### 字串
```
timestamp,dataChnId,{string}
```

### GPS
```
timestamp,dataChnId,{latitude},{longitude},{altitude}
```

纬度范围从 -90 至 90。 0 至 90 代表北纬，0 至 -90 代表南纬。

经度范围从 -180 至 180。 0 至 180 代表东经，0 至 -180 代表西经。

高度范围从 0 至 20000 公尺。

### GPIO
```
timestamp,dataChnId,{0 ot 1}
```
0 代表低，1 代表高。

### PWM
```
timestamp,dataChnId,{value},{period}

```

### 类比
```
timestamp,dataChnId,{value}

```

### 游戏控制器
```
timestamp,dataChnId,{up/down/right/left/A/B value| press(1) or release(0)}

```

### 图片
```
timestamp,dataChnId,{image file base64 encoding string value}

```

