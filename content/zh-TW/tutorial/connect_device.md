# 連接裝置

要讓您的裝置和MCS平台相連，您必須坐以下動作：

呼叫RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections 來取得Socket Server IP 和連接阜的值。

Command server會回覆您以下資料:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
使用取得的ip位置和連接阜，來打開任意一個tcp connection，並且傳送一個heartbeat訊息。

Heartbeat 形式如下:

```
    deviceId, deviceKey, timestamp

```
當TCP長連結建立後，您將可以開始使用MCS平台來對您的裝置下指令。

指令的形式如下：

```
    deviceId, deviceKey, timestamp, dataChnId, commandValue

```
您可以在API參考資料集中，查看更多關於各種資料通道的指令形式。

