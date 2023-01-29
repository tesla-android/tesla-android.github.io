## Release Notes

### 2023.4.2

#### Virtual display
##### Performance improvements

Version 2023.4.1 introduced a new transport layer to the virtual display. Unfortunately, it misbehaved in vehicles with Intel MCU, especially those with the Wi-Fi antenna placed outside the car. This version brings back the transport from 2022.45 and keeps other improvements like the connectivity check module.

#### Audio playback
##### Usability improvements

The previous update introduced volume control in Android. However, default values were around 50%, confusing users. 2022.4.2 resolves this issue and sets the Android system volume to 100%.

#### Flutter App
##### Performance improvements

Version 2023.4.2 brings several improvements in performance to the Flutter app:
- Removed fade-in and fade-out transitions from the audio playback component on each buffer flush. This change makes the volume curve consistent.
- After introducing a workaround for offline PWA support, the rendering engine was changed from HTML to CanvasKit.
- Reduced the amount of ping/pong frames used by the WebSocket transport for the virtual touchscreen

---

### 2023.4.1

#### Android 13
##### Stability improvements

The Android version has been updated to 13, and this change improves the stability of Tesla Android. Security patches have also been merged up to October 2022. The Android base for Raspberry Pi used by Tesla Android(Glodroid Project) has also been updated to the newest release, and it comes packed with improvements around the kernel, display drivers, and much more.

The entire Tesla Android codebase has been refactored in order to make feature Android Platform updates easier; this is an essential step towards making the project more maintainable.

#### H264 hardware acceleration
##### Performance improvements

Version 2022.4.1 adds support for hardware accelerated encoder and decoder for the H264 format. Playback of specific files can contain a small number of artifacts. This is a known issue that will be addressed in the future Tesla Android update. The current implementation of hardware acceleration is based on v4l2_codec2 and will be replaced with an alternative that supports more video formats.

#### Virtual display
##### Stability improvements

The virtual display has been updated to use WebSockets for transport.

#### Virtual touchscreen
##### Stability improvements

This version contains a fix for a problem with not being able to process input data after reloading the Flutter App.

#### Audio playback
##### Stability improvements

The Audio Capture app that used to provide audio from Android to the Browser has been replaced with a new low-level implementation that integrates directly with the Android framework responsible for generating the audio stream before it’s broadcasted to the actual hardware(HDMI, headphone jack, etc.). This new approach brings in a lot of other improvements:
- Increased audio quality (stereo PCM 48kHz - Lossless Audio)
- Support for DRM content (streaming services)
- Support for volume control in Android (available in the Android Settings app)

#### Flutter app
##### Stability improvements

The Flutter App has been refactored to improve stability. Here are some of the changes:
- WebSockets handling for Tesla Android services has been improved.
- Thanks to the new transport layer, the Virtual Display component is now powered by Flutter. This significantly improves stability when compared to the previously used Iframe-based approach.
- The connectivity state observer component has been introduced. The app will notify you when it wouldn’t be able to access Tesla Android services. This change ensures you will not have to manually reload the app when your car returns from sleep or the hardware itself restarts.
- Flutter Framework has been updated to version 3.3.10

#### USB tethering for iOS
##### Connectivity improvements

Version 2023.X.1 adds support for sharing the internet from iOS devices via USB. Connect your phone, enable tethering and accept the USB access permission request on your iPhone.

#### LTE Modem support
##### Connectivity improvements

This update introduces a new Android system service. The Tesla Android USB Networking Initializer simplifies how USB Modems are initialized and allows the use of per-device configuration scripts. This change resolved issues with some variants of Alcatel devices and added support for more Huawei modems.

---

### 2022.45.1

#### Google Apps
##### Usability improvements

Version 2022.45.1 brings back Google Play Store and other Google Services that were removed in 2022.25.1.  Device ID registration for Google Play is not longer required. Not all apps can be installed using Google Play Store due to lack of device certification, they need to be installed manually.

