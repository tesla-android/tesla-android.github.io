## Install guide (2022.45.1) - Manual method

#### Upgrade from 2022.44.2

If you are currently running version 2022.44.2 you can update by flashing the new Android build onto your Raspberry Pi.

Make sure to clear the browser data in your car if you experience any problems after updating.

#### Note

This install guide has been updated for version 2022.45.1. Older install guides are available below:
- [Install guide (2022.44.2)](/install-guide-2022-44)
- [Install guide (2022.38.1)](/install-guide-2022-38-1)
- [Install guide (2022.27.1)](/install-guide-2022-27-1)
- [Install guide (2022.25.1)](/install-guide-2022-25-1)
- [Install guide (2022.18.1)](/install-guide-2022-18-1)

### Setup steps

1. Begin by downloading and unzipping the newest build of Tesla Android from GitHub - [tesla-android-2022.45.1.zip](https://github.com/tesla-android/android-manifest/releases/download/2022.45.1/tesla-android-2022.45.1.zip)
2. Make sure that both fastboot and adb is installed and accessible from your terminal. Make sure to use a recent version from [https://developer.android.com/studio/releases/platform-tools](https://developer.android.com/studio/releases/platform-tools) if you stumble upon any issues with flashing.
3. Using Balena Etcher or Raspberry Pi Imager flash an image named: "deploy-sd.img" to your SD Card.
4. Insert the SD Card into your Raspberry Pi 4.
5. Connect the Pi to your computer using a USB-C to USB-A/USB-C cable.
#### Note
Make sure that your computer can power your Raspberry Pi using it's USB ports. USB 3.0 ports are known to work without issues.
6. Verify that your computer has detected the Pi by typing: "fastboot devices". Example of a correct output:
<img style="padding: 30px" src="assets/android-setup-fastboot.png">
#### Note
If you are using Windows, to make fastboot find your device you need the Android USB Driver, download it from:  [https://developer.android.com/studio/run/win-usb](https://developer.android.com/studio/run/win-usb)
After you plug your Raspberry Pi on your computers USB port, it will be shown as "USB download gadget" on the Windows Device Manager and the command "fastboot devices" won't find anything.
On the Windows Device Manager, right-click the name of the device ("USB download gadget"), and then select Update Driver Software. In the Hardware Update wizard, select Browse my computer for driver software and click Next. Click Browse and then locate the USB driver folder you just downloaded.
Fastboot should be able to find your Raspberry Pi now.
7. Navigate to a folder that contains an extracted archive with Tesla Android.
8. Execute commands one by one to install Android:
    ```bash
    fastboot flash gpt deploy-gpt.img
    fastboot flash bootloader bootloader-sd.img
    fastboot flash uboot-env  env.img
    fastboot reboot
    
    # Wait for board to power up in bootloader

    fastboot oem format
    fastboot flash bootloader      bootloader-sd.img
    fastboot flash uboot-env       env.img
    fastboot flash boot            boot.img
    fastboot flash vendor_boot     vendor_boot.img
    fastboot flash dtbo_a          boot_dtbo.img
    fastboot erase misc
    fastboot reboot-fastboot

    # Wait for board to power up in fastboot

    fastboot flash super  super.img
    fastboot format:ext4 userdata
    fastboot format:ext4 metadata
    fastboot reboot
    ```

9. Grab yourself something to drink, it will take a while.
10. The Pi will reboot a few times before the setup is finished.
11. You did it, you have successfully installed Android 12L on a Raspberry Pi 4!
12. After booting into Android your Pi will start broadcasting it's own Wi-Fi network. The default password is ``changeit``. You can update it anytime using Android system settings.

You've done it. Deploy it in your Tesla, it's ready :) Place the hardware somewhere near the center console, power using USB ports or a external 12V power supply. After connecting your car to the Wi-Fi make sure to check the: "Remain connected in Drive" checkbox in your Tesla. The URL for the Tesla Android frontend is: ``9.9.0.1``.

#### Upgrade from 2022.44.2

If you are currently running version 2022.44.2 you can update by flashing the new Android build onto your Raspberry Pi.

Make sure to clear the browser data in your car if you experience any problems after updating.