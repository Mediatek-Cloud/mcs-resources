# TCP 和 MQTT 連結

您可以選擇使用 **Command Server** 來建立 TCP 連線，或是 **MQTT** 來將裝置與 MCS 平台做溝通。裝置與 MCS 平台相連之後，您可以透過電腦或是手機將指令發送給裝置，或是接收裝置上傳的資料。

**Command Server** 是一個**單向的 TCP 通訊**，只支援從 MCS 傳送指令或是訊息至裝置端；**MQTT** 則是一個**雙向的通訊模式**，您可以同時傳送指令至裝置或是接收裝置上傳的資料。

MCS 支援此兩種通訊方式，並且我們建議您在一個裝置上，只使用其中一種方式。


## Command Server
Command Server 是一個**單向的 TCP 通訊**，只支援從 MCS 傳送指令或是訊息至裝置端。

### 設定連線
在裝置能接收 MCS 指令前，裝置須先和 MCS 平台做相連。呼叫 RESTful API: GET https://api.mediatek.com/mcs/v2/devices/{deviceId}/connections to 來取得一組 ip 位置以及連接阜來建立連結。之後，透過傳送 heartbeat 來維持連線。


### 通訊格式
透過 Command Server 傳送指令，您可以參考 [Command Server 格式](https://mcs.mediatek.com/resources/latest/api_references/#command-server-format) 來傳送正確的格式給不同的資料通道。

 ### 透過 Command Server 做 FOTA

當您的裝置已經透過 Command Server 與 MCS 連結， 並且您希望做韌體更新。當您按下推播按鈕後，MCS Command Server 會將資訊以以下格式傳替給裝置：

**deviceId, deviceKey, timestamp, FOTA, version, MD5, URL**

* deviceId: 裝置的 deviceId
* deviceKey: 裝置的 deviceKey
* timestamp: 按下推播按鈕的時間點
* FOTA: 字串
* version: 被傳遞的韌體版本
* MD5: 被傳遞的韌體 MD5
* URL: 被傳遞的韌體的下載網址

更多關於 FOTA 的資訊，請查看[此連結](../tutorial/managing_firmware)。

## MQTT
MQTT 是一種**雙向的**是一個輕量的訂閱和發佈通訊協定。您可以在[此連結](http://mqtt.org/)中查看更多關於 MQTT 通訊的資訊。MCS 採用標準的 MQTT 通訊模式，並且支援多種 MQTT 特色功能，包括離線訊息與保留訊息。

### 設定連線

MQTT 伺服器： mqtt.mcs.mediatek.com

連接阜： 1883(未加密) 或 8883(加密)

請注意， 當您使用加密阜時，MCS 使用**伺服器端加密**方式。

### 訂閱 & 發佈

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

### 通訊格式

以下格式為您**訂閱**主題時會收到的訊息內容，或是**發佈** 時亦是使用此相同格式：
```
timestamp,dataChnId,value
```

若要查看更多關於 MQTT 資料格式，您可以參考[此連結](../api_references/mqtt_communication_format)。

### Quality of Service (QoS)

QoS 或是 Quality of Service 為 MQTT 重要特色之一. 目前 MCS 只支援 QoS0 和 QoS1。

* QoS 0: 只送一次。此種送後不理的方式為最基礎的傳遞模式，且不保證訊息的成功傳達與否。
* QoS 1: 傳送至少一次。此種傳遞模式確保訊息一定會被傳達，但不限於只有傳遞一次。

### 保留訊息 & 離線訊息

MCS MQTT Broker 以 MQTT 標準模式提供保留訊息與離線訊息的服務。

* 保留訊息：此訊息會在每次有端點裝置訂閱特定主題時傳送。例如：歡迎訊息。
* 離線訊息：此訊息當端點裝置離現時，會暫時保留在伺服器端，當端點裝置上線時傳送。

### 保持連線（Keep Alive）

保持連線為端點裝置承諾，在一定的時間區間內，定期發送訊息至伺服器端以保持連線。同時伺服器端也會回覆訊息給端點裝置，讓彼此判斷對方是否在線。MCS MQTT Broker 採用標準化的 MQTT 保持連線規則。


### 透過 MQTT 做 FOTA

請注意，若您要使用 MQTT 通道來做 FOTA，您需要訂閱至 wild card 層級的主題。

格式如下：

```
mcs/:deviceId/:deviceKey/+
```

當您的裝置已經透過 MQTT 與 MCS 連結， 並且您希望做韌體更新。當您按下推播按鈕後，MCS MQTT Broker 會將資訊以以下格式傳替給裝置：

** timestamp, FOTA, version, MD5, URL**

* timestamp: 按下推播按鈕的時間點
* FOTA: 字串
* version: 被傳遞的韌體版本
* MD5: 被傳遞的韌體 MD5
* URL: 被傳遞的韌體的下載網址

更多關於 FOTA 的資訊，請查看[此連結](../tutorial/managing_firmware)。



