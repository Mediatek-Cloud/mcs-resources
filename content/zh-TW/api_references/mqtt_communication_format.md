# MQTT 溝通格式

此章節將會說明所有 MQTT 溝通格式，此格式為當裝置有訂閱主題,或是欲傳送資訊至 MQTT Broker 時，所會接收或是發送的格式。


## 事前準備

終端裝置必須先連結至 MCS MQTT Broker 並且訂閱或是發佈至一個主題，之後才可和 MCS 做訊息交換。


## 設定連線

MQTT 伺服器： mqtt.mcs.mediatek.com

連接阜： 1883(未加密) 或 8883(加密)

請注意， 當您使用加密阜時，MCS 使用**伺服器端加密**方式。

## 訂閱 & 發佈

當您連結上 MCS MQTT 伺服器後，您可以訂閱整個裝置或是個別資料通道的訊息；或是發佈訊息至特定資料通道。

當要**訂閱**特定資料通道時，訂閱主題的格式如下：

```
mcs/:deviceId/:deviceKey/:dataChnId
```

或是可訂閱特定裝置下全部資料通道：

```
mcs/:deviceId/:deviceKey/+
```

當要**發佈**時, 發佈主題的格式如下：

```
mcs/:deviceId/:deviceKey/:dataChnId
```

或是要發佈裝置下一個或多個資料通道:

```
mcs/:deviceId/:deviceKey
```


## MQTT 訂閱和發佈資料格式

一般發佈資料的格式為:

```
timestamp,dataChnId,value
```

其中timestamp使用UNIX時間戳格式
如果省略如下所示的時間戳值，則MCS將在收到時自動為該數據點建立時間戳。

```
,dataChnId,value
```
當針對特定的dataChnId發佈資料
```
mcs/:deviceId/:deviceKey/:dataChnId
```
您也可以省略dataChnId

```
,,value
```

當使用發佈裝置下一個或多個資料通道的格式時，您不可以省略dataChnId，但同時您可以在一次的發佈裡發佈多個資料點:

```
timestamp,dataChnId1,value1
timestamp,dataChnId2,value2
.
.
.
```

以下是針對不同資料通道型態的範例:


### 開關

```
timestamp,dataChnId,{0 or 1}

```
0 代表關，1 代表開。

範例：

,switch01, 1

代表將 switch01 資料通道的狀態改為開，並且由系統自動帶入時間。

### 分類
```
timestamp,dataChnId,{Key Value}
```
Key value 的值將會對應至您所設定的 Key name。

### 整數
```
timestamp,dataChnId,{Integer}
```

### 浮點數
```
timestamp,dataChnId,{Float}
```

### 十六進位數
```
timestamp,dataChnId,{Hex value}
```
十六進位數的值為 A-F 以及 0-9。

### 字串
```
timestamp,dataChnId,{string}
```

### GPS
```
timestamp,dataChnId,{latitude},{longitude},{altitude}
```

緯度範圍從 -90 至 90。 0 至 90 代表北緯，0 至 -90 代表南緯。

經度範圍從 -180 至 180。 0 至 180 代表東經，0 至 -180 代表西經。

高度範圍從 0 至 20000 公尺。

### GPIO
```
timestamp,dataChnId,{0 ot 1}
```
0 代表低，1 代表高。

### PWM
```
timestamp,dataChnId,{value},{period}

```

### 類比
```
timestamp,dataChnId,{value}

```

### 遊戲控制器
```
timestamp,dataChnId,{up/down/right/left/A/B value| press(1) or release(0)}

```

### 圖片
```
timestamp,dataChnId,{image file base64 encoding string value}

```

