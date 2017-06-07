# LinkIt 7697 教学范例

LinkIt 7697 HDK 可支援 **Arduino IDE** 或是 **LinkIt SDK for RTOS** 两种开发环境。

在本章节中，您将会学到如何使用 **Arduino IDE** 在 LinkIt 7697 开发板上编写能与 MCS 云端服务互动的应用程序。

## MCS 函式库简介

在 LinkIt 7697 HDK 的 **[开发板支援套装软件](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/setup-arduino-ide-for-linkit-7697)** (Arduino board support package) 当中包含了 MCS 函式库，方便您开发与 MCS 云端服务相关的项目。 MCS 云端服务所提供的功能与所需要的设定都已经被定义在这个函式库当中，其中包含有：

* 将装置连上 MCS 云端服务。
* 建立装置上的资料通道，但目前尚不支援 Gameplad 类型的通道。
* 将装置上产生的数据上传到 MCS 云端服务。
* 接收来自 MCS 云端服务的指令或数据。

目前此函式库是透过 TCP 与 HTTP 两种通讯协定与 MCS 云端服务沟通。更多的函式库规格文件，请参考 [MCS Library API Reference](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/using-mcs-library/mcs-library-api-reference)。

## 设定开发环境

1. 设定 LinkIt 7697 的 Arduino IDE 开发环境。 请参考 [MediaTek Labs 网站](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/setup-arduino-ide-for-linkit-7697) 上的步骤。

2. 将 LinkIt 7697 连结上您的电脑。 请参考 [MediaTek Labs 网站](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/connecting-linkit-7697-to-computer) 上的步骤。

3. 如果您尚未申请 MCS 帐号，请点击[注册](https://mcs.mediatek.com/oauth/en/signup)。已经有帐号者可直接[登录](https://mcs.mediatek.com/oauth/en/login)。接着便可在 MCS 网站上建立产品原型与测试装置啰。

## 打造您的应用程式

观看应用范例：

|[控制 LED 灯号](./7697_led_control.md)|
|---|
|[![](../images/Linkit_ONE/img_linkitone_26.png)](./7697_led_control.md)|


