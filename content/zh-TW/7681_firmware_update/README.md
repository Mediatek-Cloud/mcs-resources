# 7681 Firmware Update Instruction


## Resources

- Mobile APK: MediaTek Cloud Sandbox Mobile Application for Android **(>= 2.5.0)** on [Google Play](https://play.google.com/store/apps/details?id=com.mediatek.iotcloud). Please check your Android application version is above 2.5.0.
- 7681 Latest Firmware(2015/05/25): [MT7681_sta_header.bin.gz](https://s3-ap-southeast-1.amazonaws.com/mtk.linkit/mcs-resources/firmwares/MT7681_sta_header.bin.gz). Please unzip it to get **MT7681_sta_header.bin** for further update setup.

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


## Steps For Android App

1. Install latest MediaTek Cloud Sandbox Mobile Application for Android on [Google Play](https://play.google.com/store/apps/details?id=com.mediatek.iotcloud)
2. Link to certain Wifi AP
3. Sign in & Click on the `+` button on the right-bottom side to add devices
4. Click on `Smart Connection` and input the Wifi SSID/Password to start Smart Connection
5. After the "Processing..." dialog dismiss, you could either click on `Refresh Button` on the right-top side, or repeat **Step 4.** to re-scan devices.

- It's recommended to click "Refresh" 2 or 3 times more if you are sure that the settings listed below are correct, the devices might not be shown for the first Smart Connection process. We will desperately improve the process to be more friendly for you as soon as possible.

- You might see `No results` if you are doing **Step 4.** for the 1st time, since 7681 might not respond that fast to Smart Connection. Please manually repeat **Step 5.** to re-scan devices.

- It should be guaranteed that if you could see IP Address & other connected info on the command line tool / terminal like SecureCRT & CoolTerm with the indicated Wifi, you should see it on android mobile app.



## Detailed Update Information

#### Mobile APK Update

- Please reference MediaTek Cloud Sandbox on [Google Play](https://play.google.com/store/apps/details?id=com.mediatek.iotcloud).

### 7681 Firmware Update

The command for SecureCRT & CoolTerm to get the Mac address of a 7681 is `AT#MacAddr`. When seeing "Cloud Client parameter error or no setting, please config it!", it means that this 7681 hasn't connected with any Wifi AP yet, and is able to be Smart Connected by any other Wifi AP.


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
- `AT#Default`: Reset 7681 to default status, without Wifi binding. 7681s that already connected with other Wifi AP could not be scanned by other Smart Connection. It's required to use `AT#Default` to reset 7681, so that it could be smart connected by .
