# 連接裝置

要讓您的裝置和 MCS 平台相連，您必須做以下動作：

呼叫 RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections 來取得 Socket Server IP 和連接阜的值。

Command server 會回覆您以下資料:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
使用取得的 ip 位置和連接阜，來打開任意一個 tcp connection，並且傳送一個 heartbeat 訊息。

Heartbeat 形式如下:

```
    deviceId, deviceKey, timestamp

```
當 TCP 長連結建立後，您將可以開始使用 MCS 平台來對您的裝置下指令。

指令的形式如下：

```
    deviceId, deviceKey, timestamp, dataChnId, commandValue

```
您可以在 API 參考資料集中，查看更多關於各種資料通道的指令形式。

