## Release Notes

### 2023.20.1

#### Offline mode
##### Configuration & data usage reduction

Version 2023.20.1 includes an updated offline mode that is configurable. You can disable sending Telemetry data to Tesla(important for FSD Beta users), and the firmware updates don't have to download using the Tesla Android Wi-Fi network.

The ability to check if your car runs the latest Tesla firmware is not affected. 

Kudos to Green and Soma for making this possible!

#### Full-Screen mode
##### Usability improvements

An early fullscreen frontend is now available. You can access it using a new "Go Full-Screen" button in the Flutter App or by navigating to fullscreen.app.teslaandroid.com. 

The Virtual Display still needs to fill the entire window, and there might be some minor UI issues in the Flutter App.

#### Networking
##### Routing improvements

You can access your Tesla Android by typing using app.teslaandroid.com instead of typing the IP address. 

The DHCP server is no longer using a public IP range. Tesla Android switched to a Carrier-grade NAT range.

#### Android Platform
##### Boot time optimization

Version 2023.20.1 takes ~10s less to boot when compared to 2023.18. This was made possible by changing the Wi-Fi network initialisation code.

#### Wi-Fi
##### Performance improvements

Version 2023.20.1 add support for 5GHz Wi-Fi. The new future can be manually enabled in Settings and should improve the network speed significantly. 

Users with their own routers can now disable to Tesla Android Wi-Fi network altogether.

#### Flutter App
##### Stability improvements

Version 2023.20.1 improves the Connectivity Check module. The app is also fully integrated with a self-hosted instance of Sentry(Performance monitoring & Error Tracking). 

The data is anonymised and no fingerprints are captured. Crash logs contain the version of firmware and display resolution. 

---

### 2023.18.2

#### Virtual display
##### Performance improvements

Variable refresh rate mechanism introduced in 2023.18.1 is disabled due to its negative impact on the input latency and animation smoothness.

#### Android Platform
##### Stability improvements

Android has been updated to Android 13 release 43 with the latest security patches.

#### Web server
##### Usability improvements

Cache settings are now less aggressive. You should not need to clear browser data after every Tesla Android update.

---

### 2023.18.1

#### Virtual display
##### Performance improvements

The virtual display is now hardware accelerated via the V4L2 API. As a result, this solution behaves consistently regardless of CPU usage (gaming, video playback). 

The capture mechanism has also been replaced. The new solution sends data to the browser less frequently if nothing is happening on the display. As a result, overall resource usage of the front end is significantly reduced in typical use. 

Internally the refresh rate of the headless operation mode in drm_hwcomposer is now capped at 30Hz. The SufraceFlinger is not able to provide more frames to the virtual display(buffer allocation related).

System animation duration is now reduced to improve performance. 

Virtual display window scaling has been modified to slightly increase text size in system apps; it makes them more easily readable when driving. 

#### Browser audio
##### Usability improvements

Version 2023.18.1 adds the ability to control the sound settings in the Flutter app. The feature can be disabled if you intend to use Bluetooth Audio or other peripherals.

#### Virtual touchscreen
##### Multitouch support

Multitouch support is now available in Tesla Android. The overall stability of the component has been increased.

#### Android Platform
##### Boot time optimization

Version 2023.18.1 takes ~2/3x less time to boot when compared to other Android 13 releases.

#### Android Platform
##### Support for OTA updates

Version 2023.18.1 adds support for OTA updates. A/B (Seamless) mechanism ensures a safe installation with a rollback to the previous build in case of failure. The process takes place in the background; you can use Tesla Android when the update is being installed.

Navigate to Settings -> System -> Updater to check update availability in the future.

Updates are not incremental. You can skip a few versions and update directly to the newest build. 

Only online updates are available in this release; connect your Raspberry Pi to your home router with an Ethernet cable to avoid data charges. Each update weighs around 1 GB.

#### Single image install
##### Usability improvements

The bootloader has been updated to support the single-image install process better. In addition, the filesystem will now expand to take advantage of the entire SD Card on the first boot(similar to how Raspbian behaves). 

Any SD Card over 16GB will work with Tesla Android, but 64GB is recommended. 

The download size has been significantly reduced, and the manual installation procedure has been deprecated and removed from the website. 

#### Bluetooth
##### Usability improvements

Version 2023.18.1 fixes problems with Bluetooth Low Energy. You can now use wireless game controllers, OBD interfaces, and more. Bluetooth Audio stability is also improved.

#### Android Platform
##### Stability improvements

Android has been updated to Android 13 release 41 with the latest security patches. The platform is now in sync with the latest GloDroidCommunity AOSP base. All the board-related changes have been sent upstream, and Tesla Android was migrated to a new build mechanism to make future Android platform updates faster.

#### Flutter App
##### Usability improvements

The has been reorganized to make room for new modules. Tapping the version ribbon takes you to the screen with multiple tabs. One of them is the new Settings module, where you can control the browser audio.

#### Video playback
##### Performance improvements

Version 2023.18.1 adds AV1 decoding via ffmpeg_codec2. The new component takes advantage of multiple cores and performs better.

#### Connectivity
##### Usability improvements

Version 2023.18.1 adds support for Huawei(Brovi) E3372-325. The device is available in the European market.

#### Compute Module 4
##### Hardware improvements

Version 2023.18.1 adds support for the Raspberry Pi Compute Module 4 and was tested with both EMMC(32GB) and SD Card-equipped variants. The external Wi-Fi antenna is selected by default.

#### PWM fan support
##### Hardware improvements

PWM is now enabled on GPIO 18. Supported coolers will only turn on if necessary. You can change the settings in config.txt on the boot partition of the SDCard.

---

### 2023.7.1

#### Android Platform
##### Stability improvements

Android has been updated to Android 13.0.0_r31 with the latest available security patches.

#### H264 hardware acceleration
##### Stability improvements

Version 2023.7.1 improves the stability of the playback and solves issues with artifacts present in the previous version.

#### H265 hardware acceleration
##### Usability improvements

This version adds support for hardware-accelerated H265 video playback via ffmpeg_codec2.
          
#### Software audio decoders
##### Usability improvements
2023.7.1 adds software audio decoders exposed by ffmpeg_codec2 for the following file formats:
- aac  
- ac3  
- alac  
- flac  
- mp2 
- mp3  
- vorbis 

Most of the formats were previously supported by software decoders included with Android. The ffmpeg-powered replacements tend to consume fewer CPU resources.      

#### Software video decoders
##### Usability improvements
2023.7.1 adds software video decoders exposed by ffmpeg_codec2 for the following file formats:
- h263 
- mpeg2 
- mpeg4  
- vp8  
- vp9

Most of the formats were previously supported by software decoders included with Android. The ffmpeg-powered replacements tend to consume fewer CPU resources.   

#### Flutter App
##### Stability improvements
Flutter App received various improvements in this update:
- The framework has been updated to version 3.7.
- Version ribbon has been repositioned to the upper right corner. 
- Reverted changes in touchscreen transport that were introduced in 2023.4.1. The previous implementation was more stable. 
- The reliability of the connectivity checker module was improved by removing the ability to cache static HTML content in Lighttpd. The browser used to cache the health check response for a while after Tesla Android services became unavailable.

#### Audio playback
##### Stability improvements
This version increases the audio playback buffer flush interval from 30 to 100 milliseconds with the hope of decreasing stuttering in cases where the MCU is not able to process the data from WebSocket transport in time.
 
---   

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

Version 2023.18.1 adds support for sharing the internet from iOS devices via USB. Connect your phone, enable tethering and accept the USB access permission request on your iPhone.

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