#### Android Platform
##### Stability improvements

Tesla Android system services initialisation has been improved, all components(web server, touchscreen, display etc.) will automatically restart on failure. In previous versions a full system reboot would be needed in this scenario.

#### Virtual display
##### DRM playback

Version 2022.45.1 fixes DRM video playback and enables access to secure layers that are usually blacked out in screen capture. 

#### CarPlay
##### Visual improvements

Three row layout for CarPlay is now selected as default.

#### Virtual touchscreen
##### Stability improvements

Flutter app no longer displays information about virtual touchscreen initialisation, it is irrelevant for the single board stack and should have been removed earlier.

#### Bluetooth
##### Stability improvements

Restarting the system after disabling Bluetooth is no longer required.

#### Internet access
##### USB tethering for Android

USB tethering from Android phones is now supported in Tesla Android. No configuration is required to enable this feature. Your Android phone will be detected as an external ethernet interface when you enable tethering.

#### Internet access
##### LTE modem support

2022.45.1 introduces support for USB network devices using the cdc_ncm driver - it has been validated and works without any additional steps from the user. Experimental changes that might enable support for cdc_mbim and rndis_host drivers are also included. Previous versions supported only the cdc_ether driver. 

#### Internet access
##### Support for external routers

Tesla Android webserver and other services can now be accessed externally using ethernet. This can be used to access the device in your home network or in the car with an external router.

---

### Version 2022.44.2

#### Single Board stack
##### Hardware and setup improvements

Tesla Android does not need the hardware HDMI capture interface anymore. Updated video layer also uses less resources

#### Single system image
##### Setup improvements

Starting with version 2022.44.1 there is a new way to install Tesla Android.
New single image setup process that does not need adb or fastboot. This change requires a 64GB(or larger) SD card.",

#### LTE
##### Fixes for Huawei E3372

Previous release broke support for Huawei E3372. This issue is now resolved.

#### Android platform
##### Boot time improvements

Version 2022.44.1 includes multiple internal optimisations that allow for your Tesla Android to boot up faster after the car wakes from sleep.

#### Virtual display
##### Performance and quality improvements

Virtual display resolution has been increased to enable high fidelity Android experience in your Tesla.
The responsiveness is also improved thanks to internal changes in the video layer.

#### CarPlay
##### Performance improvements

Improvements in the video layer leave more performance for other components.
Decoding video stream from CarPlay is faster in version 2022.44.1.

#### Flutter Frontend
##### Stability improvements

Flutter frameworks has been updated in order to improve user experience.

---

### Version 2022.38.1

#### Single Board stack
##### Hardware and setup improvements

Tesla Android does not need two Raspberry Pi boards anymore!
Version 2022.38.1 is based only on Android.
This marks a significant milestone for the project and greatly lowers the barrier of entry both in terms of cost and ease of setup.

#### Browser Audio
##### Stability and volume improvements

Version 2022.38.1 brings fixes to the browser audio streaming module.
The output volume has been adjusted to match Bluetooth music playback when using CarPlay.
Audio capture service on Android is now a persistent system service that doesn't need to request permissions and automatically restarts on failure.
Bandwidth consumption has been significantly reduced when the music is not playing.

#### Offline Mode
##### Support for the Chinese market and bugfixes

Single board stack includes an updated version of the Offline mode introduced in version 2022.27.1. Connectivity is now handled directly within the Android system, Pi-hole is no longer required.
Thanks to the community input Tesla Android works better in China - version 2022.38.1 includes fixes for connection dropouts due to different API endpoints in this market.

#### Wi-Fi
##### Hotspot improvements

With Tesla Android Single Board you can now manage your Hotspot settings directly in your Tesla.
Updating your network name and credentials is now possible in the Android Settings app.

#### Virtual display
##### Backend improvements and bugfixes

