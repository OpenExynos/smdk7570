# SGSWPlatform

SGSWPlatform is an Android-based S/W Platform for smart glasses made by TO21 consortium. This repository contains all essential files for smart glasses. To build the source code and flash the image files, we should follow the below instructions.

## Starting with smart glass board

#### Smart Glass (SG) Keys and Touch
* Peripheral ports and keys

<img width="649" alt="1" src="https://user-images.githubusercontent.com/51391510/59261878-3040df00-8c79-11e9-9fa0-f4f62b6dbcd8.png">

* Touch functions

<img width="649" alt="2" src="https://user-images.githubusercontent.com/51391510/59261881-3040df00-8c79-11e9-9c12-a0b3d0b872cc.png">

#### Providing power sequence
Firstly you should follow the below sequence to provide prober power for SG.
1. Connect battery to SG.
2. Press the Key Power button until the Led turn on.
3. Connect USB cable to SG and PC.
```Note: If you provide the power from the USB port first, after that connect the battery. SG cannot finish booting up.```

#### How to download binary in to Smart Glass board.
All the necessary materials in the SNU FTP server and directory:
> /home/ockwon/Glass/Glass_Tools

1. Install driver Using the **RKDriverAssistant.zip**

<img width="200" alt="3" src="https://user-images.githubusercontent.com/51391510/59261885-3040df00-8c79-11e9-9f47-957c753c2751.png">

2. Turn on the AndroidTool.

<img width="494" alt="4" src="https://user-images.githubusercontent.com/51391510/59261886-30d97580-8c79-11e9-9d3b-b6543ba3f8a2.png">

3. Set SG board to loader mode.

4. Remove battery
    * Connect SG board to PC using USB cable.
    * Press and hold the recovery key.
    * Press the reset key meanwhile the recovery key still holds.
    * Wait about 3 seconds before the releasing the recovery key.
    
5. RKDevTool will detect the LOADER Device as bellow:

<img width="563" alt="5" src="https://user-images.githubusercontent.com/51391510/59261888-30d97580-8c79-11e9-898e-083a0621ea32.png">

6. For the first time you should download all binaries.

7. In the next time you can select which binaries you want to download by click to the check boxes.

#### Using the Total Control application
Total control is useful application to control the android board which did not have the touch screen.

1. Install Total Control in your PC

2. Total control app will automatically detect the android devices.

3. Click connect to connect to android devices.

<img width="255" alt="6" src="https://user-images.githubusercontent.com/51391510/59261889-30d97580-8c79-11e9-9da3-2b904fe2b93a.png">
<img width="439" alt="7" src="https://user-images.githubusercontent.com/51391510/59261890-30d97580-8c79-11e9-8356-287883b9a49d.png">
<img width="439" alt="8" src="https://user-images.githubusercontent.com/51391510/59261891-31720c00-8c79-11e9-9993-88e7486d0431.png">

#### How to get log cat
Using the mlogcat application to catch the logcat of andoird device.
You can download in here: http://mlogcat.tistory.com/

#### How to install android applications
You can using adb command to install android .apk file.
>$: adb install ***.apk

```Note: Because of the total control application also use the adb server. So after you finish installing the application, you should plug out - > plug in again the USB cable in order to make Total control application connect to board again.```
<br>

## How to compile the source code

#### Compile the u-boot
Go to the SDK directory and following the below commands: 
>cd u-boot make
>clean make mrproper
>./make.sh evb-rk3326

Uboot output:
- trust.img
- uboot.img

#### Compile the kernel
Go to the SDK directory and following the below commands: 
> cd kernel
> make distclean
> make ARCH=arm64 rockchip_defconfig

```Note: “make distclean” this command for the first build to clean all object files, the next building you don’t need to use this command```

Kernel output:
- kernel.img
- resource.img

#### Compile the android:
Go to the SDK directory and following the below commands: 
>source build/envsetup.sh
>lunch Chose 7: rk3326_evb-userdebug
>make -j4
>./mkimage.sh

The script “./mkimage.sh” will collect all necessary binaries and parameters (uboot, kernel, filesystems …) in to the directory “rockdev/Image-rk3326_evb”

<img width="476" alt="9" src="https://user-images.githubusercontent.com/51391510/59261892-31720c00-8c79-11e9-9845-062756968a1e.png">


#### How to configuration the UART to get kernel log
Following the bellow parameter to configuration the UART:

<img width="267" alt="10" src="https://user-images.githubusercontent.com/51391510/59261894-31720c00-8c79-11e9-960f-5520091e7582.png">
