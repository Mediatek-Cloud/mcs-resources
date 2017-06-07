# LinkIt 7697 Tutorial

There are two software development environments available to LinkIt 7697 HDK, **Arduino IDE** and **LinkIt SDK for RTOS**.

In this guide, you’ll learn how to program your own applications on LinkIt 7697 development board to communicate with MCS service with **Arduino IDE**.

## MCS Library Introduction

On LinkIt 7697 HDK, you can use MCS library, which is included in the **[Arduino board support package](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/setup-arduino-ide-for-linkit-7697)** to implement MCS related projects. MCS library acts as a wrapper for the basic operations between LinkIt 7697 HDK and MCS service, including:

* connecting to MCS server.
* creating data channels, except Gamepad controller.
* uploading data points of a specified data channel onto the MCS server.
* receiving data points of a specified data channel from the MCS server.

However, only TCP and HTTP protocols are supported in this library. Please refer to [MCS Library API Reference](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/using-mcs-library/mcs-library-api-reference) for the detailed API usage.

## Setup Development Environment

1. Setup Arduino IDE for LinkIt 7697. Follow the steps on [MediaTek Labs website](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/setup-arduino-ide-for-linkit-7697).

2. Connect LinkIt 7697 to your computer. Follow the steps on [MediaTek Labs website](https://docs.labs.mediatek.com/resource/linkit7697-arduino/en/connecting-linkit-7697-to-computer).

3. Sign up a MCS account if you don't have one. Click [here](https://mcs.mediatek.com/oauth/en/signup) to sign up or [here](https://mcs.mediatek.com/oauth/en/login) to sign in. You will then be able to define prototypes and create devices on MCS web console.

## Build your own Applications
Choose the application you would like to start with:

|[Control LED](./7697_led_control.md)|
|---|
|[![](../images/Linkit_ONE/img_linkitone_26.png)](./7697_led_control.md)|


