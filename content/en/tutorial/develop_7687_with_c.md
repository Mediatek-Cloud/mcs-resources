# Develop with LinkIt 7687 using C

In this guide you’ll learn the steps to create some applications to control the LinkIt 7687 from the web console of MCS using C.

## Develop with C

### Set up your development environment for Windows/Linux

**For Mac developer, please go to the next section.**

1. Download [v3.3.1 SDK](https://cdn.mediatek.com/download_page/index.html?platform=RTOS&version=v3.3.1&filename=LinkIt_SDK_V3.3.1_public.tar.gz).
2. Download [msys2](https://msys2.github.io/).
3. Download [gcc for Windows](https://launchpad.net/gcc-arm-embedded/4.8/4.8-2014-q3-update/+download/gcc-arm-none-eabi-4_8-2014q3-20140805-win32.zip).
4. Open msys2 and update it by:
```
update-core
```
5. Install msys2 packages by:
```
pacman -S tar unzip
pacman -S make
pacman -S git
pacman -S wget
```
6. Go to your **LinkIt_SDK_V3.3.1_public.tar** folder and unzip the file by:
```
tar -xvf ./LinkIt_SDK_V3.3.1_public.tar.gz && cd ./LinkIt_SDK_V3.3.1_public
```

7. Unzip the gcc files you donwloaded in step 2 and copy the **gcc-arm-none-eabi** folder.
8. Go to the **/LinkIt_SDK_V3.3.1_public/tools/gcc** folder and replace the **gcc-arm-none-eabi** folder under it with the one you've copied in step 7.
9. Go back to SDK root directory and modified line 15 in **build.sh** file as the following:
```
export EXTRA_VAR=-j
```

10. You should be able to build a simple image by input the following command in **SDK root** directory:
```
./build.sh mt7687_hdk iot_sdk_demo
```

11. After build completed, you should be able to see **mt7687_iot_sdk_demo.bin** file under **/out** folder in your SDK root directory.


### Set up your development environment for Mac

1. Download [v3.3.1 SDK](https://cdn.mediatek.com/download_page/index.html?platform=RTOS&version=v3.3.1&filename=LinkIt_SDK_V3.3.1_public.tar.gz).
2. Download [gcc for Mac](https://launchpad.net/gcc-arm-embedded/4.8/4.8-2014-q3-update/+download/gcc-arm-none-eabi-4_8-2014q3-20140805-mac.tar.bz2).
3. Unzip the gcc file you've downloaded in step 2 and rename the folder to **gcc-arm-none-eabi**.
4. Go to your **LinkIt_SDK_V3.3.1_public.tar** folder and unzip the file (you can use Mac build in command line terminal) by :
```
tar -xvf ./LinkIt_SDK_V3.3.1_public.tar.gz && cd ./LinkIt_SDK_V3.3.1_public
```

5. Go to the **/LinkIt_SDK_V3.3.1_public/tools/gcc** folder and replace the **gcc-arm-none-eabi** folder under it with the one you've got in step 3.
6. Go back to SDK root directory and modified line 15 in **build.sh** file as the following:
```
export EXTRA_VAR=-j
```

7.  You should be able to build a simple image by input the following command in **SDK root** directory:
```
./build.sh mt7687_hdk iot_sdk_demo
```

8. After build completed, you should be able to see **mt7687_iot_sdk_demo.bin** file under **/out** folder in your SDK root directory.

## How to burn the image file into LinkIt 7687

1. Connect LinkIt 7687 to your computer.
2. Drag and drop the **.bin** file into the 7687 disk.
3. You will see the **U6001** light in the LinkIt 7687 board is blinking which means the image is installing to the board.
4. After the process completed, the LinkIt 7687 disk disconnected and connected again which means the process is completed.


# Create application on MCS
Here you’ll create a prototype device in MCS and connect it to LinkIt 7687.

## Sign in to MCS console
Click [here](https://mcs.mediatek.com/oauth/en/login) to sign in.


Choose the application you would like to start with:

| [Simple Switch](../tutorial/7688_led_tutorial) | [Analog Controller ](../tutorial/7688_analog_tutorial) | [MD5](../tutorial/7688_gamepad_tutorial)| [FOTA](../tutorial/7688_fota_tutorial)|
| -- | -- | -- | -- |
|[![](../images/Linkit_ONE/img_linkitone_25.png)](../tutorial/7688_led_tutorial)|[![](../images/Linkit_ONE/img_linkitone_26.png)](../tutorial/7688_analog_tutorial)|[![](../images/7688/img_7688_32.png)](../tutorial/7688_gamepad_tutorial)|[![](../images/7688/img_7688_32.png)](../tutorial/7688_gamepad_tutorial)|

