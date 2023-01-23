## Install guide (2023.4.1.1) - Single image method

#### Manual install

If your SD Card is not at least 64GB you can perform a [manual install](/install-guide-full). Please note that smaller cards will not be supported in newer builds that will add support OTA updates.

#### Upgrade from 2022.45.1

If you are currently running version 2022.45.1 you can update by flashing the new Android build onto your Raspberry Pi.

Make sure to clear the browser data in your car if you experience any problems after updating.

#### Note

This install guide has been updated for version 2023.4.1. Older install guides are available below:
- [Install guide (2022.44.2)](/install-guide-2022-45-1)
- [Install guide (2022.44.2)](/install-guide-2022-44)
- [Install guide (2022.38.1)](/install-guide-2022-38-1)
- [Install guide (2022.27.1)](/install-guide-2022-27-1)
- [Install guide (2022.25.1)](/install-guide-2022-25-1)
- [Install guide (2022.18.1)](/install-guide-2022-18-1)

### Setup steps

1. Begin by downloading the newest build of Tesla Android from GitHub - [tesla-android-2023.4.1.1-single-image.img.zip](https://github.com/tesla-android/android-manifest/releases/download/2023.4.1.1/tesla-android-2023.4.1.1-single-image.zip)
2. Extract the downloaded zip file. The image is about 30 GB large (this will be reduced in a future update).
3. Using Raspberry Pi Imager flash an image named: "tesla-android-2022.45.1-single-image.img" to your SD Card.
4. Grab yourself something to drink, it will take a while.
5. Insert the SD Card into your Raspberry Pi 4 and power it on.
6. Grab yourself something to drink, it will take a while.
7. After booting into Android your Pi will start broadcasting it's own Wi-Fi network. The default password is ``changeit``. You can update it anytime using Android system settings.
8. You did it, you have successfully installed Android 13 on a Raspberry Pi 4!

You've done it. Deploy it in your Tesla, it's ready :) Place the hardware somewhere near the center console, power using USB ports or a external 12V power supply. After connecting your car to the Wi-Fi make sure to check the: "Remain connected in Drive" checkbox in your Tesla. The URL for the Tesla Android frontend is: ``9.9.0.1``.

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

#### Offline mode

Starting with version 2022.27.1 the LTE modem is not required for Tesla Android to maintain connection with your car.<br>
Keep in mind that certain online features might not be available in your car as it expects the Wi-Fi network to replace the connectivity provided by Tesla.<br>
When using the Offline Mode turning off Wi-Fi on your touchscreen or powering off Tesla Android is required for accessing your car with the Tesla Mobile App while parked.<br>
Tesla Android can still be used to provide internet to your car like in previous build - no extra configuration changes are required.

