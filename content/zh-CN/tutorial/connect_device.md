# 连接装置


要让您的装置和MCS平台相连，您必须坐以下动作：

呼叫RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections 来取得Socket Server IP 和连接阜的值。

Command server会回覆您以下资料:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
使用取得的ip位置和连接阜，来打开任意一个tcp connection，并且传送一个heartbeat讯息。

Heartbeat 形式如下:

```
    deviceId, deviceKey, timestamp

```
当TCP长连结建立后，您将可以开始使用MCS平台来对您的装置下指令。

指令的形式如下：
```
    deviceId, deviceKey, timestamp, dataChnId, commandValue

```

您可以在API参考资料集中，查看更多关于各种资料通道的指令形式。
