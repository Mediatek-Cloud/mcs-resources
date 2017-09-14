# 使用 GCC 建置 LinkIt 7687 应用程序

在这份入门指南中，您将使用 GCC ARM Embedded 命令列工具来建置 LinkIt 7687 的范例专案并且实现透过 MCS 远程控制您的装置。 

## 设定开发环境

在开发 MCS 相关的应用程序之前，您必须先安装并完成设定 LinkIt SDK 开发环境。请参考 MediaTek Labs > LinkIt 7687 HDK 入门指南 > [使用 GCC ARM Embedded](https://docs.labs.mediatek.com/resource/mt7687-mt7697/get-started-linkit-7687-hdk/gcc-arm-embedded-command-line-tools-free) 教学文件来建置您的开发环境。

> 如果您是使用 macOS on Apple Mac，请先按照下列步骤将 LinkIt SDK 中的 GCC 编译器置换成 Mac 的版本。
	
> 1. 下载 [gcc for Mac](https://launchpad.net/gcc-arm-embedded/4.8/4.8-2014-q3-update/+download/gcc-arm-none-eabi-4_8-2014q3-20140805-mac.tar.bz2)。
> 2. 将下载后的档案解压缩，并且更名为 gcc-arm-none-eabi。
> 3. 将步骤 2 中的资料夹覆盖掉原本 LinkIt SDK 中的 {SDK_Root}/tools/gcc/gcc\-arm\-none\-eabi。

## 开始 MCS 开发之旅

请先注册一个 MCS 帐号并完成[登录](https://mcs.mediatek.com/oauth/login)。

我们将会引导您在 MCS 页面上建立专案中需要的产品原型与测试装置。请选择范例：

| [LED 灯开关](../tutorial/7687_light_switch_gcc) |
| :---: | 
|[![](../images/7687/img_7687_switch.png)](../tutorial/7687_light_switch_gcc)| 