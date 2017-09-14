# 使用 GCC 建置 LinkIt 7687 應用程式

在這份入門指南中，您將使用 GCC ARM Embedded 命令列工具來建置 LinkIt 7687 的範例專案並且實現透過 MCS 遠端控制您的裝置。 

## 設定開發環境

在開發 MCS 相關的應用程式之前，您必須先安裝並完成設定 LinkIt SDK 開發環境。請參考 MediaTek Labs > LinkIt 7687 HDK 入門指南 > [使用 GCC ARM Embedded](https://docs.labs.mediatek.com/resource/mt7687-mt7697/get-started-linkit-7687-hdk/gcc-arm-embedded-command-line-tools-free) 教學文件來建置您的開發環境。

> 如果您是使用 macOS on Apple Mac，請先按照下列步驟將 LinkIt SDK 中的 GCC 編譯器置換成 Mac 的版本。
	
> 1. 下載 [gcc for Mac](https://launchpad.net/gcc-arm-embedded/4.8/4.8-2014-q3-update/+download/gcc-arm-none-eabi-4_8-2014q3-20140805-mac.tar.bz2)。
> 2. 將下載後的檔案解壓縮，並且更名為 gcc-arm-none-eabi。
> 3. 將步驟 2 中的資料夾覆蓋掉原本 LinkIt SDK 中的 {SDK_Root}/tools/gcc/gcc\-arm\-none\-eabi。

## 開始 MCS 開發之旅

請先註冊一個 MCS 帳號並完成[登入](https://mcs.mediatek.com/oauth/login)。

我們將會引導您在 MCS 頁面上建立專案中需要的產品原型與測試裝置。請選擇範例：

| [LED 燈開關](../tutorial/7687_light_switch_gcc) |
| :---: | 
|[![](../images/7687/img_7687_switch.png)](../tutorial/7687_light_switch_gcc)| 