# Using trigger and action

## How to add trigger and action

The user can set the trigger and action for a data channel when its value passes the limit of the defined range. The user will get email notification or the GCM notification based on the trigger and action setting. Please be noted that MCS currently only support trigger and action for integer and float data channel types.


On the Prototype detail page, click on the **Trigger & action** tab.

![](../images/Trigger/img_trigger_01.png)

Click on the **Trigger & action** to see the popup dialog to enter the trigger name and description.

![](../images/Trigger/img_trigger_02.png)

Then click Next button to set the trigger criteria by selecting the data channel you would like to set alert for and give the value. The rules include greater than, lower then, equal to, and between.

To have more than one data channel rules in trigger criteria, all data channel rules need to be satisfied to trigger the action(AND logic). The user can create separate trigger and action rules to have the OR loigic.

![](../images/Trigger/img_trigger_03.png)

Click Next button to select the trigger action. You can select to get email or GCM notification when your trigger criteria are met. The email and GCM notification will be sent to anyone who has the access to the test device.


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
