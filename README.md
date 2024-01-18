## Rooting Guide for Pixel Devices

<img src="android.png" width="300">

**Disclaimer: Rooting your device may void your warranty and can potentially cause damage. Proceed at your own risk. Make sure to carefully follow the steps and understand the process before proceeding.**

### Prerequisites

- Pixel Device
- PC with USB connectivity
- Type C USB Cable

**Another Disclaimer:
This will wipe all the data off your phone please backup before proceeding.**


### Why Rooting
So recently I bought a Razer Kishi V2 mobile controller for my Pixel. I've been playing games on it but I've been wanting to play some games that are restricted to Nvidia Tegra devices. To get around this I would need to Root my phone so I can bypass this limitaions and install these apps which are not authorized to run on my pixel device which is running a tensor chip. There are a million other reasons to root as well but, I won't get into that.

### Instructions

1. Go to the official Google Android Developers website: [https://developers.google.com/android/images](https://developers.google.com/android/images).

2. Locate the appropriate Factory Image for your specific Pixel device by matching the Build Number in Settings -> About Phone with the Version number on the website. Click on the "Link" button to download the ZIP file.

Optional:
If you want to check if the zip data is not corrupt use my tool to compute the SHA256 Hash and
match it to the one provided by google.
https://github.com/MitchellKopczyk/Hasher

4. Extract the downloaded ZIP file then there should be another zip prefixed with the word "image" extract this.

5. Connect your Pixel device to your PC using the Type C USB cable.

6. Copy the `boot.img` file from the extracted ZIP file to your phone's internal storage.

7. Download Magisk from the official GitHub repository: [https://github.com/topjohnwu/Magisk/releases/tag/v26.1](https://github.com/topjohnwu/Magisk/releases/).

8. Copy the downloaded Magisk APK file to your phone's internal storage.

9. On your Pixel device, use a file manager app (such as the default File app) to locate the Magisk APK file and install it. You may need to enable the installation from unknown sources in the file manager app's settings.

10. Launch the Magisk app on your Pixel device.

11. In the Magisk app, tap install button on the Magisk card.
Then choose "Select and Patch a File" under the "Method" section. Browse and select the `boot.img` file from your phone's internal storage.
Then tap Let's go -> 
The app will patch the file and output the patched file to the "Download" folder on your device this should be logged.

13. Connect your Pixel device to your PC and transfer the patched boot image file to your PC.

14. Enable the "OEM unlocking" and "USB debugging" on your device under System->Developer options

15. Install the ADB and Fastboot binaries on your PC. You can find them from the official Android SDK Platform-Tools: [https://developer.android.com/studio/releases/platform-tools](https://developer.android.com/studio/releases/platform-tools).

```
#Downloading via apt
sudo apt install -y android-tools-adb android-tools-fastboot
#Verify
adb version
fastboot --version
```

15. Make sure you pixel device is connected to your PC using the Type C USB cable.

16. Power off your Pixel device. Press and hold both the Volume Down and Power buttons to boot into the bootloader menu.

17. Open a terminal or command prompt on your PC.

18. In the terminal or command prompt, enter the following command:
    <br/>To check if you device is connected correctly:
    ```
    fastboot devices
    ```
    To unlock type:
    ```
    fastboot flashing unlock
    ```
    Follow the on screen menu to complete the unlocking process. Use the volume buttons and power for navigation. This part wipes your phone.
    Then skip the through the setup wizard to get back to the phone home screen.

19. After unlocking the bootloader again Power off your Pixel device. Press and hold both the Volume Down and Power buttons to boot into the bootloader menu.

20. Use the following command to flash the patched boot image to your device:
    ```
    fastboot flash boot /path/to/patched.img
    ```

21. Wait for the flashing process to complete.

22. Finally, reboot your Pixel device by entering the following command:
    ```
    fastboot reboot
    ```

Congratulations! Your Pixel device is now rooted! If Google pushes a OTA (Over The Air) software update your will have a new boot.img. So, this will have to be patched again. Magisk actually can do this patch for you so you don't need to repeat these steps. You can find more about this online.

Remember, rooting your device has its risks, however it's fairly simple and in general if you follow the steps and understand them you shouldn't really have any issues.

## Downgrading Pixel from Android 14 to 13

**Disclaimer:
This will wipe all the data off your phone please backup before proceeding.**

1. Go to the official Google Android Developers website: [https://developers.google.com/android/images](https://developers.google.com/android/images).

2. Locate the appropriate Factory Image for your specific Pixel device. Click on the "Link" button to download the ZIP file.

3. Extract the downloaded ZIP file

4. Inside the extracted folder you should see a flash-all.sh (shell script) and a flash-all.bat

5. Enable "USB debugging" on your device under System->Developer options.

6. Install the ADB and Fastboot binaries on your PC. You can find them from the official Android SDK Platform-Tools: [https://developer.android.com/studio/releases/platform-tools](https://developer.android.com/studio/releases/platform-tools).

```
#Downloading via apt
sudo apt install -y android-tools-adb android-tools-fastboot
#Verify
adb version
fastboot --version
```

7. Make sure your pixel device is connected to your PC using the Type C USB cable. Power off your Pixel device. Press and hold both the Volume Down and Power buttons to boot into the bootloader menu.
    
8. Open a terminal or command prompt on your PC.

9. Navigate to the directory of the scripts. Then execute your script. I also recommend opening the script in text editor and going through the commands. For Windows use the flash-all.bat script instead.
    ```
    #mac or linux
    sh ./flash-all.sh

    #windows
    fash-all.bat
    ```
    
10. Then wait until the flashing completes. Your phone will reboot into the newly installed system.

**Heads up for rolling back to 12:**

The Android 13 update for Pixel 6, Pixel 6 Pro, and the Pixel 6a contains a bootloader update that increments the anti-roll back version for the bootloader. After flashing an Android 13 build on these devices you will not be able to flash and boot older Android 12 builds.

Method above was tested on my pixel 6a "bluejay" from 14.0.0 (UP1A.231005.007, Oct 2023) to 13.0.0 (TQ3A.230901.001, Sep 2023) 
