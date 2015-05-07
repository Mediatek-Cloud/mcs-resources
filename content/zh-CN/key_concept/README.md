在这个章节，我们将介绍有关于MediaTek Cloud Sandbox 的一些基本概念，帮助您打造您的穿戴式和物联网装置。您可以在MCS的**开发页面**，操作所有关于产品原型的开发的功能和服务。此外，您亦可在MCS的**我的装置页面**，看到所以您建立的或是有授权使用的装置。

# **开发**

在开发页面中，您可以建立一个或是多个的产品原型，并且为您的产品原型建立多个测试装置来和您的实体装置作连结。每个产品原型内含有以下内容：


- **资料通道**，您可以替每个资料通道选择一种资料型态类型来传输。
- **通知设定**，当装置状态改变到达预设时，发出通知。
- **使用者权限管理**，您可以管理您个别的产品原型和装置的使用者权限，让其他使用者能共同开发或浏览。
- **固件管理**，您可以管理您产品原型的所有固件，并决定是否更新至个别装置。
- **测试装置**，您可以将测试装置和实体装置作连结，来实现您的产品原型设计。

当您开发完产品原型后，就可以开始建立测试装置与您的实体装置作连结了。

## **产品原型**


![](../images/content_img/content_img-03.jpg)

**产品原型**是您开发装置的蓝图。每个产品原型都具有独特的Id和Key。

## **资料通道**

一个**资料通道**代表:
- 由MCS所储存的由装置的感应元件搜集而来的资料，或是
- 透过MCS传送给装置的指令

这些资料通道可以分为以下几类：
- 显示器
- 控制器
- 综合型显示控制器

## **资料通道类别**

###**显示器**

![](../images/content_img/content_img-04.jpg)

此类型的资料通道是专门储存和显示由装置的感应元件搜集而来的资料。例如从装置感应元件上船而来的温度，MCS会将此资料以时间序列方式储存。


###**控制器**

![](../images/content_img/content_img-05.jpg)

此类型的资料通道是专门用来传递指令至装置，已控制装置内元件的状态。例如控制灯的开或关。


###**综合型显示控制器**

![](../images/content_img/content_img-06.jpg)

此类型的资料型态能同时为显示器和控制器。例如冷气机的温度显示器，并且同时能控制冷气的开关或是调整温度。


## **资料型态**




每个资料通道都能用来传输以下的九种种资料型态的一种：

- **开/关**— 此类型的资料型态用来表示装置的两种状态，使用者能选择开启或是关闭装置的状态。例如　一盏灯的开或关。

- **类别**— 此类型的资料型态能用来表示一个任意的类别。您能定义任何您想要的类别和此类别相对的内容。例如您能用来储存星期，月份，或是风扇的状态（关，慢速，中速，高速）。

- **整数**— 此类型的资料型态能用来表示任意的整数，例如某一个使用者一天走了多少步的数值。

- **浮点数**— 此类型的资料型态能用来表示任意的浮点数，例如气温。

- **字串**— 此类型的资料型态用来表示字串，例如装置回传的讯息。

- **十六进位数**— 此类型的资料型态用来表示十六进位数值，例如LED灯的显示颜色。

- **GPS** — 此类型的资料型态用来表示地理位置，包含经度，纬度，和高度。

- **GPIO** — 此类型的资料型态用来表示GPIO的数位讯号。例如在Pin 4位置为High的讯号状态。

- **PWM** — 此类型的资料型态用来表示传递到GPIO的PWM数位讯号, 例如在Pin 3位置的level 15讯号。


## **通知**




此功能可让您定义触发电子邮件或基于云的通报标准，您身为装置的拥有者，除了会无条件的收到通知外，还能透过设定使用者权限来使其他使用者也收到相同的通知。

触发器可用于以下情况:

- 当某一个资料通道回传的资料超过或是低于预设值，将会触发通知条件，并且通知有权限的使用者。同时，资料质能然会被保存。

- 当控制器型态的资料通道的值被改片时，触发通知。


## **使用者权限管理**

此功能让您能够给予其他MCS用户各种访问产品原型或是测试装置的权限，如查看或是更改产品原型设置或是创建一个新的测试装置。


## **韧体服务**

使用此功能，您可以上传并管理特定产品原型的韧体。每当一个测试被新增时，MCS都会从原产品型中检测能够兼容的韧体，并提供用户通过空中更新设备韧体的服务。

## **测试装置**

此功能使您能够从产品原型的详细信息页面中建立测试装置。您创建的每个装置都会有一个**DeviceId ** 和 **DeviceKey** ，此讯息当您在呼叫MCS所提供的API时将会需要用到。您亦可于**My Device 页面**中查看装置的DeviceId以及DeviceKey等详细信息。


# **我的装置**

用您可以在**我的装置页面**来管理已创建或获得访问权限的设备。

在这个页面中，您可以查看资料通道，使用者权限，以及从产品原型继承过来的通知条件。您亦可以在此修改特定装置的通知条件和使用者权限设置。除了在产品原型页面的测试装置标签页中查看DeviceId和DeviceKey之外，您也可以在此页面中查看这些关于装置的细节。

此页面除了列出所有您所创建的和您有被授权访问的装置。不同的授权等级能决定您所能对此装置的操作。例如，如果你是该装置的浏览者，你只能读取数据，不能对装置设定进行任何的修改和更新。