Starting with version 2022.38.1 Tesla Android does not use Ustreamer for video streaming.
Single board stack uses a modified version of mjpg_streamer built with Android NDK.
The new solution is modular and was chosen with bringing direct framebuffer capture to Tesla Android in mind.
Resolution of the virtual display has been updated to match the Tesla Browser viewport introduced with Tesla Version 2022.24.

#### Flutter Frontend
##### Stability improvements

Flutter Frontend has been updated in order to improve user experience.
Framework version has been bumped to 3.3.

---

### Version 2022.27.1

####  Offline Mode
#####  LTE modem is now optional

Starting with version 2022.27.1 the LTE modem is not required for Tesla Android to maintain connection with your car.
Keep in mind that certain online features might not be available in your car as it expects the Wi-Fi network to replace the connectivity provided by Tesla.
When using the Offline Mode turning off Wi-Fi on your touchscreen or powering off Tesla Android is required for accessing your car with the Tesla Mobile App while parked.
Tesla Android can still be used to provide internet to your car like in previous build - no extra configuration changes are required.

####  Wi-Fi
#####  Persistent connection with your Tesla

As a result of introducing the new Offline Mode Wi-Fi stability and connection times have been significantly improved.
If you use the (now optional) LTE modem to get a full Android experience your Wi-Fi with the car won't disconnect when there is no LTE coverage(highways, underground parking etc).

####  Virtual display
#####  Quality improvements

Video stream quality has been slightly improved after reducing the image compression.

####  Flutter Frontend
#####  Stability improvements

Flutter Frontend has been updated in order to improve user experience.
Framework version has been bumped to 3.0.4. Rendering engine has been switched to HTML from CanvasKit due to problems with offline loading in Flutter.

---

### Version 2022.25.1

####  Virtual display
#####  Performance improvements 

Display component has been refactored in order to allow up to 60Hz refresh rate.
Tesla Android will now behave normally when loaded in Drive or Reverse.
Simplification of video stack improves stability of the Flutter application running in the Tesla Browser.

####  Audio Output
#####  Combined audio streams

Audio from Android is routed directly to your Tesla Browser.
Playback is allowed even when Drive or Reverse is engaged, meaning that there is no need to pair Tesla Android with your car using Bluetooth(Bluetooth link with the car is only used by your phone for Android Auto or CarPlay).
Audio output from Tesla Browser does not pause media playback from Tesla OS or CarPlay.
In order to active this feature open Audio Capture app on your Tesla Android after installing the OS. It will automatically launch on each boot later. Audio Capture can be terminated using a button present in the status notification.
Not all apps support audio capture, this restriction will be removed in a feature update.

####  Flutter Frontend
#####  Stability improvements

Flutter Frontend has been updated in order to improve user experience.
Loading times have been improved significantly.
All major components of the app now have proper state management and error handling.

####  Android Platform
#####  Move to Android 12.1

Tesla Android has been migrated to Android 12.1 from AOSP Master in order to improve stability.
Release 2022.25.1 includes Android security updates up to May 5, 2022.

####  Orientation lock
#####  All apps launch in landscape

Tesla Android now includes a working orientation lock for third party apps.
This feature allows phone apps like Apple Music to launch in landscape.

####  Google Play Store
#####  App discoverability

Google Play Store has been replaced with Aurora Store, an Open Source alternative that includes Device Spoofing(emulating Google certification).
Google Play Services have been replaced with microG(Open Source Google Apps).
FDroid(Open Source App Store that does not rely on Google Play Store) is also included.",

####  Video Streaming
#####  DRM support

Tesla Android now supports DRM video playback. Apps like Netflix function normally in version 2022.25.1.

####  CarPlay
#####  Audio/Video improvements

Default resolution of CarPlay is a perfect match for Tesla Android in this release(no content overlapping in audio apps).
Navigation sounds also work, however this feature is active only when Tesla Browser is active.

####  Setup
#####  Simplified device configuration

Setup process of Tesla Android has been simplified, meaning several steps are no longer needed(obtaining a device identifier for Google Services, switching CarPlay resolution etc).

---

#### Version 2022.18.1

Initial release
