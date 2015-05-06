在這個章節，我們將介紹有關於MediaTek Cloud Sandbox 的一些基本概念，幫助您打造您的穿戴式和物聯網裝置。您可以在MCS的開發頁面，操作所有關於產品原型的開發的功能和服務。此外，您亦可在MCS的我的裝置頁面，看到所以您建立的或是有授權使用的裝置。

# **開發**

在開發頁面中，您可以建立一個或是多個的產品原型，並且為您的產品原型建立多個測試裝置來和您的實體裝置作連結。
每個產品原型內含有以下內容：


- **資料通道**，您可以替每個資料通道選擇一種資料型態類型來傳輸。
- **通知設定**，當裝置狀態改變到達預設時，發出通知。
- **使用者權限管理**，您可以管理您個別的產品原型和裝置的使用者權限，讓其他使用者能共同開發或瀏覽。
- **韌體管理**，您可以管理您產品原型的所有韌體，並決定是否更新至個別裝置。
- **測試裝置**，您可以將測試裝置和實體裝置作連結，來實現您的產品原型設計。

當您開發完產品原型後，就可以開始建立測試裝置與您的實體裝置作連結了。


## **產品原型**


![](../images/content_img/content_img-03.jpg)

**產品原型**是您開發裝置的藍圖。每個產品原型都具有獨特的Id和Key。


## **資料通道**

一個 **資料通道** 代表:
- 由MCS所儲存的由裝置的感應元件蒐集而來的資料，或是
- 透過MCS傳送給裝置的指令

這些資料通道可以分為以下幾類：
- 顯示器
- 控制器
- 綜合型顯示控制器

## **資料通道類別**

###**顯示器**

![](../images/content_img/content_img-04.jpg)

此資料通道類型是專門儲存和顯示由裝置的感應元件蒐集而來的資料。


This data channel type is for data generated from a component of a device that has no related commands. For example data from a temperature sensor that is pushed to the sandbox and stored as a sequence over time.


###**Controller**

![](../images/content_img/content_img-05.jpg)

This data channel type is for data generated in the sandbox and sent to the device to control the setting of a logical or physical component in the device. For example, a switch to turn a light on or off.


###**Hybrid**

![](../images/content_img/content_img-06.jpg)

This data channel enables a Display and Controller data channel to be combined, where there is a logical relationship between the two. For example, as between the data from a temperature sensor and the control settings for an air conditioning unit.


## **Data Types**




Each Data Channel can hold one of seven types of data:

- **ON/OFF** — this data type represents a switch and enables the user to activate or deactivate a component of the device, such as turning a light on or off.

- **Category** — this data type represents an arbitrary category. You’re free to define the category and its content as you wish. For example, you could store weekday, month, fan settings (off, slow, medium and fast) and alike.

- **int** — this data type represents an arbitrary integer, such as the number of steps a user has taken.

- **float** — this data type represents an arbitrary floating point number, such as temperature.

- **string** — this data type represents a string, such as a message issued by the device.

- **HEX** — this data type represents a hexadecimal value, such as the color used in an LED display.

- **GPS** — this data type represents a geo-location identified by longitude, latitude, elevation and related attributes.

- **GPIO** — this data type represents a digital signal for a specific GPIO pin, such as HIGH on Pin 4.

- **PWM** — this data type represents a PWM signal delivered to a specific GPIO pin, such as level 15 on Pin 3.


## **Notifications**




This function enables you to define criteria that trigger an email or cloud-based notification as well as define additional user’s the notification will be sent to — you as the prototype owner receive notifications by default.

Triggers are available for:

- Data received on a channel being above or below a specific value, which will issue a defined number of notifications while the data remains above or below the trigger value.

- Each time the data value is changed on a Controller data channel.


## **User privileges**

This feature enables you to give other MCS users various privileges to access the Prototype, such as the ability to view the Prototype settings, create a device and alike.


## **Firmware**

Using this feature you can upload and manage the firmware for a specific prototype. Once devices have been created from the prototype the sandbox will detect compatible devices and offer their users the option to update the devices’ firmware over the air.

## **Test Devices**

This feature enables you to create test devices from the Prototype details. Each device you create is given a **Device ID** and **Device Key**, which you use in the MediaTek Cloud Sandbox APIs to identify data pushed to and pulled from the device. Device details, along with their ID and key, are displayed in your **My Devices** page.


# **My Devices**

You use **My Devices** to manage the devices you have created or have been given access to.

In this page, you can see the data channel, user privilege, and notification configurations as defined in the device’s prototype. You can modify the notification and user privilege settings for specific devices on this page. You can also see the device Id and device key, in addition to being able to see those details in the Test device tab in a prototype’s details page.

In addition to listing all the devices created for your prototypes, this page also shows devices from other prototypes that you have been given the access to. The actions you can do to the devices vary depending on the privileges granted to you. For example, if you are a viewer of the device, you can only see the data and cannot make any change to the device.

