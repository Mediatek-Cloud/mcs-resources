# Command server 格式

此章節將會說明所有command server的格式，此格式為command server發送指令置裝置的格式。

**此處使用UNIX timestamp時間格式。

裝置會從command server接收到以下格式的指令，並且使用者可以自行寫一段解析程式來處理收到的指令。

以下為一段範例解析程式用來擷取一個PWM資料型態指令中的資料通道ID，資料值，以及頻率。

https://gist.github.com/MTK-mcs/e8ee0ad19d5f5755b232


## 事前準備

在裝置能接收MCS指令前，裝置須先和MCS平台做相連。


呼叫 RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections to 來取得一組ip位置以及連接阜來建立連結。

Command server 回覆格式:

```
{
    "ip": "ServerIp",
    "port": "serverPort"
}

```
來打開任意一個tcp connection，並且傳送一個heartbeat訊息。

Heartbeat 格式:

```
    deviceId, deviceKey, timestamp

```
當TCP長連結建立後，您將可以開始使用MCS平台來對您的裝置下指令。

指令的形式如下：
```
    deviceId, deviceKey, timestamp, dataChnId, commandValue

```


## 各種資料通道的command格式


### 開關

```
deviceId,deviceKey,timestamp,dataChannelId,{0 or 1}

```
0代表關，1代表開。

範例：

switch01,, 1

代表將switch01資料通道的狀態改為開，並且由系統自動帶入時間。

### 分類
```
deviceId,deviceKey,timestamp,dataChannelId,{Key Value}
```
Key value 的值將會對應至您所設定的Key name。

### 整數
```
deviceId,deviceKey,timestamp,dataChannelId,{Integer}
```

### 浮點數
```
deviceId,deviceKey,timestamp,dataChannelId,{Float}
```

### 十六進位數
```
deviceId,deviceKey,timestamp,dataChannelId,{Hex value}
```
十六進位數的值為A-F以及0-9。

### 字串
```
deviceId,deviceKey,timestamp,dataChannelId,{string}
```

### GPS
```
deviceId,deviceKey,timestamp,dataChannelId,{latitude},{longitude},{altitude}
```

緯度範圍從 -90 至 90。 0 至 90 代表北緯，0 至 -90 代表南緯。

經度範圍從 -180 至 180。 0 至 180 代表東經，0 至 -180 代表西經。

高度範圍從 0 至 20000公尺。

### GPIO
```
deviceId,deviceKey,timestamp,dataChannelId,{0 ot 1}
```
0代表低，1代表高。

### PWM
```
deviceId,deviceKey,timestamp,dataChannelId,{value},{period}

```
