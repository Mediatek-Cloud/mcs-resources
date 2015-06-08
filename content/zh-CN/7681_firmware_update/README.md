# LinkIt™ Connect 7681 Firmware Update Instruction


## Resources

- Mobile APK: MediaTek Cloud Sandbox Mobile Application for Android **(>= 2.5.0)** on [Google Play](https://play.google.com/store/apps/details?id=com.mediatek.iotcloud). Please check your Android application version is above 2.5.0.
- 7681 Latest Firmware(2015/05/25): [MT7681_sta_header.bin](https://s3-ap-southeast-1.amazonaws.com/mtk.linkit/mcs-resources/firmwares/MT7681_sta_header.bin). With ability to show 7681's Mac Address.

## Steps For 7681 Update

1. Update 7681 with latest firmware. Please follow [MediaTek LinkIt Connect 7681 Developer’s Guide: 3.2 Firmware uploader](https://labs.mediatek.com/fileMedia/download/60b77480-f08e-46de-b4ab-513916dcff75) for further information. It's recommended to follow `3.2 Firmware uploader`, and use syntax like below:
	
	on Windows
	
	```
	> mt7681_uploader.exe -f MT7681_sta_header.bin -c COM7
	Or
	> python mt7681_uploader.py -f MT7681_sta_header.bin -c 	COM7
	```
	
	While on Linux
	
	```
	> python mt7681_uploader.py -f MT7681_sta_header.bin -c /dev/ttyUSB0
	```


2. Use `AT#MacAddr` to get the Mac address.


## Steps For Smart Connection on Android App

1. Install latest MediaTek Cloud Sandbox Mobile Application for Android on [Google Play](https://play.google.com/store/apps/details?id=com.mediatek.iotcloud)
2. Link to certain Wifi AP
3. Sign in & Click on the `+` button on the right-bottom side to add devices
4. Click on `Smart Connection` and input the Wifi SSID/Password to start Smart Connection
5. After the "Processing..." dialog dismiss, you could either click on `Refresh Button` on the right-top side, or repeat **Step 4.** to re-scan devices.

- It's recommended to click "Refresh" 2 or 3 times more if you are sure that the settings listed below are correct, the devices might not be shown for the first Smart Connection process. We will desperately improve the process to be more friendly for you as soon as possible.

- You might see `No results` if you are doing **Step 4.** for the 1st time, since 7681 might not respond that fast to Smart Connection. Please manually repeat **Step 5.** to re-scan devices.

- It should be guaranteed that if you could see IP Address & other connected info on the command line tool / terminal like SecureCRT & CoolTerm with the indicated Wifi, you should see it on android mobile app.


## Terminal Commands

1. `AT#Reboot`: This is the same as press the real button on 7681. Please NOTICE that this only reboot the 7681 device.

	```
	==> Recovery Mode
	<== RecoveryMode
	```

2. `AT#Default`: Reset the 7681 device to default status. This clear the connected Wifi AP and set the activation status to un-activated. You should see the log below.

	```
	SM=0, Sub=0
	SM=1, Sub=0
	```

3. `AT#MacAddr`: Show the Mac Address of this 7681. e.g. `MAC address-00:0c:12:34:56:78`



## Terminal Logs

1. Default status

	```
	SM=0, Sub=0
	SM=1, Sub=0
	```


2. Certain Wifi AP has been set, while the Wifi AP is not available now.

	```
	SM=0, Sub=0
	SM=2, Sub=0
	```
	
3. Certain Wifi AP has been set, and is currently connected to it.

	```
	SM=2, Sub=0
	SM=3, Sub=0
	Auth with:ssid = YOUR_WIFI_SSID, auth mode = SOME_NUMBER,
	SM=3, Sub=1
	SM=4, Sub=0
	SM=4, Sub=1
	SM=5, Sub=0
	SM=6, Sub=0
	```
	an example in [MediaTek LinkIt Connect 7681 Developer’s Guide: 4.5.1 States](https://labs.mediatek.com/fileMedia/download/60b77480-f08e-46de-b4ab-513916dcff75) is like
	
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

4. 7681 has not been activated on MCS server yet.

	```
	cloud client parameter error or no setting, please config it!
	```

5. 7681 has already been activated on MCS server.

	```
	cloud client had beeb actived!
	```


## Trouble-Shooting

If you cannot see your device on "Add Device" page, the reason might be

- 7681 Check points (using command line tool)
	a. Firmware is out-dated. Please check if you can see Mac address using `AT#MacAddr`. If yes, then it's updated.
	b. 7681 has been connected to another Wifi AP. If you cannot see  "SM=1", but keep seeing "SM=2", then it's already connected to another Wifi AP. Please use `AT#Default` to reset.
- Mobile APK
	a. APK is out-dated. Please install the latest apk as attached.
	b. Smart Connection hasn't been established. As **step 5.** mentioned, it's possible to see "No result" for the first time. Ideally process should be that after you click on "Smart Connection", the 7681 is scanned, and the terminal should show some info about connected to the Wifi AP with SSID & given IP Address. At this time, if you refresh again, the device should show on the list. And after this first connection, you should be able to quickly see devices next time when you enter "Add Device" page.


Others

- Refreshing. It's recommended to refresh multiple times if you could not find
- `AT#Default`: Reset 7681 to default status, without Wifi binding. 7681s that already connected with other Wifi AP could not be scanned by other Smart Connection. It's required to use `AT#Default` to reset 7681, so that it could be smart connected by MCS App.
