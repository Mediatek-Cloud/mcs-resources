# Firmware Management

MediaTek Cloud Sandbox(MCS) enables you to manage the device firmware and supports Firmware Over-The-Air (FOTA) for upgrade.

MCS provides firmware repository services for the prototypes and test devices. This service provides basic firmware upload and download with version control, a web console for firmware management as well as APIs that enable test devices to retrieve compatible firmware from MCS.

MCS won't handle the complete device firmware upgrade process on your device, the developers have to implement this and leverage the firmware related library in your development board's SDK.

## Upload a Firmware to MCS
You can manage the firmwares for your prototype on **Prototype Details -> Firmware** page. 

To upload your first firmware, you just need to click **Add firmware** link, fill up the name and version of this firmware, select the firmware file and click **Upload**.

![](../images/Firmware/img_firmware_01.png)


In the next step, you could configure the compatibility of this firmware. **All firmware** is selected by default, or you could also select **Limited firmware** and opt in the individual firmwares which are compatible with this version. 

Only the devices which are using the compatible firmwares are allowed to fetch this firmware information and be upgraded to this version.

Now, you can either click **Done** to finish the firmware upload process or click **Next** to push the firmware to selected devices.
![](../images/Firmware/img_firmware_02.png)


After selecting the devices you'd like to upgrade, click **Push**. 
![](../images/Firmware/img_firmware_03.png)

You can also trigger this by clicking on the push icon in the firmware list.
![](../images/Firmware/img_firmware_04.png)

## Upgrade the Firmware on Device

After the firmware is uploaded to MCS platform, you could **push** it to the connected devices on MCS web console or use **MCS APIs** to fetch the information of compatible firmwares.

The **push firmware** function is available on both **Prototype -> Firmware** or **Device details -> Firmware** page.

Please note that the **Push** button is only available when the device is connected to MCS platform. The icon in front of the device name indicates the device connection status. The green light means the device is connected; and it turns to grey color if the device is offline.

![](../images/Firmware/img_firmware_05.png)

Click **Push** button next to the firmware you want to use for device upgrade. After the upgrade process finishes, you will see a success message as shown below.

![](../images/Firmware/img_firmware_06.png)


Please note: MCS could only **push** the firmware information down to the selected device, but it will not handle the complete firmware upgrade process on the device side. You have to implement your own program to download the firmware binary and upgrade the firmware accordingly.

After you click **push** button, MCS will send out the firmware information selected devices. Here are the supported protocol and format.

1. TCP connection: **deviceId,deviceKey,timestamp,FOTA,version,MD5,URL**, for example

	```
	Dbxxxx9k,TPJVxxxxxxxxBxBv,1513132150790,FOTA,2.0,null,https://cdn.mediatek.com/firmwares/P9MxxxxxxbTK/6a94dxxxxxxxxxxxxxxxxxxxx61f5df/a.bin
	```
	
	* deviceId: the device ID of the device
	* deviceKey: the device key of the device
	* timestamp: the timestamp when this firmware is pushed
	* FOTA: a fixed string which stands for "Firmware Over-The-Air"
	* version: the version of this firmware
	* MD5: the MD5 hash of this firmware
	* URL: the download URL of this firmware

2. MQTT connection: **timestamp,FOTA,version,MD5,URL**, for example

	```
	1513133357160,FOTA,2.0,null,https://cdn.mediatek.com/firmwares/P9MxxxxxxbTK/6a94dxxxxxxxxxxxxxxxxxxxx61f5df/a.bin
	```

	* timestamp: the timestamp when this firmware
	* FOTA: a fixed string which stands for "Firmware Over-The-Air"
	* version: the version of this firmware
	* MD5: the MD5 hash of this firmware
	* URL: the download URL of this firmware

Also, for devices based on LinkIt Connect 7681, the firmware upgrade process is handled by MCS, and you do not need to do any additional coding. However, you need to set a unique firmware version due to device limitation related to LinkIt Connect 7681, which is that it can only upgrade to a firmware with higher version.

## MCS APIs

MCS provides the following APIs for firmware management and development.

1. [Report firmware version of a device](http://mcs.mediatek.com/resources/latest/api_references/#report-device-firmware): This API allows device to report its current firmware version back to MCS platform. Only the version number which has been uploaded onto MCS platform can be reported.

2. [Retrieve the compatible firmwares](http://mcs.mediatek.com/resources/latest/api_references/#report-device-firmware): After the device has reported its firmware version to MCS platform, this API provides a list of firmwares which are compatible with the current version. If the device hasn't reported its firmware yet, then, only the firmwares without any compatibility limitation are listed.

3. [Retrieve the compatible firmwares by version](https://mcs.mediatek.com/resources/latest/api_references/#retrieve-compatible-firmware-by-version): This API provides a flexibility to query the firmware compatibility by simply specifying the version number in the request.

4. [Retrieve firmware URL](https://mcs.mediatek.com/resources/latest/api_references/#retrieve-firmware-url): This API returns the download URL of specified firmware binary file.




