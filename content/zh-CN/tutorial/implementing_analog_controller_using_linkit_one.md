# 使用 LinkIt ONE 开发板实现类比控制器


下面是一个简单的指南来快速设置您的 LinkIt ONE 开发板（Aster 2502 ）在 MediaTek Cloud Sandbox 上，做类比控制器之应用。

## 情境

此教程的情境为，替您的 LinkIt ONE 开发板建立一个测试装置，替您的板子上传一段 Arduino code，且使用 RESTful API 来控制您位于开发板上 ~D3 的 LED 灯光亮度。

## 设置准备

为了要完成此设置，您必须先：

1. 您的开发板必须有电源连接，电源可来自电池或是 micro-USB。
2. 您的开发板必须有 Wifi 连结。


此外，您不需要额外的电子组件，就可以连接到开发板了。

### 步骤一　替您的产品原型新增一个类比控制器资料通道

a. 登入平台后，点选上方开发之下的"产品原型"，并且点击新增按钮，来新增一个新的产品原型。您亦可直接汇入此[范例产品原型](http://cdn.mediatek.com/tutorial/LinkIt_ONE/LinkIt_ONE_analog_CN.json)，若您选择直接汇入产品原型，您可以跳过步骤一，直接从步骤二开始。


![](../images/Linkit_ONE/img_linkitone_02.png)

b. 请跟着画面指示填入产品原型的基本资讯：

![](../images/Linkit_ONE/img_linkitone_03.png)


c. 点击您刚建立的产品原型下方的"详情"按钮

![](../images/Linkit_ONE/img_linkitone_04.png)

d. 在产品原型详情页面中，点击"资料通道"分页，并且点击新增按钮来新增一个资料通道：

![](../images/Linkit_ONE/img_linkitone_05.png)

在此教程中，我们需要建立一个资料通道用来对开发版上的 LED 亮度发出调整控制讯号。

e. 点击在"控制器"下方的新增按钮，并输入以下资讯：

![](../images/Linkit_ONE/img_linkitone_08.png)

![](../images/Linkit_ONE/img_linkitone_19.png)

 请注意，您在此输入的资料通道 Id 是独特不可重复的，之后将会在呼叫 API 时使用到。


### 步骤二　建立测试装置

a. 点击画面右上方的"创建测试装置"

![](../images/Linkit_ONE/img_linkitone_11.png)

b. 输入测试装置名称和描述：

![](../images/Linkit_ONE/img_linkitone_20.png)

c. 测试装置建立后，点击"详细资讯"连结至测试装置详情页面:

![](../images/Linkit_ONE/img_linkitone_13.png)

![](../images/Linkit_ONE/img_linkitone_21.png)


请注意，deviceId 和 deviceKey 是独特不可重复的，之后将会在呼叫 API 时使用到。

### 步骤三　取得 DeviceId，DeviceKey，以及资料通道 ID

下方的摘要讯息为我们与测试装置沟通时所需要的必要栏位：

| 名称 | 值 | 备注 |
| -- | -- | -- |
| deviceId | Dsre1qRQ | 测试装置的独特识别码 |
| deviceKey | DFbtsNWg4AuLZ30v | 测试装置的 API Key |
| dataChannelId | analogTest | 此教程中所需控制器类型 LED 灯量度的资料通道代码 |

注意一：此教程中图片所显示的 deviceId 和 deviceKey 会和您实际操作时取得的不一样，请使用您所取得的值。

注意二：deviceId 的大小写是不一样的，请保持和上方表格资料值相同的大小写。

### 步骤四　替您的开发板编程

操作流程如下：

a. 呼叫 RESTful API：
GET api.mediatek.com/mcs/v2/devices/{deviceId}/connections.csv
来取得 Socket Server IP 和连接阜的值。

b. 和 Socket server 建立 TCP connection

c. 呼叫 RESTful API:
POST api.mediatek.com/mcs/v2/devices/{deviceId}/datapoints.csv
每五秒上传一次位于开发板 ~D3 位置的 LED 灯状态

请注意：当您使用 Analog 和 PWM 类型之资料通道，您需要使用在 LinkIt ONE 开发板上带有~ 开头之脚位。例如本教程中所使用之 ~D3 脚位。

d. 并且保持 TCP connection 连线随时可以接收来自 MCS 的指令

e. 每 90 秒更新一次 TCP connection 的heartbeat 连线

请点击此连结来下载 Arduino 范例程式[here](https://raw.githubusercontent.com/Mediatek-Cloud/MCS/master/source_code/AnalogLinkItOneSample)

请注意:
使用此范例程式需要 HttpClient，您可使用此连结下载
[here](https://github.com/amcewen/HttpClient/releases)

f. 替您的 LinkIt ONE 开发板外接以下电路板及元件：

![](../images/Linkit_ONE/img_linkitone_23.jpg)

### 步骤五　让您的开发板开始动作吧！

当您将范例程式上传至开发板后，请确保开发板有 Wifi 网路连线，并且有定时传送讯号显示装置已连接并正在待命中：

![](../images/Linkit_ONE/img_linkitone_15.JPG)

现在您已可至装置详情页面中，透过类比控制器资料通道来控制您的 LED 灯号亮度。当您将控制器调至 255 时，LED 灯亮度将会开到最大。当您将控制器调至 100 时，LED 灯还会是亮的，但是亮度降低。当您将控制器调至 0 时，LED 灯则会关闭。


![](../images/Linkit_ONE/img_linkitone_22.png)


恭喜！您已完成此教程！


