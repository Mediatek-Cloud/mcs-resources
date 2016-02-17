# 连接装置


要让您的装置和 MCS 平台相连，您必须做以下动作：

呼叫 RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections 来取得 Socket Server IP 和连接阜的值。

Command server 会回覆您以下资料:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
使用取得的 ip 位置和连接阜，来打开任意一个 tcp connection，并且传送一个 heartbeat 讯息。

Heartbeat 形式如下:

```
    deviceId,deviceKey,timestamp

```
当 TCP 长连结建立后，您将可以开始使用 MCS 平台来对您的装置下指令。

指令的形式如下：
```
    deviceId,deviceKey,timestamp,dataChnId,commandValue

```

您可以在 API 参考资料集中，查看更多关于各种资料通道的指令形式。
