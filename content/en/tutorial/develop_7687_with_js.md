# Develop with LinkIt 7687 using Node.js

In this guide you’ll learn the steps to create some applications to control the LinkIt 7687 from the web console of MCS using Node.js.


## Develop with Microlattice.js

To use Node.js to develop, you need to install the Microlattice package.

### Set up your development environment

If you wish to develop your LinkIt 7687 using node.js, you can use our microlattice.js package.
Follow the following instruction.

#### Prerequisite for Windows developer

**If you are mac developer, you can skip this section.**

For windows developer, please prepare the following:
1. Install [msys2](https://msys2.github.io/).
2. Install [mbed driver](https://developer.mbed.org/handbook/Windows-serial-configuration).
3. Open msys2 and input:
```
update-core
```

4. Install msys2 packages by:
```
pacman -S tar unzip
pacman -S make
pacman -S git
pacman -S wget
```

### Set up Microlattice development environment

1. You must have Node.js (0.10.32 ~ 4.x.x) enviropnment to continue.
    * For Mac/Linux user, use [nvm](https://github.com/creationix/nvm) to install.
    * For Windows user, download the [Node.js](https://nodejs.org/en/) here.
2. Open command line tool and input:
```
npm install microlattice -g
```

3. Create a folder called **testSDK**:
```
mkdir testSDK
```

4. Go to the testSDK folder:
```
cd testSDK
```

5. Create a microlattice project by input:
```
ml create
```

6. Edit **featureConfig.json**:
```
{
"IC_CONFIG": "mt7687",
"BOARD_CONFIG": "mt7687_hdk"
}
```

7. npm install ml-mt7687-config --save
8. ml init:mt7687
9. npm i

### Set up the 7687 project

1. Download the latest LinkIt 7687 [3.3.1 SDK](https://cdn.mediatek.com/download_page/index.html?platform=RTOS&version=v3.3.1&filename=LinkIt_SDK_V3.3.1_public.tar.gz).
2. Put the downloaded **LinkIt_SDK_V3.3.1_public.tar.gz** into the sdk folder in your project.
3. **(Windows only)**Download the [gcc](https://launchpad.net/gcc-arm-embedded/4.8/4.8-2014-q3-update/+download/gcc-arm-none-eabi-4_8-2014q3-20140805-win32.zip) and rename it as **gcc-arm-none-eabi.zip**. Put the **gcc-arm-none-eabi.zip** file into your project sdk folder as well.
4. Copy cache file:
```
cp ./node_modules/ml-mt7687-config/templates/v3.3.1_out.zip ./sdk
```

5. Install the environment:
```
npm run installEnv
```

6. **(Windows only)** Copy the 4 files in sdk folder to **./sdk/tools/gcc/gcc-arm-none-eabi/** folder and cover the original ones. If there is any file conflict, remove the original ones and paste again.
7. **(Windows only)** Go to the **root** folder and input the following:
```
./windows.sh
```


### Launch a Hello World project

1. Edit the **index.js** file and add the followng:
```
print('Hello world!');
```

2. Connect your LinkIt 7687 to your computer.
3. Give the following command:
```
npm run build
```

4. You will see **Hello world!** pops out in a while.
5. Congratulation! You've completed the microlattice development environment set up and you are ready to build your Node.js project in LinkIt 7687.



# Create application on MCS
Here you’ll create a prototype device in MCS and connect it to LinkIt 7687.

## Sign in to MCS console
Click [here](https://mcs.mediatek.com/oauth/en/login) to sign in.



Choose the application you would like to start with:

| [Simple Switch](../tutorial/7688_led_tutorial) | [Analog Controller ](../tutorial/7688_analog_tutorial) | [MD5](../tutorial/7688_gamepad_tutorial)| [FOTA](../tutorial/7688_fota_tutorial)|
| -- | -- | -- | -- |
|[![](../images/Linkit_ONE/img_linkitone_25.png)](../tutorial/7688_led_tutorial)|[![](../images/Linkit_ONE/img_linkitone_26.png)](../tutorial/7688_analog_tutorial)|[![](../images/7688/img_7688_32.png)](../tutorial/7688_gamepad_tutorial)|[![](../images/7688/img_7688_32.png)](../tutorial/7688_gamepad_tutorial)|




