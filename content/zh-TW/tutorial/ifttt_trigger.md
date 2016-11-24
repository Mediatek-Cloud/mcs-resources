# Connecting MCS with IFTTT

In this tutorial, we will learn how to set up MCS with [IFTTT](https://ifttt.com/). You can connect your MCS device with IFTTT and interact with many other IoT and social media service providers on IFTTT platform such as Google and Facebook.

Note: MCS currently interacts with IFTTT using **Maker Service**. For more information about Maker Service, please refer to this [link](https://ifttt.com/maker).


In this tutorial, you will learn how to connect MCS with IFTTT to create a applet that* when the temperature data channel in MCS is above 30 degree, then turn on the switch data channel*. To fulfill this, you need to create a prototype in MCS to have:
1. a display integer data channel called **temperature**.
2. a controller switch data channel called **switch**.
3. create a test device.
4. Go to MCS profile page and **Apply for appId and appSecret**.


## Send MCS trigger to IFTTT

If you wish to send MCS trigger to any service on IFTTT platform, you will need to set up a **webhook notification**. To do this, it means you will make the notification as an IF criteria in your IFTTT applet.

Let's assume we will *send a webhook notification to IFTTT when the temperature data channel is above 30 degree* as the IF criteria as an example.
1. Obtain your unique **maker url** on IFTTT. You can find this in the Maker Service setting page after logged in and connect with Maker Service.
2. Create a applet by click on the **New Applet** button on IFTTT.
3. Click **this** link and choose **Maker Service**.
4. Select **Receive a web request**.
5. Enter the **Event Name** you like. For example: temperature_over_30.
6. Go to MCS prototype trigger and action tab.
7. Create a webhook trigger called **temperature_over_30** and input the Url as the following.
```
https://maker.ifttt.com/use/{useId}
```
8. You can also customized the message body you would like to send to IFTTT.
9. Now you've completed setting up MCS to send trigger to IFTTT IF criteria.

Note: MCS support sending variable via webhook. If your IFTTT recipe needs to get additional information, you can use the ingredient that IFTTT provided and set the variable sent from MCS webhook to be the ingredient.

## Receiving command from IFTTT

Let's finish the assumption *if the temperature data channel is above 30 defree, then turn on the switch data channel*.

When the **temperature_over_30** in MCS is triggered, then we turn on the switch data channel in MCS via IFTTT.
1. Go to the IFTTT website, and finish your IF criteria as previous paragraph.
2. Continue creating the recipe by clicking on the **that** link.
3. Choose **Maker Service**.
4. Select **Make a web request**.
4. Enter the Url as the following:
```
https://api.mediatek.com/mcs/v2/devices/{deviceId}/datapoints
```
5. Select **POST** for Method.
6. Select **application/json** for Content Type.
7. Enter the body as the following:
```
{
    "appId":"{your appId}",
    "appSecret": "{your appSecret}",
    "datapoints":[
    {
        "dataChnId":"switch",
        "values":{ "value":"1" }
    }
    ]
}
```
8. Click **Create Action** button to Finish.

Now you can test the IFTTT applet by uploading an integer above 30 to MCS temperature data channel, then wait for a moment, you will see the switch data channel automatically turn on.







