## Install guide (2022.38.1)

Version 2022.38.1 is the first release that does not require a secondary Raspberry Pi board running Linux. Given that mostof the software has been either migrated or rewritten from scratch it might take a few builds to improve performance and remove new bugs. Consider trying 2022.27.1 if you are looking for the most consistent performance. 

#### Upgrade from 2022.27.1

If you are currently running version 2022.27.1 you can update by flashing the new Android build onto your primary Raspberry Pi and reconnecting the capture board to it's camera header.

#### Note

This install guide has been updated for version 2022.38.1. Older install guides are available below:
- [Install guide (2022.27.1)](/install-guide-2022-27-1)
- [Install guide (2022.25.1)](/install-guide-2022-25-1)
- [Install guide (2022.18.1)](/install-guide-2022-18-1)

### Setup steps

1. Ensure you have the latest firmware for your raspberry pi by using a separate SD card to load Raspberry Pi OS and [updating the firmware](https://all3dp.com/2/raspberry-pi-4-firmware-update-tutorial/#:~:text=You%20can%20do%20this%20by,your%20Pi's%20software%2C%20firmware%20included).
1. Begin by downloading and unzipping the newest build of Tesla Android from GitHub - [tesla-android-2022.38.1.zip](https://github.com/tesla-android/android-manifest/releases/download/2022.38.1/tesla-android-2022.38.1.zip)
2. Make sure that both fastboot and adb is installed and accessible from your terminal. Make sure to use a recent version from [https://developer.android.com/studio/releases/platform-tools](https://developer.android.com/studio/releases/platform-tools) if you stumble upon any issues with flashing.
3. Using [Raspberry Pi Imager](https://www.raspberrypi.com/software/) flash the image named: `deploy-sd.img` to your SD Card.
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

### Optional steps

#### Audio output

Audio from Android is routed directly to your Tesla Browser.

Playback is allowed even when Drive or Reverse is engaged, meaning that there is no need to pair Tesla Android with your car using Bluetooth(Bluetooth link with the car is only used by your phone for Android Auto or CarPlay).

Audio output from Tesla Browser does not pause media playback from Tesla OS or CarPlay.

Not all apps support audio capture, this restriction will be removed in a feature update.

#### Video streaming

Tesla Android is capable of video streaming, if you want to get smooth playback in a normal resolution I recommended to overclock the Android Pi slightly.

On the boot partition for Android SD card there is a file named config.txt. Add this on the end of it:
```
over_voltage=2
arm_freq=1750
gpu_freq=600
```
Feel free to adjust the preset, this might not be enough if you plan to do some retro console emulation :)

NOTE: Keep in mind that overclocking calls for extra cooling for your Pi. If it starts overheating the performance will be degrated.


#### CarPlay

Tesla Android comes with an app called AutoKit. It enables Apple CarPlay or Android auto using a dongle from Carlinkit (required for both wireless and wired modes). To ensure it works properly apply recommended configuration:
- Set framerate to 30fps or 60fps. Tesla Android uses a 60Hz refresh rate, however 60Hz CarPlay is more power hungry.
- In Advanced Settings section change Audio Channel(Beta) to Bluetooth (That is very important, this option makes it possible to connect your phone directly to the Car. This enables microphone, steering wheel controls, Siri etc).

<img src="assets/carplay-settings.png">

If you find your CarPlay jittery at times apply an overclock to your Android Pi. Android on Raspberry Pi 4 lacks support for hardware accelerated video decoding.

Navigation sounds from CarPlay will be routed via Tesla Browser even when Audio Channel is set to Bluetooth in Autokit. This is a problem with the dongle that has been mitigated by Tesla Android in 2022.25.1. If you can't hear navigation sounds make sure to update the AutoKit app.

### Extras

#### Wi-Fi connectivity after install

If you are not able to connect to Wi-Fi after installing Tesla Android:

1. Leave the board powered on for a few minutes(10, 15) after the first boot (the boot sequence is completed when the Wi-Fi network becomes available)
2. Reboot the board by unplugging the USB-C cable
3. Try again

Please make sure that your Raspberry Pi 4 has current EEPROM(firmware)!

If you can't reach 9.9.0.1 after connecting to the network check the video capture card, the web server won't start when there is a problem with the card.

#### Offline mode

Starting with version 2022.27.1 the LTE modem is not required for Tesla Android to maintain connection with your car.<br>
Keep in mind that certain online features might not be available in your car as it expects the Wi-Fi network to replace the connectivity provided by Tesla.<br>
When using the Offline Mode turning off Wi-Fi on your touchscreen or powering off Tesla Android is required for accessing your car with the Tesla Mobile App while parked.<br>
Tesla Android can still be used to provide internet to your car like in previous build - no extra configuration changes are required.

