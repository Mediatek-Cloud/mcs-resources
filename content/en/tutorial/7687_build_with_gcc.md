# Building your LinkIt 7687 applications with GCC

In this guide we will show you how to use GCC ARM Embedded to create your projects for LinkIt 7687 and enable the remote control ability. 

## Setting up the environment

Installing the LinkIt SDK build environment. Before we go further to build MCS related projects, please refer to MediaTek Labs > Get Started with LinkIt 7687 HDK > [GCC ARM Embedded command line tools](https://docs.labs.mediatek.com/resource/mt7687-mt7697/get-started-linkit-7687-hdk/gcc-arm-embedded-command-line-tools-free) to setup your development environment, including get the LinkIt RTOS SDK, connect to the serial port, etc.

> If you're using macOS on Apple Mac, you have to replace the GCC compiler in the origin LinkIt SDK.
	
> 1. Download [gcc for Mac](https://launchpad.net/gcc-arm-embedded/4.8/4.8-2014-q3-update/+download/gcc-arm-none-eabi-4_8-2014q3-20140805-mac.tar.bz2).
> 2. Unzip the gcc file you've downloaded and rename the folder to gcc-arm-none-eabi.
> 3. Replace {SDK_Root}/tools/gcc/gcc\-arm\-none\-eabi with this downloaded folder.


## Starting your journey in MCS

Please register a MCS account and [sign in](https://mcs.mediatek.com/oauth/login) first. 

We will guide you to setup your MCS prototype and test devices accordingly in each example. Now, choose the application you would like to start with:

| [Light Switch](../tutorial/7687_light_switch_gcc) |
| :---: | 
|[![](../images/7687/img_7687_switch.png)](../tutorial/7687_light_switch_gcc)| 