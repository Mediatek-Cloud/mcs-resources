# LinkIt ONE Tutorial

Before you dump some code onto your LinkIt ONE board and link it up to the MCS cloud, you're going to want to make sure your computer and board are set up the right way.

# Computer development environment and Board Setup


1. Download the Arduino IDE and LinkIt ONE SDK

    [Mac](http://labs.mediatek.com/site/global/developer_tools/mediatek_linkit/get-started/mac/install/)

    [Windows]( http://labs.mediatek.com/site/global/developer_tools/mediatek_linkit/get-started/windows/install/)
2. Update the firmware on your board

    [Mac](http://labs.mediatek.com/site/global/developer_tools/mediatek_linkit/get-started/mac/update/)

    [Windows](http://labs.mediatek.com/site/global/developer_tools/mediatek_linkit/get-started/windows/update/)

3. Configure the SDK in the Arduino IDE, and connect your board to Wi-Fi via a port selection.

    [Mac](http://labs.mediatek.com/site/global/developer_tools/mediatek_linkit/get-started/mac/configure/)

    [Windows](http://labs.mediatek.com/site/global/developer_tools/mediatek_linkit/get-started/windows/configure/)


An excellent guide for this setup can be found [here](http://labs.mediatek.com/site/global/developer_tools/mediatek_linkit/get-started/index.gsp). Please come back to this guide after finishing all the steps above, which can be done by visiting all the links in order.


**Just a note: The current LinkIt ONE SDK is only compatible with Arduino IDE versions 1.5.6-r2 BETA or 1.5.7 BETA.**


# Add Libraries

Now that your computer and your IDEs are all set up, it's time to integrate some libraries! For this example, the only library we need is the HttpClient library, which can be found [here](https://github.com/amcewen/HttpClient/releases). Download the .zip file, then open up your Arduino IDE.

In the "Sketch" drop-down, click on "Import Libraries", then navigate to your .zip file.

![](../images/Linkit_ONE/img_linkitone_24.png)

# MCS Cloud Setup
Almost there! At this point, you're going to want to set up the MCS cloud so you can control and track your board. We've made it really easy; no downloading or coding required!

Choose the application you would like to start with:

| [Simple Switch tutorial](../tutorial/implementing_using_linkit_one) | [Analog Controller tutorial](../tutorial/implementing_analog_using_linkit_one) |
| -- | -- |
|[![](../images/Linkit_ONE/img_linkitone_25.png)](../tutorial/implementing_using_linkit_one)|[![](../images/Linkit_ONE/img_linkitone_26.png)](../tutorial/implementing_analog_using_linkit_one)|

