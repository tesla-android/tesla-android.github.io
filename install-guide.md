## Install guide (2023.32.1)

### Setup steps

1. Begin by downloading the newest build of Tesla Android from GitHub - [Raspberry Pi 4 releases](https://github.com/tesla-android/android-raspberry-pi/releases). 
2. Extract the downloaded zip file.
3. Using Raspberry Pi Imager flash an image named: "TeslaAndroid-XXXX-rpi4-single-image-installer.img.zip" to your SD Card.
4. Grab yourself something to drink, it will take a while.
5. Insert the SD Card into your Raspberry Pi 4 and power it on.
6. Grab yourself something to drink, it will take a while.
7. After booting into Android your Pi will start broadcasting it's own Wi-Fi network. The default password is ``changeit``. You can update it anytime using Android system settings.
8. You have successfully installed Android 13 on a Raspberry Pi 4!

Deploy it in your Tesla, it's ready :) Place the hardware somewhere near the center console, power using USB ports or a external 12V power supply. After connecting your car to the Wi-Fi make sure to check the: "Remain connected in Drive" checkbox in your Tesla. The URL for the Tesla Android frontend is: ``device.teslaandroid.com``.


#### Notes

1) **New domain used in version 2023.32.1** ``device.teslaandroid.com`` is used instead of ``app.teslaandroid.com``

2) **Make sure to clear the Tesla Browser cache** before connecting to a new version of Tesla Android's web page at ``device.teslaandroid.com``.

3) **Raspberry Pi firmware update might be needed** before installing Tesla Android. Verions 2023.18.1 & newer require that the Raspberry Pi firmware is 2022-04-26 or newer. The updated bootloader is available in Raspberry Pi Imager.<br>

4) **Newer Model 3/Y vehicles provide less power via USB-C ports.**Please switch to a dedicated power supply if you face any issues

5) **Revoke the GPS permission in the browser if you encounter browser crashes**. This is an issue with the Tesla OS that will be hopefully resolved at some point.

### Optional steps

#### Google Play Store

Since Raspberry Pi 4 is not a certified Android device some apps might not be available in the Play Store. You can install them manually using sites like APK Mirror.

#### Audio output

Audio from Android is routed directly to your Tesla Browser.

Playback is allowed even when Drive or Reverse is engaged, meaning that there is no need to pair Tesla Android with your car using Bluetooth(Bluetooth link with the car is only used by your phone for Android Auto or CarPlay).

Audio output from Tesla Browser does not pause media playback from Tesla OS or CarPlay.

#### CarPlay

Tesla Android comes with an app called AutoKit. It enables Apple CarPlay or Android auto using a dongle from Carlinkit (required for both wireless and wired modes). To ensure it works properly apply recommended configuration:
- In Advanced Settings section change Audio Channel(Beta) to Bluetooth (That is very important, this option makes it possible to connect your phone directly to the Car. This enables microphone, steering wheel controls, Siri etc).

<img src="assets/carplay-settings.png">

### Extras

#### Over-the-air updates

OTA updates are supported on versions newer than 2023.18. <br>
To check for updates navigate to Settings->System->Updater.

#### Offline mode

Starting with version 2022.27.1 the LTE modem is not required for Tesla Android to maintain connection with your car.<br>
Keep in mind that certain online features might not be available in your car as it expects the Wi-Fi network to replace the connectivity provided by Tesla.<br>
When using the Offline Mode turning off Wi-Fi on your touchscreen or powering off Tesla Android is required for accessing your car with the Tesla Mobile App while parked.<br>
Tesla Android can still be used to provide internet to your car like in previous build - no extra configuration changes are required.

#### Wi-Fi performance

Version 2023.20.1 add support for 5GHz Wi-Fi. 2023.32.1 makes 5GHz the new default for fresh installs. Make sure to update your settings if needed.
