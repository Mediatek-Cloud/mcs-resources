# Using trigger and action

## How to add trigger and action

The user can set the trigger and action for a data channel when its value passes the limit of the defined range. The user will get email notification or the Mobile Push notification based on the trigger and action setting. In addition, MCS supports webhook trigger, you can input the URL that you would like to recieve this trigger.

Please be noted that MCS currently only supports trigger and action for integer and float data channel types. Also, only data points uploaded by the device (data points uploaded with deviceKey) will trigger the action. The data points uploaded by user (via web using authentication) will not be triggered.


On the Prototype detail page, click on the **Trigger & action** tab.

![](../images/Trigger/img_trigger_01.png)

Click on the **Add trigger & action** to see the popup dialog to enter the trigger name and description.

![](../images/Trigger/img_trigger_02.png)

Then click on Next button to set the trigger criteria by selecting the data channel you would like to set alert for and give the value. The rules include greater than, lower then, equal to, and between.

To have more than one data channel rules in trigger criteria, all data channel rules need to be satisfied to trigger the action(AND logic). The user can create separate trigger and action rules to have the OR loigic.

![](../images/Trigger/img_trigger_03.png)

Click Next button to select the trigger action. You can select to get email or Mobile Push notification when your trigger criteria are met. The email and Mobile Push notification will be sent to anyone who has the access to the test device.

Furthermore, you are allowed to use MCS pre-defined variables in Title and Content fileds to capture the real value when the action was triggered.


![](../images/Trigger/img_trigger_04.png)

The test device will inherit all the trigger and action from its parent prototype. In the test device, user can only change the value of the trigger criteria or select to turn on or turn off specific trigger and action.

![](../images/Trigger/img_trigger_05.png)

## Setting trigger and action for different mobiles

If a user has mutiple mobile devices, MCS allows the user to set if each mobile will receieve the mobile push notification or not. The user can find the setting in two place:

1. In the **User Profile** page to turn on or off all the notification from MCS to specific mobile.
2. In the **Test device** page to turn on or off the notification for specific test device to specific mobile.

In the **User Profile** page, you can see a mobile list here. All the user's mobiles will be listed here if it has the MCS app installed on. You can use the swithc here to control if specific mobile will receivev **all** the notification from MCS.

![](../images/Trigger/img_trigger_06.png)

In the **Test device** page, expand the **Manage your action** section and you can also see a mobile list here. All the user's mobiles will be listed here if it has the MCS app installed on. You can use the switch here to control if specific mobile will receive the notification from **this test device**.

![](../images/Trigger/img_trigger_07.png)



# Set up a webhook trigger

To set up a webhook trigger, you have to select the **webhook** as the action in the Trigger & action tab in the prototype. And input the url that you would like to get the webhook trigger.

![](../images/Trigger/img_trigger_08.png)

There is a Test button for you to test if the trigger has been sent to the url. The device name, deviceId, deviceKey, and the triggered value will be sent to the triggered url.

# Use variables in notification message

MCS provides pre-defined variables which can be used in both Title and Content fileds. These variables will be replaced with real values when the action is triggered. The pre-defined variables include:

* **${deviceId}**: The ID of device
* **${deviceName}**: The name of device
* **${value}**: The value of this data channel

![](../images/Trigger/img_trigger_09.png)

For example:

You can set Email content as
	
	The temperature of ${deviceName} is now ${value}.

The message delivered to users will be replaced with real value, like 

	The temperature of My Living Room is now 30.
	