# Beta-release prototype

When your prototype is sufficiently tested and you are ready to release it to a samll group of user for trial run, you can beta-release the prototype.

Once you beta-release your prototype, the prototype will be frozen, which means you can no longer make any modification to the prototype including the prototype detail, data channels, and triiger & action rules. However, you can still add other developers to join this prototype or continue to upload firmware for the test device or device to upgrade.

## How to beta-release prototype

To beta-release the prototype, simply click on the **Beta-release** button on the upper right corner in the prototype detail page.

**(補一張圖在這邊~)**

# Create Device

User can only create devices after the prototype is beta-release and frozen. User can choose to create device at once or separately base on his/her needs.

After devices are created, user can manage those devices in **Management** page, where devices are categorized by prototype. Each device will have a unique activation code, the device will only be available after being activated.


## How to create device

You can choose to create device all at once or separately. Also, you can choose to enter the serial number by manual input or using a pre-defined csv file.

Step 1. Click the Create Device button on the upper right corner in a beta-released prototype.

**(補一張圖在這邊~)**

Step 2. Enter the device name and description.

Step 3. Enter the serail number for the devices. The serail number format is limited to A-Z, a-z, 0-9, and must less the 50 characters.

Step 4. Click create button.

**(補一張圖在這邊~)**

Devices are created in non-activated state and each device will have a unique activation code. The device will only be available after being activated. After activated, the device will get its deviceId and deviceKey like the test device and start to work.

The developer can find the activation code and all other device related information in the **Management** page.

# Device Management

After the prototype is beta-released and you have created several devices for it. You can find all the devices in the **Management** page.

**(補一張圖在這邊~)**

The developer can see the device count and activation rate for each prototype in the Management page. The developer can further check the devices for each prototype by clicking into the specific prototype in that page.

The following information will be enclosed:
* Device online status
* Device Serial number
* Device activation code
* Device activation date
* Device last data point time

**(補一張圖在這邊~)**

Please be noted that all test device and device will be counted as your account limitation no matter it is activaed or non-activated. Please be noted that only when a device is in non- activated state can it be deleted.

## How to activate device

When the device is created, you can find the activation code in the **Management** page. Each device can only be activated once using the activation code.

At current moment, MCS only provides API to activate device. Please find the **device activation** in API reference page [here](../api_references/). For the developer, you can design your own way to activate the device by calling our API.


After the device is activated, there will be a device detail page listing the device detail including the deviceId, deviceKey, data channel value, trigger & action rules, and firmware version.

