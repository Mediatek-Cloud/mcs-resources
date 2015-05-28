# LinkIt Connect 7681 實際操作

下面是一個簡單的指南來快速設置您的 LinkIt Connect 7681 開發板（MT 7681）連接到 MediaTek Cloud Sandbox。

## 情境

此教程的情境為，將您的 LinkIt Connect 7681 開發板與 MCS 平台相連，並可從 MCS 網頁端或手機端接收或傳送指令。


## 設置準備

為了要完成此設置，您必須先：

1. 您的開發板必須有 micro-USB 電源連接。
2. 您的開發板必須有 Wifi 連結。
3. MCS 手機應用程式。此程是目前只支援安卓 (Android) 系統。請使用此 QR code 下載最新的手機安裝檔：

![](../images/mobileapp_android.png)

此外，您不需要額外的電子組件，就可以連接到開發板了。

## MT7681　控制器清單以及相對的 MCS 資料通道 ID

MT7681 晶片組提供了五組 GPIO 針腳，您亦可使用 PWM 資料型態和一組 UART 阜。以下是 MT7681 的針腳和對應的資料通道 ID。

|  | GPIO | PWM | UART |
| -- | -- | -- | -- |
| 00 | GPIO_00 | PWM_00 | UART |
| 01 | GPIO_01 | PWM_01 |
| 02 | GPIO_02 | PWM_02 |
| 03 | GPIO_03 | PWM_03 |
| 04 | GPIO_04 | PWM_04 |


## 逐步指引

### 步驟一　建立有 GPIO，PWM，以及 UART 資料通道的產品原型。

a. 點擊畫面上方的 **開發**

b. 在產品原型清單頁面中，點擊**創建**按鈕來新增一個新的產品原型。


![](../images/screenshot/screen_shot-01.jpg)

c. 輸入產品原型名稱，版本，並選擇產業別。硬體平台請選擇 **MT7681**，之後點擊儲存按鈕。您的產品原型已建立。


![](../images/screenshot/screen_shot-22.jpg)

d. 現在您已準備好替您的產品原型新增一組控制器類型的 GPIO 資料通道了。點擊您剛新建好的產品原型下方的**詳情**按鈕。

![](../images/screenshot/screen_shot-23.jpg)

e. 點擊**資料通道分頁**，並點擊**新增**按鈕。

![](../images/screenshot/screen_shot-03.jpg)


f. 請點擊**控制器**下方的**新增**按鈕來新增一個控制器類型的資料通道。


![](../images/screenshot/screen_shot-13.jpg)

g. MT7681 類型的產品原型，資料通道 ID 的格式如以下定義 - GPIO_nn, nn代表從00開始的腳號。替第一個腳號建立資料通道，您可使用"GPIO_00"。輸入資料通道名稱(GPIO_00)，輸入描述，並且選擇 **GPIO** 資料型態。點擊**儲存**來新增您的資料通道。

![](../images/Mobile/connect_9.jpg)


h. 增加更多的 GPIO 腳號控制器，重複步驟 e，f，和g。並注意需使用正確的資料通道 ID (GPIO_01 至 GPIO_04)。

i. 現在您已經準備好控制器類型的 PWM 資料通道。重複步驟 e 和 g 來打開新增資料通道視窗。輸入"PWM_00" 為您的資料通道 ID，並選擇 PWM 為您的資料通道類型。點擊**儲存**來新增您的資料通道。


![](../images/Mobile/connect_10.jpg)

j. 增加更多的 PWM 腳號控制器，重複步驟 i。並注意需使用正確的資料通道 ID (PMW_01 至 PMW_04)。

k. 另一個您需要替 MT7681 產品原型所新增的資料通道為 UART。要新增 UART 資料通道，重複步驟 e 和 f，新增一個控制器類型的資料通道。輸入資料通道名稱為 "UART" 並根據您的需求選擇**字串**或是**十六進位數**資料型態。點擊**儲存**來新增您的資料通道。


![](../images/screenshot/screen_shot-26.jpg)

您現在已建立好所有 LinkIt Connect 7681 產品原型教程所支持的資料通道。請繼續至步驟二。


### 步驟二　將您的開發板連上無線網路

a. 使用手機打開 MCS 手機應用程式，使用您的帳號密碼登入。

