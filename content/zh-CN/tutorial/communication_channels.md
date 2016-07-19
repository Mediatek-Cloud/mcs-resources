# TCP 和 MQTT 连结

您可以选择使用 **Command Server** 来建立 TCP 连线，或是 **MQTT** 来将装置与 MCS 平台做沟通。装置与 MCS 平台相连之后，您可以透过电脑或是手机将指令发送给装置，或是接收装置上传的资料。

**Command Server** 是一个**单向的 TCP 通讯**，只支援从 MCS 传送指令或是讯息至装置端；**MQTT** 则是一个**双向的通讯模式**，您可以同时传送指令至装置或是接收装置上传的资料。

MCS 支援此两种通讯方式，并且我们建议您在一个装置上，只使用其中一种方式。


## Command Server
Command Server 是一个**单向的 TCP 通讯**，只支援从 MCS 传送指令或是讯息至装置端。

### 设定连线
在装置能接收 MCS 指令前，装置须先和 MCS 平台做相连。呼叫 RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections to 来取得一组 ip 位置以及连接阜来建立连结。之后，透过传送 heartbeat 来维持连线。


### 通讯格式
透过 Command Server 传送指令，您可以参考 [Command Server 格式](https://mcs.mediatek.com/resources/latest/api_references/#command-server-format) 来传送正确的格式给不同的资料通道。

 ### 透过 Command Server 做 FOTA

当您的装置已经透过 Command Server 与 MCS 连结， 并且您希望做韧体更新。当您按下推播按钮后，MCS Command Server 会将资讯以以下格式传递给装置：

**deviceId,deviceKey,timestamp,FOTA,version,MD5,URL**

* deviceId: 装置的 deviceId
* deviceKey: 装置的 deviceKey
* timestamp: 按下推播按钮的时间点
* FOTA: 字串
* version: 被传递的韧体版本
* MD5: 被传递的韧体 MD5
* URL: 被传递的韧体的下载网址

更多关于 FOTA 的资讯，请查看[此连结](../tutorial/managing_firmware)。

## MQTT
MQTT 是一种**双向的**是一个轻量的订阅和发布通讯协定。您可以在[此连结](http://mqtt.org/)中查看更多关于 MQTT 通讯的资讯。 MCS 采用标准的 MQTT 通讯模式，并且支援多种 MQTT 特色功能，包括离线讯息与保留讯息。

### 设定连线

MQTT 伺服器： mqtt.mcs.mediatek.com

连接阜： 1883(未加密) 或 8883(加密)

请注意， 当您使用加密阜时，MCS 使用**伺服器端加密**方式。

### 订阅 & 发布

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

### 通讯格式

以下格式为您**订阅**主题时会收到的讯息内容，或是**发布** 时亦是使用此相同格式：
```
timestamp,dataChnId,value
```

若要查看更多关于 MQTT 资料格式，您可以参考[此连结](../api_references/mqtt_communication_format)。

### Quality of Service (QoS)

QoS 或是 Quality of Service 为 MQTT 重要特色之一. 目前 MCS 只支援 QoS0 和 QoS1。

* QoS 0: 只送一次。此种送后不理的方式为最基础的传递模式，且不保证讯息的成功传达与否。
* QoS 1: 传送至少一次。此种传递模式确保讯息一定会被传达，但不限于只有传递一次。

### 保留讯息 & 离线讯息

MCS MQTT Broker 以 MQTT 标准模式提供保留讯息与离线讯息的服务。

* 保留讯息：此讯息会在每次有端点装置订阅特定主题时传送。例如：欢迎讯息。
* 离线讯息：此讯息当端点装置离线时，会暂时保留在伺服器端，当端点装置上线时传送。

### 保持连线（Keep Alive）

保持连线为端点装置承诺，在一定的时间区间内，定期发送讯息至伺服器端以保持连线。同时伺服器端也会回覆讯息给端点装置，让彼此判断对方是否在线。 MCS MQTT Broker 采用标准化的 MQTT 保持连线规则。


### 透过 MQTT 做 FOTA

请注意，若您要使用 MQTT 通道来做 FOTA，您需要订阅至 wild card 层级的主题。

格式如下：

```
mcs/:deviceId/:deviceKey/+
```

当您的装置已经透过 MQTT 与 MCS 连结， 并且您希望做韧体更新。当您按下推播按钮后，MCS MQTT Broker 会将资讯以以下格式传递给装置：

**timestamp,FOTA,version,MD5,URL**

* timestamp: 按下推播按钮的时间点
* FOTA: 字串
* version: 被传递的韧体版本
* MD5: 被传递的韧体 MD5
* URL: 被传递的韧体的下载网址

更多关于 FOTA 的资讯，请查看[此连结](../tutorial/managing_firmware)。

