# LinkIt 7697 教學範例

LinkIt 7697 HDK 可支援 **Arduino IDE** 或是 **LinkIt SDK for RTOS** 兩種開發環境。

在本章節中，您將會學到如何使用 **Arduino IDE** 在 LinkIt 7697 開發板上編寫能與 MCS 雲端服務互動的應用程式。

## MCS 函式庫簡介 

在 LinkIt 7697 HDK 的 **[開發板支援套裝軟體](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/setup-arduino-ide-for-linkit-7697)** (Arduino board support package) 當中包含了 MCS 函式庫，方便您開發與 MCS 雲端服務相關的專案。 MCS 雲端服務所提供的功能與所需要的設定都已經被定義在這個函式庫當中，其中包含有：

* 將裝置連上 MCS 雲端服務。
* 建立裝置上的資料通道，但目前尚不支援 Gameplad 類型的通道。
* 將裝置上產生的數據上傳到 MCS 雲端服務。
* 接收來自 MCS 雲端服務的指令或數據。

目前此函式庫是透過 TCP 與 HTTP 兩種通訊協定與 MCS 雲端服務溝通。更多的函式庫規格文件，請參考 [MCS Library API Reference](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/using-mcs-library/mcs-library-api-reference)。

## 設定開發環境

1. 設定 LinkIt 7697 的 Arduino IDE 開發環境。請參考 [MediaTek Labs 網站](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/setup-arduino-ide-for-linkit-7697) 上的步驟。

2. 將 LinkIt 7697 連結上您的電腦。請參考 [MediaTek Labs 網站](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/connecting-linkit-7697-to-computer) 上的步驟。

3. 如果您尚未申請 MCS 帳號，請點擊[註冊](https://mcs.mediatek.com/oauth/en/signup)。已經有帳號者可直接[登入](https://mcs.mediatek.com/oauth/en/login)。接著便可在 MCS 網站頁面上建立產品原型與測試裝置囉。

## 打造您的應用程式
觀看應用範例：

|[控制 LED 燈號](./7697_led_control.md)|
|---|
|[![](../images/Linkit_ONE/img_linkitone_26.png)](./7697_led_control.md)|