b. 登入後，點擊畫面又下方的新增按鈕。

![](../images/Mobile/connect_1.jpg)

c. 點擊畫面下方的 **Smart Connection** 按鈕。此功能是使用 MediaTek Smart Connection，如欲知更多細節，請參考 MediaTek LinkIt Connect 7681 開發者手冊。


![](../images/Mobile/connect_2.png)

d. 輸入無線網路的 SSID 和密碼，之後點擊**開始**。正常情況下，SSID 會自動帶入您手機所連線至的無線網路。

![](../images/Mobile/connect_3.png)

e. 等待幾秒後，如果 Smart Connection 成功，您將會看到您的裝置在列表上。

點擊**取消**來退出 Smart Connection 視窗。

現在，您可以透過 MCS 手機應用程式(步驟 3A)，或是 MCS 網頁版(步驟3B)來註冊您的測試裝置。


###步驟3A　使用MCS手機應用程式來註冊 LinkIt Connect 7681 測試裝置

a. 打開 MCS 手機應用程式並登入。登入後，點擊畫面又下方的新增按鈕。

![](../images/Mobile/connect_1.jpg)

b. 如果您的裝置已透過無線網路 Smart Connection 成功，您可以在清單中看見您的實體裝置。點擊裝置右方的加號，來新增測試裝置。


![](../images/Mobile/connect_4.png)

c. 之後您將會看到產品原型列表。選擇您要新增測試裝置的產品原型，然後點擊**下一步**按鈕。

![](../images/Mobile/connect_5.png)

d. 輸入測試裝置名稱和描述，然後點擊**儲存**按鈕。

![](../images/Mobile/connect_6.png)

當測試裝置註冊後，您即可在測試裝置清單中看見您剛才所建立的測試裝置以及測試裝置內的資料通道。

![](../images/Mobile/connect_7.png)

### 步驟 3B　使用MCS網頁版建立測試裝置

a. 在MCS網頁版中，點擊畫面上方的**開發**，之後點擊您在步驟一所建立的產品原型的詳情按鈕來新增一個測試裝置。

![](../images/screenshot/screen_shot-02.jpg)

b. 點擊畫面右上方的**創建測試裝置**按鈕。

![](../images/screenshot/screen_shot-27.jpg)

c. 輸入**測試裝置名稱**和**描述**，之後點擊**確定**按鈕。您將會看到一個跳出視窗顯示您已成功建立測試裝置。點擊**詳細資訊**來查看測試裝置詳情。


![](../images/screenshot/screen_shot-18.jpg)

d. 在測試裝置頁面中，您可以查看此測試裝置的 deviceId 和 deviceKey。

![](../images/screenshot/screen_shot-28.jpg)

e. 現在您可以手動將此測試裝置的 deviceId 寫入您的實體裝置。打開任意終端機，並輸入已下指令：

```
AT#FLASH -s0x180e9 -c[deviceId]
```
接下來，將 deviceKey 寫入您的實體裝置
```
AT#FLASH -s0x180f1 -c[deviceKey]
```

之後，輸入以下指令來註冊此裝置：
```
AT#FLASH -s0x18101 –v1
AT#FLASH -s0x18102 –v0
```
您的實體裝置已和 MCS 平台相連了。


### 步驟 4A　透過手機應用程式來控制您的裝置

a. 打開 MCS 手機應用程式並登入。點擊您欲操作的測試裝置。


![](../images/Mobile/connect_7.png)

b. 您將會看到您在步驟一所建立的資料通道。將 GPIO 控制器狀態從低更改至高：您將會看到開發板上的 LED 燈打開。


![](../images/Mobile/connect_8.png)

### 步驟 4B　透過 MCS 網頁版來控制裝置

a. 點擊網頁版上方的**我的裝置**，在您新增並註冊的裝置下方的，點擊**詳情**。


![](../images/screenshot/screen_shot-29.jpg)

b. 您可以看到裝置內的資料通道，並可透過 MCS 傳送指令。您可以透過拖拉控制器來更改裝置狀態。將 GPIO 控制器狀態從低更改至高：您將會看到開發板上的 LED 燈打開。

![](../images/screenshot/screen_shot-30.jpg)


