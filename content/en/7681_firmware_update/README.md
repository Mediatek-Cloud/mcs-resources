# LinkIt™ Connect 7681 Firmware Update Instruction


## Resources

- Mobile APK: MediaTek Cloud Sandbox Mobile Application for Android **(>= 2.5.0)** on [Google Play](https://play.google.com/store/apps/details?id=com.mediatek.iotcloud). Please check your Android application version is above 2.5.0.
- LinkIt Connect 7681 Latest Firmware(2015/05/25): [MT7681_sta_header.bin](https://s3-ap-southeast-1.amazonaws.com/mtk.linkit/mcs-resources/firmwares/MT7681_sta_header.bin). With LinkIt Connect 7681's MAC address display.
## Steps for LinkIt Connect 7681 Firmware Update

1. Update your LinkIt Connect 7681 development board with the latest firmware. Please check [MediaTek LinkIt Connect 7681 Developer’s Guide: section 3.2, Firmware Uploader](https://labs.mediatek.com/fileMedia/download/60b77480-f08e-46de-b4ab-513916dcff75) for more information. Please use the following syntax as described in the aforementioned section from the developer’s guide:
	For Windows:

	```
	> mt7681_uploader.exe -f MT7681_sta_header.bin -c COM7
	```
	
	or
	
	```
	> python mt7681_uploader.py -f MT7681_sta_header.bin -c COM7
	```

	For Linux:

	```
	> python mt7681_uploader.py -f MT7681_sta_header.bin -c /dev/ttyUSB0
	```


2. Use `AT#MacAddr` to get the Mac address.


## Steps for Smart Connection on Android App

1. Install the latest MediaTek Cloud Sandbox mobile application for Android on [Google Play](https://play.google.com/store/apps/details?id=com.mediatek.iotcloud).
2. Link to a Wi-Fi AP.
3. Launch the App, sign in and click on the **+** button on the bottom-right side to add devices.
4. Click on **Smart Connection** and enter the Wi-Fi SSID and Password.
5. After the Processing icon is dismissed and the device your would like to connect is not displayed in the list, you can either click on **Refresh Button** on the top-right cornor, or repeat **Step 4.** to re-scan for devices.

- It's recommended to click **Refresh** 2 or 3 times more if you are sure that the settings listed below are correct becuase the devices might not be displayed in the first Smart Connection process. MCS is working hard on improving the process to be more user-friendly, please check back with us for updates.

- You might see **No results** from doing **Step 4.** for the first time, since LinkIt Connect 7681 might have not responded to Smart Connection yet. Please manually repeat **Step 5.** to re-scan for devices.

- It should be certain that if you can see IP Address and other connected info in the command line tool or terminal like SecureCRT and CoolTerm with the indicated Wi-Fi, you should also see it on Android mobile app.


## Terminal Commands

1. `AT#Reboot`: This command is equivalent to pressing the real button on a LinkIt Connect 7681. Please NOTE that this reboots the 7681 device.

	```
	==> Recovery Mode
	<== Recovery Mode
	```

2. `AT#Default`: Resets the LinkIt Connect 7681 device to default status. This clears the connected Wi-Fi AP and sets the activation status to de-activated. You should see a log similar to below.

	```
	SM=0, Sub=0
	SM=1, Sub=0
	```

3. `AT#MacAddr`: Shows the LinkIt Connect 7681’s MAC Address, for example:

	```
	MAC address-00:0c:12:34:56:78
	```


## Terminal Logs

1. Default status

	```
	SM=0, Sub=0
	SM=1, Sub=0
	```


2. Certain Wi-Fi AP has been set, while the Wi-Fi AP is not available now.

	```
	SM=0, Sub=0
	SM=2, Sub=0
	```

3. Certain Wi-Fi AP has been set, and is currently connected to it.

	```
	SM=2, Sub=0
	SM=3, Sub=0
	Auth with:ssid = YOUR_Wi-Fi_SSID, auth mode = SOME_NUMBER,
	SM=3, Sub=1
	SM=4, Sub=0
	SM=4, Sub=1
	SM=5, Sub=0
	SM=6, Sub=0
	```
	An example in [MediaTek LinkIt Connect 7681 Developer’s Guide: 4.5.1 States](https://labs.mediatek.com/fileMedia/download/60b77480-f08e-46de-b4ab-513916dcff75) is like

	```
	==> Recovery Mode /* start to running recovery/Calibration image*/
	<== Recovery Mode /* end to running recovery/Calibration image*/
	(-) /* start to running station image*/
	SM=0, Sub=0 /* Change to “WIFI_STATE_INIT” */
	SM=1, Sub=0 /* Change to “WIFI_STATE_SMTCNT” */
	[WTask]5001 /*--output timer log period to notice system alive--*/
	SM=2, Sub=0 /* Change to “WIFI_STATE_SCAN” */
	SM=3, Sub=0 /* Change to “WIFI_STATE_AUTH”, is going to send Auth Request*/
	Auth with:ssid = belkin, auth mode = 9, /*--output the target AP’s information “SSID, AuthMode”-- */
	SM=3, Sub=1 /* Change to “WIFI_STATE_AUTH” is waiting Auth Response*/
	SM=4, Sub=0 /* Change to “WIFI_STATE_ASSOC”, is going to send Assoc Request*/
	SM=4, Sub=1 /* Change to “WIFI_STATE_ASSOC”, is waiting Assoc Response */
	SM=5, Sub=0 /* Change to “WIFI_STATE_4WAY” */
	[WTask]10005
	SM=6, Sub=0 /* Change to “WIFI_STATE_CONNED”, start to get IP*/
	[WTask]15006
	Got IP:192.168.2.12/* Got IP from target AP*/
	[WTask]20009
	```

4. LinkIt Connect 7681 has not been activated on MCS server yet.

	```
	cloud client parameter error or no setting, please config it!
	```

5. LinkIt Connect 7681 has already been activated on MCS server.

	```
	cloud client had beeb actived!
	```


## Troubleshooting

If you can't see your device on **Add Device** page, it could be due to one of the following reasons:

- LinkIt Connect 7681 check points (using command line tool)

	a. __Firmware is out-dated__. Please check the MAC address using **AT#MacAddr**. If you can see it, then the device’s updated.

	b. __7681 is connected to another Wi-Fi AP__. If you can't see "SM=1", but sees __"SM=2"__, then it's already connected to another Wi-Fi AP. Please use `AT#Default` to reset the device.

- Mobile APK

	a. __APK is out-dated__. Please install the latest APK as attached.

	b. __Smart Connection hasn't been established__. As **Step 5.** described, it's possible to get **No result** for the first time you try smart connection. Ideally the process should be that after you click on the **Smart Connection**, the 7681 is scanned, and the terminal shows information about SSID and IP Address about connected to the Wi-Fi AP. If that didn’t happen, you should click **Refresh** again, and the device should show on the scanned list. After a successful first connection, you should be able to see the device next time you enter **Add Device** page.

Others

- Refresh Scan. It's recommended to refresh scan multiple times if you can’t find the AP.- `AT#Default`: Resets LinkIt Connect 7681 to default status without a Wi-Fi binding. For 7681s that are already connected to other Wi-Fi AP, they aren’t scanned by other Smart Connection. It's required to use `AT#Default` to reset LinkIt Connect 7681 in order to be smart connected by the MCS App.

