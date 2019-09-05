## Release 2.28.0
Release Date: 5 Sep 2019

### API Changes
[Link](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2280)

### New Features & Improvements
* [#4786](https://github.com/IntelRealSense/librealsense/pull/4786) - [Realsense-Viewer] Set Decimation off by default for 
RGB streams (DSO-13570)
* [#4746](https://github.com/IntelRealSense/librealsense/pull/4746) - [Realsense-Viewer] Adding option to use Pre-Release firmware for D400 devices.
* [#4749](https://github.com/IntelRealSense/librealsense/pull/4749) - [Python] Code refactoring, minor fixes

### Bug Fixes
* [#4788](https://github.com/IntelRealSense/librealsense/pull/4788) - Fix Frame Validation (RS5-5244)
* [#4787](https://github.com/IntelRealSense/librealsense/pull/4787) - Fix Jupyter Notebook. #4142, #4579
* [#4785](https://github.com/IntelRealSense/librealsense/pull/4785) - Fix a potential out-of-order initialization for A-factor (DSO-13560)
* [#4774](https://github.com/IntelRealSense/librealsense/pull/4774) - [Kernel Patches] Adjust Ubuntu LTS track branches for kernel sources
* [#4772](https://github.com/IntelRealSense/librealsense/pull/4772) - [Realsense-Viewer] Fixing basic threading issues within on-chip calibration UI.
* [#4759](https://github.com/IntelRealSense/librealsense/pull/4759) - MSVC2019 compilation fix by @UnaNancyOwen
* [#4758](https://github.com/IntelRealSense/librealsense/pull/4758) - Fix deadlock on pipeline.stop() with playback device in realtime=false mode
* [#4752](https://github.com/IntelRealSense/librealsense/pull/4752) - [Android] Streaming got stuck with camera APP (DSO-13453)


### Known Issues
* Firmware Update - owners of SR300 device shall not use firmware versions v3.27.xx as it overrides camera's product id (PID) and may render it non-recognizable with the client's code, especially with the legacy versions.
A new compatibility enforcement policy that shall prevents accidental upgrades will be integrated in future releases.
* Firmware Update with `rs-fw-update` tool. The firmware update process may fail when additional librealsense application runs in background. Make sure to close any librealsense-based application during the Firmware Update routine (DSO-13078)
* Firmware Update on Linux - backup procedure may takes up to two minutes (DSO-13072)
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized value(s)
* Global Timestamp: first 15 seconds of frames timestamps are unstable (DSO-12942)
* IMU jitter and drops events [LRS] regression (DSO-12940)
* (DSO-13541) - On-Chip Calibration stuck at 0% when in USB2 mode
* (DSO-13540) - On-Chip Calibration with D415 and blank wall target may return "Calibration didn't converge! (EDGE_TO_CLOSE) please retry in different lighting conditions". (Note: w/a is using textured target)
* (DSO-13539) - [Android] Camera disconnected after streaming some duration with Android Camera Sample
* (DSO-13525) - 3D viewer moved when sliding the tare calibration sliders
* (DSO-13524) - Viewer crash when running Update Unsigned FW with signed FW image (unlocked units only)

## Release 2.27.0
Release Date: 29 Aug 2019

### API Changes
[link](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2270)

### New Features & Improvements

* **T265 Calibration APIs**:
  * [#4650](https://github.com/IntelRealSense/librealsense/pull/4650) - write calibration APIs
  * [#4717](https://github.com/IntelRealSense/librealsense/pull/4717) - updating default T265 firmware to 0.1.0.279
     * Expose the ability to modify the T265 calibration (w/ #4650)
     * T265 tracking performance improvement
     * Fixes #4700 T265 load/start/stop/load/start failure
  * [#4739](https://github.com/IntelRealSense/librealsense/pull/4739) and [#4685](https://github.com/IntelRealSense/librealsense/pull/4685) - documentation enhancements
* **New OpenCV example** - [#4733](https://github.com/IntelRealSense/librealsense/pull/4733) (Implementing ["Depth Map Improvements for Stereo-based
Depth Cameras on Drones"](http://www.qwrt.de/pdf/Depth_Map_Improvements_for_Stereo_based_Depth_Cameras_on_Drones.pdf))
* [#4721](https://github.com/IntelRealSense/librealsense/pull/4721) - Fix format-security warnings (contributed by [@morxa](https://github.com/morxa))
* [#4706](https://github.com/IntelRealSense/librealsense/pull/4706) - [Viewer] Enable step forward and backward during playback

### Bug Fixes
* **On-Chip Calibration** enhancements ([#4735](https://github.com/IntelRealSense/librealsense/pull/4735)) - 
  * Integration with firmware 5.11.14 (pre-release)
  * Unlocking the feature for D435i (DSO-13538)
  * Fixing Tare calibration units (DSO-13537)
* [#4731](https://github.com/IntelRealSense/librealsense/pull/4731) - Fixing Java example (addressing issues [#4701](https://github.com/IntelRealSense/librealsense/issues/4701) and [#4693](https://github.com/IntelRealSense/librealsense/issues/4693))
* [#4729](https://github.com/IntelRealSense/librealsense/pull/4729) - Fix Ubuntu 32bit compilation (addressing [#3448](https://github.com/IntelRealSense/librealsense/issues/3448) / DSO-12283)
* [#4698](https://github.com/IntelRealSense/librealsense/pull/4698) - [Android] GLFrame resource release (addressing DSO-13120)

### Known Issues
* Firmware Update - owners of SR300 device shall not use firmware versions v3.27.xx as it overrides camera's product id (PID) and may render it non-recognizable with the client's code, especially with the legacy versions.
A new compatibility enforcement policy that shall prevents accidental upgrades will be integrated in future releases.
* Firmware Update with `rs-fw-update` tool. The firmware update process may fail when additional librealsense application runs in background. Make sure to close any librealsense-based application during the Firmware Update routine (DSO-13078)
* Firmware Update on Linux - backup procedure may takes up to two minutes (DSO-13072)
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized value(s)
* Global Timestamp: first 15 seconds of frames timestamps are unstable (DSO-12942)
* IMU jitter and drops events [LRS] regression (DSO-12940)
* (DSO-13541) - On-Chip Calibration stuck at 0% when in USB2 mode
* (DSO-13540) - On-Chip Calibration with D415 and blank wall target may return "Calibration didn't converge! (EDGE_TO_CLOSE) please retry in different lighting conditions". (Note: w/a is using textured target)
* (DSO-13539) - [Android] Camera disconnected after streaming some duration with Android Camera Sample
* (DSO-13525) - 3D viewer moved when sliding the tare calibration sliders
* (DSO-13524) - Viewer crash when running Update Unsigned FW with signed FW image (unlocked units only)

## Release 2.26.0
Release Date: 21 Aug 2019

### API Changes
[link](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2260)

### New Features & Improvements

* [#4658](https://github.com/IntelRealSense/librealsense/pull/4658) - D400 On-Chip Auto-calibration. Allows to recalibrate and therefore, improve depth quality using SDK-provided tools : `realsense-viewer` and `rs-depth-quality`. Note that this capability relies on FW version 5.13.x+ which is not yet publicly available at this stage. Follow the above link for more details.
* [#4605](https://github.com/IntelRealSense/librealsense/pull/4605) - Cross platform IMU HID device. This PR brings a cross platform HID device (IMU), implemented above rsusb interface.
435i IMU streaming is now enabled on Android platform. It is also available on non-X86 platforms, such as Arm with libuvc backend (e.g. Jetson TX2 amd Nano). (DSO-11944)
* [#4433](https://github.com/IntelRealSense/librealsense/pull/4433) - Add support for Firmware Update using non-signed images
* [#4492](https://github.com/IntelRealSense/librealsense/pull/4492) - Python: an Ethernet client-server example code for Realsense devices. Requires python 2.7.

### Enhancements

* [#4677](https://github.com/IntelRealSense/librealsense/pull/4677) - Pointcloud 3D-view in Android. Addresses [#4601](https://github.com/IntelRealSense/librealsense/issues/4601)
* [#4673](https://github.com/IntelRealSense/librealsense/pull/4673) - T265 Firmware Upgrade to version 0.1.0.242 to improve start and stop reliability, and overall stability, can have a positive effect on [#4592](https://github.com/IntelRealSense/librealsense/issues/4592), [#4518](https://github.com/IntelRealSense/librealsense/issues/4518).
* [#4666](https://github.com/IntelRealSense/librealsense/pull/4666) - Synchronize wrappers options with the core SDK. (matlab, node.js, python) [#4288](https://github.com/IntelRealSense/librealsense/issues/4288)
* [#4645](https://github.com/IntelRealSense/librealsense/pull/4645) - T265: auxillary function to print out motion intrinsic data
* [#4638](https://github.com/IntelRealSense/librealsense/pull/4645) - T265 Documentation: fix python examples link
* [#4622](https://github.com/IntelRealSense/librealsense/pull/4622) - Support for MJPEG stream for selected SKUs.
* [#4620](https://github.com/IntelRealSense/librealsense/pull/4620) - Community Project: realsense with cyber update, by @mickeyouyou
* [#4618](https://github.com/IntelRealSense/librealsense/pull/4618) - Windows7 : Drivers update to include support for the new and provisional model types, DFU mode. Digital certificate update as of Aug 2019.
* [#4602](https://github.com/IntelRealSense/librealsense/pull/4602)  - T265: Increase internal queue size to mitigate frame drops
* [#4583](https://github.com/IntelRealSense/librealsense/pull/4583)  - Android: SR300 firmware update improvements. (DSO-13360)
* [#4587](https://github.com/IntelRealSense/librealsense/pull/4587)  - D400: fix IMU data rate configuration. (DSO-13325)
* [#4582](https://github.com/IntelRealSense/librealsense/pull/4582)  - CMake enhancement, addresses [#3024](https://github.com/IntelRealSense/librealsense/issues/3024)
* [#4546](https://github.com/IntelRealSense/librealsense/pull/4546) - Python: Add syncer support for sensor start method. (DSO-13062)
* [#4545](https://github.com/IntelRealSense/librealsense/pull/4545) - `rs-enumerate-devices` robustness enhancement
* [#4537](https://github.com/IntelRealSense/librealsense/pull/4537) - Conform to ROS name convention. [#1161](https://github.com/IntelRealSense/librealsense/issues/1161)
* [#4248](https://github.com/IntelRealSense/librealsense/pull/4248) - Windows7 stability fixes and enhancements

### Bug Fixes
* [#4678](https://github.com/IntelRealSense/librealsense/pull/4678) - Fix Out-of-Memory error - Android UVC. Addresses [#3612](https://github.com/IntelRealSense/librealsense/issues/3612), [#4091](https://github.com/IntelRealSense/librealsense/issues/4091), [#4215](https://github.com/IntelRealSense/librealsense/issues/4215)
* [#4631](https://github.com/IntelRealSense/librealsense/pull/4631) - Fix default stream index for synthetic stream
* [#4616](https://github.com/IntelRealSense/librealsense/pull/4616) - Fix matlab method syntax in points.m by @dpiskas
dpiskas
* [#4596](https://github.com/IntelRealSense/librealsense/pull/4596) - Fix memory leak in `rs-multi-cam` example
* [#4562](https://github.com/IntelRealSense/librealsense/pull/4562) - DQT: fix plane and metric annotations when stream is paused. (RS5-3386)
* [#4561](https://github.com/IntelRealSense/librealsense/pull/4561) - CMake: fix offline build with no FW image available
* [#4560](https://github.com/IntelRealSense/librealsense/pull/4560) - Viewer - fix unresponsive UI on errors. (DSO-13146)
* [#4535](https://github.com/IntelRealSense/librealsense/pull/4535) - Remove "Depth Visualization" tab under unrelated sensors in viewer. (DSO-12361)
* [#4531](https://github.com/IntelRealSense/librealsense/pull/4531) - Use full GPG Key IDs for installing in linux by @miguelprada
* [#4507](https://github.com/IntelRealSense/librealsense/pull/4507) - T265: Use the origin of the Pose frame as the baseline for sensor extrinsic


### Known Issues
* Firmware Update - owners of SR300 device shall not use firmware versions v3.27.xx as it overrides camera's product id (PID) and may render it non-recognizable with the client's code, especially with the legacy versions.
A new compatibility enforcement policy that shall prevents accidental upgrades will be integrated in future releases.
* Firmware Update with `rs-fw-update` tool. The firmware update process may fail when additional librealsense application runs in background. Make sure to close any librealsense-based application during the Firmware Update routine (DSO-13078)
* Firmware Update on Linux - backup procedure may takes up to two minutes (DSO-13072)
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets #3781.(DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized value(s)
* Global Timestamp: first 15 seconds of frames timestamps are unstable (DSO-12942)
* IMU jitter and drops events [LRS] regression (DSO-12940)


## Release 2.25.0
Release Date: 1 Aug 2019

### API Changes
[link](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2250)

### New Features & Improvements

* [#4340](https://github.com/IntelRealSense/librealsense/pull/4340) - T265 Demo with Apriltag detection on host
* [#4327](https://github.com/IntelRealSense/librealsense/pull/4327) - T265 Tracking + Depth Example


Enhancements
* [#4544](https://github.com/IntelRealSense/librealsense/pull/4544) - RGB Distortion correction for the supported sensors types (DSO-8307) linked to [IntelRealSense/realsense-ros#779](https://github.com/IntelRealSense/realsense-ros/issues/779)
* [#4321](https://github.com/IntelRealSense/librealsense/pull/4321) - T265 Mapping/Relocalization/Jumping Options
* [#4511](https://github.com/IntelRealSense/librealsense/pull/4511) - T265 advanced options to the python wrapper:
`enable_mapping`, `enable_pose_jumping`, and `enable_relocalization`. Follow up on [#4321](https://github.com/IntelRealSense/librealsense/pull/4321)
* [#4478](https://github.com/IntelRealSense/librealsense/pull/4478) - Support new calibration command `RECPARAMSGET` for D400 series
* [#4472](https://github.com/IntelRealSense/librealsense/pull/4472) - RGB Auto-Exposure ROI control for SR300
* [#4448](https://github.com/IntelRealSense/librealsense/pull/4448) - T265 expose Frame timestamp metadata attribute
* [#4403](https://github.com/IntelRealSense/librealsense/pull/4403) - T265 to support GLOBAL_TIMESTAMP_DOMAIN (TM2-4496)
* [#4402](https://github.com/IntelRealSense/librealsense/pull/4402) - Update for `realsense_device_manager.py` example by 
@NicholasWon47
* [#4389](https://github.com/IntelRealSense/librealsense/pull/4389) - IMU Support for D465.
* [#4380](https://github.com/IntelRealSense/librealsense/pull/4380) - Update SR300 recommended fW version to 2.26.1.0
* [#4367](https://github.com/IntelRealSense/librealsense/pull/4367) - Update 3rd-party `update stb_image_write.h` to v1.13 by @sailfish009
* [#4365](https://github.com/IntelRealSense/librealsense/pull/4365) - Remove the default 2Mb limit for log file generation (RS5-4780)
* [#4358](https://github.com/IntelRealSense/librealsense/pull/4358) - Silence OpenGL deprecation warnings on MacOS 10.14
* [#4314](https://github.com/IntelRealSense/librealsense/pull/4314) - Firmware Update robustness enhancement


### Bug Fixes
* [#4377](https://github.com/IntelRealSense/librealsense/pull/4377) - OpenCV Kinfu example dependency fix by @peterhinson
* [#4360](https://github.com/IntelRealSense/librealsense/pull/4360) - Fix for udev-rules validation routine (RS5-4780) addresses #4350
* [#4329](https://github.com/IntelRealSense/librealsense/pull/4329) - Easy-logging bug fix
* [#4313](https://github.com/IntelRealSense/librealsense/pull/4313) - Fix python readme by @kechako
* Firmware Update on Windows with Realsense-Viewer halts at  (30-50)% progress. Troubleshoot this by disconnecting and reconnecting the camera, then rerun Firmware update process (DSO-13070)

### Known Issues
* Firmware Update with `rs-fw-update` tool. The firmware update process may fail when additional librealsense application runs in background. Make sure to close any librealsense-based application during the Firmware Update routine (DSO-13078)
* Firmware Update on Linux - backup procedure may takes up to two minutes (DSO-13072)
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets #3781.(DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized value(s)
* Global Timestamp: first 15 seconds of frames timestamps are unstable (DSO-12942)
* IMU jitter and drops events [LRS] regression (DSO-12940)



## Release 2.24.0
Release Date: 27 Jun 2019

### API Changes
[link](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2240)

### New Features & Improvements
Streamlining Firmware Update for D400 and SR300 Depth Cameras:
A new Cross-platform firmware update capability has been introduced to facilitate the camera maintenance.  
Platforms supported: Windows(*), Linux, Android, MacOS. *Before updating device please review errata below.  
The capability is integrated into `realsense-viewer` and a stand-alone `rs-fw-update` tools.
For more info see
* [#4267](https://github.com/IntelRealSense/librealsense/pull/4267) - Firmware Update Capability and `rs-fw-update` tool
* [#4280](https://github.com/IntelRealSense/librealsense/pull/4280) - Firmware Update integration with Viewer
* [#4304](https://github.com/IntelRealSense/librealsense/pull/4304) - Firmware Update in Android camera app

Enhancements
* [#4265](https://github.com/IntelRealSense/librealsense/pull/4265) - Adding Ubuntu Kernel 4.18 support. Non-LTS Kernel 5.0 is also supported with manual installation.
* [#4240](https://github.com/IntelRealSense/librealsense/pull/4240) - Contradictory Camera Axis Labels for T265 #4226
* [#4237](https://github.com/IntelRealSense/librealsense/pull/4237) - Android - dynamic USB read buffer size #3612, #4091, #4215
* [#4203](https://github.com/IntelRealSense/librealsense/pull/4203) - Nodejs support for windows build. Documentation update

### Bug Fixes
* [#4268](https://github.com/IntelRealSense/librealsense/pull/4268) - Viewer - fix variables name #4157
* [#4264](https://github.com/IntelRealSense/librealsense/pull/4264) - Fix Kernel 4.19+ error #2850 (DSO-11696)
* [#4251](https://github.com/IntelRealSense/librealsense/pull/51) -  `rs-terminal` improperly selects target in case of multiple devices connected
* [#4246](https://github.com/IntelRealSense/librealsense/pull/4246) - Linux file descriptors are not released when device is plugged off. Can be related to #3538 (DSO-12768)
* [#4219](https://github.com/IntelRealSense/librealsense/pull/4219) - Android l500 detection issue
* [#4208](https://github.com/IntelRealSense/librealsense/pull/4208) - Matlab and Python wrappers updates. Fixes  #4034, #4146.

### Known Issues
* Firmware Update on Windows with Realsense-Viewer halts at  (30-50)% progress. Troubleshoot this by disconnecting and reconnecting the camera, then rerun Firmware update process (DSO-13070)
* Firmware Update with `rs-fw-update` tool. The firmware update process may fail when additional librealsense application runs in background. Make sure to close any librealsense-based application during the Firmware Update routine (DSO-13078)
* Firmware Update on Linux - backup procedure may takes up to two minutes (DSO-13072)
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets #3781.(DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized value(s)
* Global Timestamp: first 15 seconds of frames timestamps are unstable (DSO-12942)
* IMU jitter and drops events [LRS] regression (DSO-12940)


## Release 2.23.0
Release Date: 10 Jun 2019

### API Changes
[link](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2230)

### New Features & Improvements
* [#3998](https://github.com/IntelRealSense/librealsense/pull/3998) - Add comprehensive documentation to Python via sphinx - published via `intelrealsense.github.io`[link](https://intelrealsense.github.io/librealsense/python_docs/_generated/pyrealsense2.html#module-pyrealsense2)
* [#4100](https://github.com/IntelRealSense/librealsense/pull/4100),[#4162](https://github.com/IntelRealSense/librealsense/pull/4162) - Depth linearity enhancement - Mitigate the half-pixel disparity issue by adjusting the modulation amplitude. `rs2_set_amp_factor/rs2_get_amp_factor` Advanced-mode parameters functions. Requires FW version 5.11.9+ (DSO-12737)
* [#3992](https://github.com/IntelRealSense/librealsense/pull/3992) - T265: Expose the Fisheye sensor manual exposure control.
* [#4135](https://github.com/IntelRealSense/librealsense/pull/4135) - Propagating IMU HW timestamp via metadata API. Allows to retrieve IMU HW timestamp via the metadata API. Also add support for IMU metadata backend timestamps (DSO-12860).
* [#4159](https://github.com/IntelRealSense/librealsense/pull/4159) - Retrofitting metadata quirks into the linux kerenel patches for additional SKUs.
* [#4012](https://github.com/IntelRealSense/librealsense/pull/4012) - Add python 3.7 support (by @ClimbsRocks)
* [#4133](https://github.com/IntelRealSense/librealsense/pull/4133) - Documentation enhancement (by @VasuAgrawal)
* [#4094](https://github.com/IntelRealSense/librealsense/pull/4094) - CMake improvements 
* [#4122](https://github.com/IntelRealSense/librealsense/pull/4122), [#4152](https://github.com/IntelRealSense/librealsense/pull/4152) - T265: Quiet Static Nodes
* [#4078](https://github.com/IntelRealSense/librealsense/pull/4078) - Add support for D4xx SKUs (DSO-12649).
* [#4149](https://github.com/IntelRealSense/librealsense/pull/4149), [#4119](https://github.com/IntelRealSense/librealsense/pull/4119) - SKU enhancements

### Bug Fixes
* [#4160](https://github.com/IntelRealSense/librealsense/pull/4160) - Revisited and updated RGB extrinsic calibration recovery routine that applies to D435i that underwent upgrade to v5.11.6.200. The changes are transparent to the end user.
Addresses #3788, #3949, #4050. (DSO-12820, DSO-12623)
* [#4117](https://github.com/IntelRealSense/librealsense/pull/4117) - Android examples fix with `config` object 
* [#4093](https://github.com/IntelRealSense/librealsense/pull/4093) - Linux: Restore OpenMP support #4023 
* [#4073](https://github.com/IntelRealSense/librealsense/pull/4073) - Fix GlobalTimer prevents enter power-saving mode (DSO-12794).
* [#4032](https://github.com/IntelRealSense/librealsense/pull/4032) - Fix Android error handling flow.
* [#4029](https://github.com/IntelRealSense/librealsense/pull/4029) - Fix RGB calibration recovery exceptions handling (DSO-12789)
* [#4013](https://github.com/IntelRealSense/librealsense/pull/4013) - T265: Improve precision tolerance of Quaternion<=>Rotation transformation to remain within 6% off the norm.
* [#4000](https://github.com/IntelRealSense/librealsense/pull/4000) - T265: Fix t265_rpy.py demo.

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets #3781.(DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* [#2850](https://github.com/IntelRealSense/librealsense/issues/2850) / DSO-11696 - Linux Kernel 4.19 support
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized value(s)
* Global Timestamp: first 15 seconds of frames timestamps are unstable (DSO-12942)
* IMU jitter and drops events [LRS] regression (DSO-12940)

## Release 2.22.0
Release Date: 20 May 2019

### API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2220)

### New Features & Improvements
* [#3909](https://github.com/IntelRealSense/librealsense/pull/3909) - introducing Global Camera Timestamp. The feature is a prerequisite for inter-cam synchronization and requires frame metadata attributes.
 The PR changes the default behavior of `frame.get_timestamp()` by returning the timestamp in `RS2_TIMESTAMP_DOMAIN_GLOBAL_TIME`. Follow the PR link for more details. Addresses #2922, #2188  (RS-3975). 
* [#3654](https://github.com/IntelRealSense/librealsense/pull/3654) - New Module - GLSL Processing Blocks.
This pull-request introduces auxiliary realsense2-gl module. It can be used to perform common SDK processing tasks on the GPU in a relatively generic way (vendor neutral, unlike CUDA) via GLSL shaders.
In addition, it serves as a proof-of-concept for future SDK extensions beyond core API.(Follow the PR link for in-depth introduction)
* [#3828](https://github.com/IntelRealSense/librealsense/pull/3828) - Adding common cross-platform USB back-end API. Initially, it will be used for cross-platform FW update API and tools(DSO-10947).
In the future the infrastructure will allow unified implementation for UVC/HID/TM2 for all the supported operating systems.
* [#3907](https://github.com/IntelRealSense/librealsense/pull/3907) - Promote TM2 Firmware 0.0.18.5715 - re-localization and tracking stability enhancements
* [#3882](https://github.com/IntelRealSense/librealsense/pull/3882) - T265: Re-enabling re-localization reports.
* [#3869](https://github.com/IntelRealSense/librealsense/pull/3869) - Android OS (Java): Add post-processing filters and demo.
* [#3930](https://github.com/IntelRealSense/librealsense/pull/3930) - Add `realsense2-gl` Debian distribution packages to support PR3654.
* [#3933](https://github.com/IntelRealSense/librealsense/pull/3933) - Adding `rs2_get_frame_sensor` function (DSO-12656)
* [#3951](https://github.com/IntelRealSense/librealsense/pull/3951) - New T265 Example: Generate Depth map from T265 Stereo sensors with OpenCv.
* [#3982](https://github.com/IntelRealSense/librealsense/pull/3982) - Add a processing block to generate depth frame in metric format (RS5-4269)
* [#3993](https://github.com/IntelRealSense/librealsense/pull/3993) - Add comprehensive documentation to Python wrapper via Sphinx.
* [#3956](https://github.com/IntelRealSense/librealsense/pull/3956) - Unreal Engine 4 wrapper supports v4.22.
* [#3972](https://github.com/IntelRealSense/librealsense/pull/3972) - Adding `software_device` support to C# wrapper.
* [#3820](https://github.com/IntelRealSense/librealsense/pull/3820) - RealSense depth viewer community example
* [#3860](https://github.com/IntelRealSense/librealsense/pull/3860) - Python Documentation - sample code enhancement
* [#3826](https://github.com/IntelRealSense/librealsense/pull/3826) - C#: Expose T265-specific APIs (Localization map, Static node).
* [#3883](https://github.com/IntelRealSense/librealsense/pull/3883) - OpenCv: Fix missing `RS2_FORMAT_DISPARITY32` handler.

### Bug Fixes
* [#3884](https://github.com/IntelRealSense/librealsense/pull/3884) - T265: Pose record/playback to provide the required metadata attributes; Enable `rs-enumerate-devices` extract info from ROSBag record files. Addresses #3837 (TM2-4344)
* [#3976](https://github.com/IntelRealSense/librealsense/pull/3976) - D435i: Rectify invalid RGB-Depth extrinsic calibration produced by FW versions 5.10.13+. Addresses #3474, #3788, #3201(DSO-12623)
* [#3900](https://github.com/IntelRealSense/librealsense/pull/3900) - Fix extrinsic graph multiplications order.
* [#3901](https://github.com/IntelRealSense/librealsense/pull/3901) - Fix D435i IMU extrinsic
* [#3971](https://github.com/IntelRealSense/librealsense/pull/3971) - T265 FW: Fix potential issue with UNC paths and rc.exe.

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets #3781.(DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* [#2850](https://github.com/IntelRealSense/librealsense/issues/2850) / DSO-11696 - Linux Kernel 4.19 support
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialised value(s)



## Release 2.21.0
Release Date: 22 April 2019

### API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2200-to-2210) from 2.20.x versions

### New Features & Improvements
* [#3778](https://github.com/IntelRealSense/librealsense/pull/3778) - T265 Firmware update to 0.0.18.5502 - re-localization and tracking stability enhancements
* [#3775](https://github.com/IntelRealSense/librealsense/pull/3775) - T265 Wheel Odometer documentation updated.
* [#3771](https://github.com/IntelRealSense/librealsense/pull/3771) - Android OS - add Visual Presets support. (DSO-12447)
* [#3739](https://github.com/IntelRealSense/librealsense/pull/3739) - Python wrapper performance enhancement - release GIL during invocation of polling routines (DSO-12493)
* [#3736](https://github.com/IntelRealSense/librealsense/pull/3736) - T265: Disable low power default mode.
* [#3729](https://github.com/IntelRealSense/librealsense/pull/3729) - Streamline Linux installation instructions.  (contributed by [@pedrombmachado](https://github.com/pedrombmachado))
* [#3647](https://github.com/IntelRealSense/librealsense/pull/3647) - CMake enhancements : Simplified T265 FW handling, disabling redundant downloads



### Bug Fixes
* [#3810](https://github.com/IntelRealSense/librealsense/pull/3810) - Fix typo in Raspbian documentation (contributed by [@jonherke](https://github.com/jonherke))
* [#3807](https://github.com/IntelRealSense/librealsense/pull/3807) - Enable `rs-measure` with USB2 configurations
* [#3777](https://github.com/IntelRealSense/librealsense/pull/3777) - Matlab installation build fix with T265 firmware.
* [#3773](https://github.com/IntelRealSense/librealsense/pull/3773) - D435i: Fix D435i IMU timestamp precision (DSO-12084)
* [#3760](https://github.com/IntelRealSense/librealsense/pull/3760) - Fix misalignment when generating 3D Pointcloud from Depth-Aligned-To-Color #3752. (DSO-12515)
* [#3755](https://github.com/IntelRealSense/librealsense/pull/3755) - Fix "Elseif" statement in Matlab wrapper
* [#3726](https://github.com/IntelRealSense/librealsense/pull/3726) - D435i: Fix HID Timestamp trimming. #3776, #3675, (DSO-12084)
* [#3702](https://github.com/IntelRealSense/librealsense/pull/3702) - D435i: Fix Windows Metadata script for IMU-enabled SKUs.

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets #3781.(DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* [#2850](https://github.com/IntelRealSense/librealsense/issues/2850) / DSO-11696 - Linux Kernel 4.19 support
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialised value(s)


## Release 2.20.0
Release Date: 4 April 2019

### API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-version-2190-to-2200) from 2.19.x versions

### New Features & Improvements
* [#3522](https://github.com/IntelRealSense/librealsense/pull/3522) - Adding Pose&Image T265 example
* [#3541](https://github.com/IntelRealSense/librealsense/pull/3541) - Implement T265 Fisheye camera intrinsics
* [#3563](https://github.com/IntelRealSense/librealsense/pull/3563) - Implement T265 extrinsics
* [#3571](https://github.com/IntelRealSense/librealsense/pull/3571) - Adding Roll-pitch-yaw T265 example
* [#3593](https://github.com/IntelRealSense/librealsense/pull/3593) - Adding Basic Augmented Reality T265 example
* [#3600](https://github.com/IntelRealSense/librealsense/pull/3600) - Updating Unity documentation
* [#3602](https://github.com/IntelRealSense/librealsense/pull/3602) - C# development, adding [cookbook.md](https://github.com/ogoshen/librealsense/blob/4b7b6c9cbcc68e96f840e13255924ca2f8e426a7/wrappers/csharp/Documentation/cookbook.md) and addressing [#3418](https://github.com/IntelRealSense/librealsense/issues/3418), [#3419](https://github.com/IntelRealSense/librealsense/issues/3419), [#3557](https://github.com/IntelRealSense/librealsense/issues/3557)
* [#3634](https://github.com/IntelRealSense/librealsense/pull/3634) - Adding pipeline callbacks API for python
* [#3643](https://github.com/IntelRealSense/librealsense/pull/3643) - Simplified udev-rules installation script
* [#3669](https://github.com/IntelRealSense/librealsense/pull/3669) - Integration of T265 firmware 0.0.18.5448, with better long-term stability and calibration APIs
* [#3673](https://github.com/IntelRealSense/librealsense/pull/3673) - Adding documentation on update of Debian packages

### Bug Fixes
* [#3610](https://github.com/IntelRealSense/librealsense/pull/3610) - Fixing Raspbian documentation (contributed by [RitwikSaikia](https://github.com/RitwikSaikia))
* [#3564](https://github.com/IntelRealSense/librealsense/pull/3564) - Fixing rs-convert crash (contributed by [@YangJiao1996](https://github.com/YangJiao1996))
* [#3591](https://github.com/IntelRealSense/librealsense/pull/3591) - Fixing [#3435](https://github.com/IntelRealSense/librealsense/issues/3435), multi-T265 display in the RealSense Viewer
* [#3641](https://github.com/IntelRealSense/librealsense/pull/3641) - Fixing [#3623](https://github.com/IntelRealSense/librealsense/issues/3623), broken CUDA optimization of color conversion
* [#3646](https://github.com/IntelRealSense/librealsense/pull/3646) - Fixes to wheel-odometry unit-test
* [#3666](https://github.com/IntelRealSense/librealsense/pull/3666) - Release GIL in `pipeline::wait_for_frames()` (contributed by [@landersson](https://github.com/landersson))

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2693](https://github.com/IntelRealSense/librealsense/issues/2693) - Error in reading rosbag files
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* [#2850](https://github.com/IntelRealSense/librealsense/issues/2850) / DSO-11696 - Linux Kernel 4.19 support
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialised value(s)

## Release 2.19.2
Release Date: 27 March 2019

### API Changes
No API changes in this release

### New Features & Improvements
* SDK Examples Enhancements [#3548](https://github.com/IntelRealSense/librealsense/pull/3548)
* [Android] Adding device query and firmware version checking [#3547](https://github.com/IntelRealSense/librealsense/pull/3547)
* Use CASE macro consistently [#3539](https://github.com/IntelRealSense/librealsense/pull/3539) contributed by [@nussetorten](https://github.com/nussetorten)
* [T265] Separate wheel-odometry tests [#3535](https://github.com/IntelRealSense/librealsense/pull/3535)
* [T265] Enforce stream index for fisheye streams of the T265 [#3521](https://github.com/IntelRealSense/librealsense/pull/3521)
* [T265] Adding Trajectory example [#3513](https://github.com/IntelRealSense/librealsense/pull/3513)
* Improved comment on the post processing example [#3509](https://github.com/IntelRealSense/librealsense/pull/3509) contributed by [@Heidelberger](https://github.com/Heidelberger)
* Fix typo in raspbian installation [#3484](https://github.com/IntelRealSense/librealsense/pull/3484) contributed by [yuta-imai](https://github.com/yuta-imai)
* [T265] Get Motion Intrinsics [#3482](https://github.com/IntelRealSense/librealsense/pull/3482)
* [#3478](https://github.com/IntelRealSense/librealsense/pull/3478) Add arguments for python threshold filter, contributed by [@codinglife001](https://github.com/codinglife001)
* [T265] Don't raise a hardware event for relocalizations [#3477](https://github.com/IntelRealSense/librealsense/pull/3477)
* [#3471](https://github.com/IntelRealSense/librealsense/pull/3471) `rs-enumerate-devices` enhancements
* [#3462](https://github.com/IntelRealSense/librealsense/pull/3462) - Wheel odometry API: use translational velocity 
* [#3459](https://github.com/IntelRealSense/librealsense/pull/3459) - Adding CMake option to generate python documentation
* [T265] Use T265 system timestamps [#3453](https://github.com/IntelRealSense/librealsense/pull/3453)
* [Linux] Adding minor version to the SONAME [#3449](https://github.com/IntelRealSense/librealsense/pull/3449) contributed by [@morxa](https://github.com/morxa)

### Bug Fixes
* [D435i][python] IMU FPS can't be changed in Python, tracked on DSO-12326, [#3578](https://github.com/IntelRealSense/librealsense/pull/3578)
* [Matlab] Aligning colour to depth [#3577](https://github.com/IntelRealSense/librealsense/pull/3577) addressing [3338](https://github.com/IntelRealSense/librealsense/issues/3338)
* [Viewer] Fixing SegFault on pose stream info [#3423](https://github.com/IntelRealSense/librealsense/issues/3423)
* Fixing [3494](https://github.com/IntelRealSense/librealsense/issues/3494) - backward compatibility break for older ROS-bag recordings
* [T265] Fix query_devices issue with the tracking camera [#3515](https://github.com/IntelRealSense/librealsense/pull/3515), addressing #3488, #3465, #3361, also related to #3437, #3434, tracked on: TM2-4235
* [#3466](https://github.com/IntelRealSense/librealsense/pull/3466) - Fixing USB2 being identified as USB3 in some cases
* [#3455](https://github.com/IntelRealSense/librealsense/pull/3455) - Trimming HID timestamps to 32-bit, tracked on: DSO-12084

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2693](https://github.com/IntelRealSense/librealsense/issues/2693) - Error in reading rosbag files
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* [#2850](https://github.com/IntelRealSense/librealsense/issues/2850) / DSO-11696 - Linux Kernel 4.19 support
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3435](https://github.com/IntelRealSense/librealsense/issues/3435) - multiple T265 cameras are not visualized correctly in the RealSense Viewer
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialised value(s)

## Release 2.19.1
Release Date: 10 March 2019

### API Changes
No API changes in this release

### New Features & Improvements
* Intel RealSense D430i support - [#3415](https://github.com/IntelRealSense/librealsense/pull/3415) and [#3424](https://github.com/IntelRealSense/librealsense/pull/3424) (requires firmware 5.11.6)
* Adding [`pose-predict`](https://github.com/IntelRealSense/librealsense/tree/development/examples/pose-predict) example for the T265 tracking camera
* **Preliminary** Mac-OS support for the T265 (see known issues)
* Adding support for 848x100 resolution at 100 FPS (requires firmware 5.11.6)
* [#3425](https://github.com/IntelRealSense/librealsense/pull/3425) - improved Mac OS installation documentation (contributed by [@yousseb](https://github.com/yousseb))

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2693](https://github.com/IntelRealSense/librealsense/issues/2693) - Error in reading rosbag files
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* [#2850](https://github.com/IntelRealSense/librealsense/issues/2850) / DSO-11696 - Linux Kernel 4.19 support
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* [#3435](https://github.com/IntelRealSense/librealsense/issues/3435) - multiple T265 cameras are not visualized correctly in the RealSense Viewer
* [#3423](https://github.com/IntelRealSense/librealsense/issues/3423) - possible SEGFAULT when switching into Pose Info view in the RealSense Viewer

## Release 2.19.0
Release Date: 05 March 2019

## API Changes
* [2.18.1 to 2.19.0](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-version-2181-to-2190)

### New Features & Improvements

#### T265 Tracking Camera

* [T265 tracking camera support](https://github.com/IntelRealSense/librealsense/blob/v2.18.1/doc/imu_and_tracking_sensors.md) - [#3331](https://github.com/IntelRealSense/librealsense/pull/3331), [#3359](https://github.com/IntelRealSense/librealsense/pull/3359):
> :pushpin: The T265 tracking camera is not yet supported on Android and Mac-OS via librealsense. Support is planned to be added in a future release.

> :pushpin: Wheel-odometry is required to meet performance of <1% loop closure error on wheeled robots. [Learn More...](https://github.com/IntelRealSense/librealsense/pull/3324)

> :pushpin: T265 map internal format will change in future releases

> :pushpin: Additional examples, white-papers and tutorials on advanced topics including wheel-odometry and relocalization map loading will be published in the future
* [Advanced T265 APIs](https://github.com/IntelRealSense/librealsense/pull/3324) - adding new sensors extensions allowing relocalization map load / store, static node set / get (coordinates transform between different maps) and wheel odometry input
* [Ability to unload tracking camera module](https://github.com/IntelRealSense/librealsense/pull/3339) - for better ROS and [NCS](https://github.com/IntelRealSense/librealsense/issues/2924) compatibility
* [rs-pose](https://github.com/IntelRealSense/librealsense/tree/development/examples/pose) - new example showing the basics of working with T265 tracking camera

#### Android

* [Android Play-Store support](https://github.com/IntelRealSense/librealsense/blob/development/doc/android.md) - [#3083](https://github.com/IntelRealSense/librealsense/pull/3083), [#3317](https://github.com/IntelRealSense/librealsense/pull/3317), [#3337](https://github.com/IntelRealSense/librealsense/pull/3337), [#3366](https://github.com/IntelRealSense/librealsense/pull/3366): using peripheral RealSense cameras on Android no longer require the device to be rooted. This feature includes **basic** Java bindings, code samples and tools. 
> :pushpin: The T265 tracking camera and the D435i depth camera are not yet supported on Android via librealsense. Support is planned to be added in a future release.

#### Other

* [Automated Standards Enforcement](https://github.com/IntelRealSense/librealsense/pull/3265) - enforce basic project standards during CI
* [C# & Unity updates](https://github.com/IntelRealSense/librealsense/pull/3285) - multiple changes to the .NET wrapper, including support for motion and pose frames, addressing [#2854](https://github.com/IntelRealSense/librealsense/pull/2854), [#3250](https://github.com/IntelRealSense/librealsense/pull/3250), [#3275](https://github.com/IntelRealSense/librealsense/pull/3275)
* [Refactoring of options and filters API](https://github.com/IntelRealSense/librealsense/pull/3352) - allows different devices to advertise different post-processing capabilities.
* [API for adding software device into existing context](https://github.com/IntelRealSense/librealsense/pull/3340) - for development of better converters and 3rd-party depth sources

## Bug Fixes
* [Added fstream dependency](https://github.com/IntelRealSense/librealsense/pull/3280) - contributed by [@RanoVeder](https://github.com/RanoVeder) addressing [#3279](https://github.com/IntelRealSense/librealsense/issues/3279) and DSO-12001
* [Update python-rs400-advanced-mode-example.py](https://github.com/IntelRealSense/librealsense/pull/3347) - contributed by [@skylouis](https://github.com/skylouis)
* [Replace vec2mat with reshape 2](https://github.com/IntelRealSense/librealsense/pull/3257) - contributed by [@changh95](https://github.com/changh95)
* DSO-11755 - Viewer crash when fail to set advanced mode setting
* [#3252](https://github.com/IntelRealSense/librealsense/issues/3252) - Cannot change AE mean intensity point in the Viewer
* DSO-9820 - Cannot load JSON with RGB8 format in the Viewer
* [#3297](https://github.com/IntelRealSense/librealsense/issues/3297) - rs-convert does not terminate execution
* [#3214](https://github.com/IntelRealSense/librealsense/issues/3214) - rs-convert does not convert to PLY
* [#3159](https://github.com/IntelRealSense/librealsense/issues/3159) - conditionally define `STRINGIFY` macro
* [#3187](https://github.com/IntelRealSense/librealsense/issues/3187) - missing include in `example.hpp`
* [#2844](https://github.com/IntelRealSense/librealsense/issues/2844) - `rs2_depth_frame_get_distance` doesn't work for software_device sensor
* DSO-11903 - YUY in the Viewer produces white image

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2693](https://github.com/IntelRealSense/librealsense/issues/2693) - Error in reading rosbag files
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* [#2850](https://github.com/IntelRealSense/librealsense/issues/2850) / DSO-11696 - Linux Kernel 4.19 support
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing

## Release 2.18.1
Feb 07, 2019
 
## API Changes
No C/C++ API changes in this release
 
### New Features & Improvements
* [rs-motion](https://github.com/IntelRealSense/librealsense/blob/development/examples/motion) - new example dedicated to devices with an IMU
* [#3203](https://github.com/IntelRealSense/librealsense/pull/3203) - correct T265 PID reporting
* .NET API to register extrinsics ([#3202](https://github.com/IntelRealSense/librealsense/pull/3202) contributed by [@jb455](https://github.com/jb455))
* Making CV examples work with all versions of OpenCV ([#3196](https://github.com/IntelRealSense/librealsense/pull/3196) contributed by [@devernay](https://github.com/devernay) and [@s-trinh](https://github.com/s-trinh))
* Added link to [realsense-ir-to-vaapi-h264](https://github.com/bmegli/realsense-ir-to-vaapi-h264) community example ([#3194](https://github.com/IntelRealSense/librealsense/pull/3194) contributed by [@bmegli](https://github.com/bmegli))
* Adding Hardware Reset to .NET API ([#3192](https://github.com/IntelRealSense/librealsense/pull/3192) contributed by [@victorsbd](https://github.com/victorsbd))
* Addressing libusb error C2001 ([#3190](https://github.com/IntelRealSense/librealsense/pull/3190) contributed by [@UnaNancyOwen](https://github.com/UnaNancyOwen)) 
* Improvements to IMU calibration documentation ([#3172](https://github.com/IntelRealSense/librealsense/pull/3172) and [#3132](https://github.com/IntelRealSense/librealsense/pull/3132) contributed by [@barnjamin](https://github.com/barnjamin))
* [#3162](https://github.com/IntelRealSense/librealsense/pull/3162) - basic T265 Python example
* [#3161](https://github.com/IntelRealSense/librealsense/pull/3161) - adding IMU documentation
* [#3149](https://github.com/IntelRealSense/librealsense/pull/3149) - don't rebuild libtm after CMake if T265 firmware did not change

### Bug Fixes
* Fixing GLSL issue on Mac OS ([#3195](https://github.com/IntelRealSense/librealsense/pull/3195) contributed by [@devernay](https://github.com/devernay))
* [#3177](https://github.com/IntelRealSense/librealsense/issues/3177) - Depth quality tool issue, no point cloud visualization in 3D mode ([#3130](https://github.com/IntelRealSense/librealsense/pull/3130))
* [#3137](https://github.com/IntelRealSense/librealsense/issues/3137), [#3146](https://github.com/IntelRealSense/librealsense/issues/3146), [#3212](https://github.com/IntelRealSense/librealsense/issues/3212), [#3191](https://github.com/IntelRealSense/librealsense/issues/3191) - Invalid Value in rs2_get_option error after upgrading to firmware 5.11.1.0 ([#3127](https://github.com/IntelRealSense/librealsense/pull/3127))
* [#2965](https://github.com/IntelRealSense/librealsense/issues/2965) - D435i accelero not working on some platforms ([#3200](https://github.com/IntelRealSense/librealsense/pull/3200), DSO-11745)
* [#3113](https://github.com/IntelRealSense/librealsense/pull/3113) / DSO-11799 - Fix bug with depth scale before starting device
* (Python) [#3111](https://github.com/IntelRealSense/librealsense/pull/3111) / DSO-10988 - Add dims=3 option to get_vertices/get_texture for (h,w,n) output format
 
### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2472) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2693](https://github.com/IntelRealSense/librealsense/issues/2693) - Error in reading rosbag files
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* (Python) DSO-10777 - LIBUSB_ERROR_IO on repeated sensor open/close
* DSO-9820 - Cannot load RGB8 format in the JSON file for D415
* (.NET) [#2854](https://github.com/IntelRealSense/librealsense/issues/2854) / DSO-11095 - c# D400 Series Visual Presets
* [#2924](https://github.com/IntelRealSense/librealsense/issues/2924) / DSO-11705 - usbids conflicts with Movidius Neural Compute Stick
* [#2850](https://github.com/IntelRealSense/librealsense/issues/2850) / DSO-11696 - Linux Kernel 4.19 support
* (Python) [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) / DSO-10681 - missing python example of alignment with post-processing
* DSO-11755 - Realsense Viewer total crash when sliding Rsm controls to max value

## Release 2.18.0
Jan 22, 2019
 
## API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-version-2170-to-2180) from 2.17.0 version
 
### New Features & Improvements
* Realsense-viewer enhancements:
   * Rendering 3D camera model in 3D view
   * Depth threshold [min/max] control
   * Adding `Report Issue` button
   * Adding configuration file to control and preserve UX settings
     - Control record file name and location ([#2750](https://github.com/IntelRealSense/librealsense/issues/2750))
     - Recording compression level (follow-up on [#2687](https://github.com/IntelRealSense/librealsense/pull/2687))
   * Enhancing support for POSE frame type ([#3010](https://github.com/IntelRealSense/librealsense/pull/3010))
* D435i IMU intrinsic calibration ([Learn More...](https://github.com/IntelRealSense/librealsense/tree/master/tools/rs-imu-calibration#rs-imu-calibration-tool)) [(#3023)](https://github.com/IntelRealSense/librealsense/pull/3023).
* **[Firmware 5.11+]** Alternating emitter (on/off) flickering pattern ([#3066](https://github.com/IntelRealSense/librealsense/pull/3066) following-up on [#482](https://github.com/IntelRealSense/librealsense/issues/482), [#1299](https://github.com/IntelRealSense/librealsense/issues/1299))
* Upgrade to GLFW 3.3 ([#3051](https://github.com/IntelRealSense/librealsense/pull/3051))
* Adding **Code of Conduct** ([#3034](https://github.com/IntelRealSense/librealsense/pull/3034))
* Improved file structure in the C# wrapper ([#3038](https://github.com/IntelRealSense/librealsense/pull/3038))
* Completing CI migration from Appveyor and consolidation all build types to Travis, including Windows. Enhancing parallel build ([#2993](https://github.com/IntelRealSense/librealsense/pull/2993))
* Adding community-developed [installation guide for **raspbian**](https://github.com/IntelRealSense/librealsense/blob/master/doc/installation_raspbian.md) platform (contributed by [@koji](https://github.com/koji)) 
 
### Bug Fixed
* [#2997](https://github.com/IntelRealSense/librealsense/pull/2997) - Fix IMU Start-up delay on Linux (DSO-11674)
* [#3080](https://github.com/IntelRealSense/librealsense/issues/3080) - **[Matlab]** `get_extrinsics` fix
* [#3047](https://github.com/IntelRealSense/librealsense/issues/3047) - Revert to a stable libusb release
* [#2540](https://github.com/IntelRealSense/librealsense/issues/2540) - Using playback function in unity crash (DSO-10757)
* [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) - Python Decimation Filter with Aligning Frames (DSO-10681)
 
### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block
* [#2965](https://github.com/IntelRealSense/librealsense/issues/2965) - D435i accel sensor fails to start on some Linux PC
* **[MacOS]** File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2492) - Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2693](https://github.com/IntelRealSense/librealsense/issues/2693) - Error in reading rosbag files
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug

## Release 2.17.0
Nov 28, 2018

## API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-version-2160-to-2170) from 2.16.x versions

### New Features & Improvements

* Adding [rs-callback](https://github.com/IntelRealSense/librealsense/tree/development/examples/callback) example for asynchronous (low-latency) processing with pipeline.
* Adding new [python](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/python/examples#pointcloud-visualization) and [Matlab](https://github.com/IntelRealSense/librealsense/tree/development/wrappers/matlab#building-from-source) examples for point-cloud data visualization 
* D435i IMU is now supported on Windows 10 ([#2788](https://github.com/IntelRealSense/librealsense/pull/2788), DSO-10754)
* `rs-capture` will now show IMU data when connected to D435i, and rest of the SDK demos will work properly.

### Bug Fixes

* [#2763](https://github.com/IntelRealSense/librealsense/issues/2763) - SDK can now be compiled with `-Werror=shadow` GCC flag
* [#2645](https://github.com/IntelRealSense/librealsense/issues/2645) - fixing symbols collision with ROS libraries

### Known Issues
* [#866](https://github.com/IntelRealSense/librealsense/issues/866) **[Firmware]** - Read device temperature
* [#774](https://github.com/IntelRealSense/librealsense/issues/774) **[Firmware]** RGB-Depth sync
* [#1086](https://github.com/IntelRealSense/librealsense/issues/1086) **[Firmware]** Frames didn't arrive error - after improper shutdown 
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* [#2241](https://github.com/IntelRealSense/librealsense/issues/2241) Intel RealSence Viewer crash when add playback source
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) Python Decimation Filter with Aligning Frames (DSO-10681)
* [#2376](https://github.com/IntelRealSense/librealsense/issues/2376) cv::align not optimized (windows 10, C++) (DSO-10718)
* [#2540](https://github.com/IntelRealSense/librealsense/issues/2540) Using playback function in unity crash (DSO-10757)
* [#2575](https://github.com/IntelRealSense/librealsense/issues/2575) Automatic Firmware Downgrade: 5.9.2 to 5.8.15
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2492) Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2479](https://github.com/IntelRealSense/librealsense/issues/2497) USB2.1 infra-red exposure issue for short exposure times
* [#2693](https://github.com/IntelRealSense/librealsense/issues/2693) - Error in reading rosbag files


### Other Issues
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).

## Release 2.16.5
Nov 19, 2018

## API Changes
No API changes in this release

### New Features & Improvements
* Optimization of [align processing with CUDA](https://github.com/IntelRealSense/librealsense/pull/2670).  
Results with Jetson TX2 board:  

![align_results](https://user-images.githubusercontent.com/18511514/47967255-31b38480-e064-11e8-9815-240117e37505.PNG)
* [Core] Disable platform cameras from being selected with pipeline ([PR2600](https://github.com/IntelRealSense/librealsense/pull/2600))
* [Core] Refactoring of CMake configuration files - also addressing [#745](https://github.com/IntelRealSense/librealsense/issues/745) issue ([PR2716](https://github.com/IntelRealSense/librealsense/pull/2716)).  
Note that the following librealsense Cmake variables have been modified:  
`realsense_INCLUDE_DIR` -> `realsense2_INCLUDE_DIR`  
`realsense_VERSION` -> `realsense2_VERSION`  
* [Linux] Add D435i IMU patch for non-LTS kernel 4.16
* [Matlab] Add Matlab build to CMake. Multiple fixes to wrapper [2644](https://github.com/IntelRealSense/librealsense/pull/2644), []()
* [Matlab] Replace toolbox' `vec2mat` with standard `reshape` in `rosbag_example` by [@apoorva2398](https://github.com/IntelRealSense/librealsense/pull/2708)
* [OpenCV] Fixing typo in [Getting Started with OpenCV](https://github.com/IntelRealSense/librealsense/blob/master/doc/stepbystep/getting_started_with_openCV.md) guide by [@gideont](https://github.com/IntelRealSense/librealsense/pull/2708)
* [OpenCV] Adding a key press to exit the image window by [@vinaysannaiah](https://github.com/IntelRealSense/librealsense/pull/2641)
* [PCL] Color example provided by [@LinuxGogley](https://github.com/IntelRealSense/librealsense/pull/2668)
* [OpenNI] Linux build fix by [@Daichou ](https://github.com/IntelRealSense/librealsense/pull/2651)
* [Easylogging++] Update to v9.96.5 by [@rschlaikjer](https://github.com/IntelRealSense/librealsense/pull/2674)
* [Core] `rs-convert` documentation updated to address [#2671](https://github.com/IntelRealSense/librealsense/issues/2671)

### Bug fixes
* [#745](https://github.com/IntelRealSense/librealsense/issues/745) - CMake: fix `find_package` functionality
* [#2710](https://github.com/IntelRealSense/librealsense/issues/2710) - Matlab wrapper: Correct error in align.m
* [#2539](https://github.com/IntelRealSense/librealsense/issues/2539) - Matlab wrapper: error on context.query_devices
* [#2541](https://github.com/IntelRealSense/librealsense/issues/2541) - Matlab wrapper: crash when trying to get intrinsics
* [#2487](https://github.com/IntelRealSense/librealsense/issues/2487) - Matlab: wrapper typos
* [#1587](https://github.com/IntelRealSense/librealsense/issues/1587) -  [Libuvc] serializing json in adv mode (DSO-9702)
* DSO-10889: IMU timestamp conversion patch with kernels 4.8/10 ([PR2732](https://github.com/IntelRealSense/librealsense/pull/2732)).
* DSO-10471: Remove zero-copy for YUYV ([PR2653](https://github.com/IntelRealSense/librealsense/pull/2653)).
* Update depth units when modified by user ([PR2665](https://github.com/IntelRealSense/librealsense/pull/2665)).

### Known Issues
* [#866](https://github.com/IntelRealSense/librealsense/issues/866) **[Firmware]** - Read device temperature
* [#774](https://github.com/IntelRealSense/librealsense/issues/774) **[Firmware]** RGB-Depth sync
* [#1086](https://github.com/IntelRealSense/librealsense/issues/1086) **[Firmware]** Frames didn't arrive error - after improper shutdown 
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* [#2241](https://github.com/IntelRealSense/librealsense/issues/2241) Intel RealSence Viewer crash when add playback source
* Frame Drops when changing depth controls while depth streaming. (DSO-9065)
* [#2321](https://github.com/IntelRealSense/librealsense/issues/2321) and [#2376](https://github.com/IntelRealSense/librealsense/issues/2376) rs2::align optimization/performance (DSO-10718)
* [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) Python Decimation Filter with Aligning Frames (DSO-10681)
* [#2376](https://github.com/IntelRealSense/librealsense/issues/2376) cv::align not optimized (windows 10, C++) (DSO-10718)
* [#2540](https://github.com/IntelRealSense/librealsense/issues/2540) Using playback function in unity crash (DSO-10757)
* [#2575](https://github.com/IntelRealSense/librealsense/issues/2575) Automatic Firmware Downgrade: 5.9.2 to 5.8.15
* [#2472](https://github.com/IntelRealSense/librealsense/issues/2492) Application hangs when trying to close file replay pipeline (DSO-10749)
* [#2479](https://github.com/IntelRealSense/librealsense/issues/2497) USB2.1 infra-red exposure issue for short exposure times
* [#2645](https://github.com/IntelRealSense/librealsense/issues/2645)[ROS] Librealsense collision with ROS API ros::Time::now()
* [#2693](https://github.com/IntelRealSense/librealsense/issues/2693) - Error in reading rosbag files


### Other Issues
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).


## Release 2.16.1
Sep 25, 2018

## API Changes
No API changes in this release

### New Features & Improvements

* [Add log mechanism for Android port](https://github.com/IntelRealSense/librealsense/pull/2429)
* [Adding Windows 7 support](https://github.com/dorodnic/librealsense/blob/development/doc/installation_win7.md)
* [Adding `ENABLE_CCACHE` CMake flag, contributed by @akatrevorjay](https://github.com/IntelRealSense/librealsense/pull/2342)
* [Strict uvcvideo buffers overflow handling](https://github.com/IntelRealSense/librealsense/pull/2341) - this patch is likely to create issues with 5.8.15 firmware and requires a firmware update.
* [Adding `TESTDATA_LOCATION` CMake flag, contributed by @muojp](https://github.com/IntelRealSense/librealsense/pull/2388/files)

### Bug fixes
* [#2420](https://github.com/IntelRealSense/librealsense/issues/2420), [#2306](https://github.com/IntelRealSense/librealsense/issues/2306) - RGB decoding on non-Intel non-Android systems
* [#2430](https://github.com/IntelRealSense/librealsense/pull/2430) - crash on some Android systems due to memory alignment
* [#2377](https://github.com/IntelRealSense/librealsense/pull/2377) - fix for ROS file format, contributed by @shuntaraw
* [#2371](https://github.com/IntelRealSense/librealsense/pull/2371) - fixing texture misalignment in the Viewer in last release
* [#1579](https://github.com/IntelRealSense/librealsense/issues/1579), [#1919](https://github.com/IntelRealSense/librealsense/issues/1919), [#2102](https://github.com/IntelRealSense/librealsense/issues/2102), [#2242](https://github.com/IntelRealSense/librealsense/issues/2242), [#2224](https://github.com/IntelRealSense/librealsense/issues/2224), [#2216](https://github.com/IntelRealSense/librealsense/issues/2216), [#2214](https://github.com/IntelRealSense/librealsense/issues/2214), [#2308](https://github.com/IntelRealSense/librealsense/issues/2308), [#2411](https://github.com/IntelRealSense/librealsense/issues/2411) - Issues related to ROS-bag playback
* Several issues related to Mac OS stability reported under [#2057](https://github.com/IntelRealSense/librealsense/issues/2057)
* [#2354](https://github.com/IntelRealSense/librealsense/pull/2354) - fixed OpenCV compilation, contributed by @neuralassembly
* [#2318](https://github.com/IntelRealSense/librealsense/issues/2318) - Broken presets interface in the Intel RealSense Viewer 
* [#2311](https://github.com/IntelRealSense/librealsense/issues/2311) - USB 2.1 when plugging in slowly

### Known Issues
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* DSO-9702 #1587 Issue serializing json in adv mode: Value not found in map! value=8
* DSO-9065 - Frame Drops when changing depth controls while depth streaming
* **[Firmware]** - Read device temperature [#866](https://github.com/IntelRealSense/librealsense/issues/866)

### Other Issues
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).

## Release 2.16.0
Aug 27, 2018

## API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-version-2150-to-2160) from 2.15.0 version

### New Features & Improvements
* [#2154](https://github.com/IntelRealSense/librealsense/pull/2154) - Adding Two Dimensional Data Protocols for python wrapper (by @baptiste-mnh)
* DSO-10233 / [#2265](https://github.com/IntelRealSense/librealsense/pull/2265) - Adding function to project single color pixel to the depth image
* DSO-7213 / [#1038](https://github.com/IntelRealSense/librealsense/pull/1038) - Matlab Wrapper
* DSO-10202 / [#2245](https://github.com/IntelRealSense/librealsense/pull/2245) - making sure all SDK processing can be done consistently at frame-set level, allowing easier composition of processing

### Bug fixes
* DSO-9792 / [#1899](https://github.com/IntelRealSense/librealsense/issues/1899) - C# query device function doesn't release memory causing memory leak
* [#2299](https://github.com/IntelRealSense/librealsense/issues/2299) - better handling of AVX compilation (by @kjkjava)
* DSO-10262 / [#2293](https://github.com/IntelRealSense/librealsense/pull/2293) - D430+MM not moving to idle power state
* [#2008](https://github.com/IntelRealSense/librealsense/issues/2008) / [#2075](https://github.com/IntelRealSense/librealsense/issues/2075) - merging general Android fixes
* DSO-10227 / [#2283](https://github.com/IntelRealSense/librealsense/pull/2283) - pipeline stop & start not working on Android
* DSO-10045 / [#2002](https://github.com/IntelRealSense/librealsense/issues/2002) - aligned intrinsics incorrect
* DSO-10274 / [#2187](https://github.com/IntelRealSense/librealsense/issues/2187) - end of recording sometimes causes a crash
* DSO-9160 / [#1514](https://github.com/IntelRealSense/librealsense/issues/1514) - Kernel 4.16 support (new metadata V4L2 API)
* DSO-10101 / [#2097](https://github.com/IntelRealSense/librealsense/issues/2097) - Pre-built Intel.Realsense.dll has no version number
* [#2261](https://github.com/IntelRealSense/librealsense/issues/2261) - RGBA with depth-to-color alignment
* [#2256](https://github.com/IntelRealSense/librealsense/issues/2256) - avoid crash in case of illegal device ID (by @bentank)


### Known Issues
* Repeatedly changing exposure of d435 brings down a camera ([#1687](https://github.com/IntelRealSense/librealsense/issues/1687))
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Artifact generated in depth image/point cloud from SR300 (DSO-9383)
* DSO-9702 #1587 Issue serializing json in adv mode: Value not found in map! value=8
* DSO-9853 - #1919 problems (framedrop) in rs_convert
* DSO-9065 - Frame Drops when changing depth controls while depth streaming

### Other Issues
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).

## Release 2.15.0
Aug 10, 2018

## API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-version-2140-to-2150) from 2.14.0 version

### New Features & Improvements
* Establishing [Debian repository](https://github.com/IntelRealSense/librealsense/pull/2146) for Ubuntu 18 (Bionic) packages, including DKMS.
* Adding [processing blocks to Unity wrapper](https://github.com/IntelRealSense/librealsense/pull/2164)
* Enhancements for python [Box Dimentioner](https://github.com/IntelRealSense/librealsense/pull/2160) demo 

### Bug fixes
* DSO-10232 / [#2202](https://github.com/IntelRealSense/librealsense/issues/2202) - Depth alignment grid artifact for specific resolutions
* [Android] Fix Android Studio build
* DSO-9738 / [#2208](https://github.com/IntelRealSense/librealsense/issues/2208) - [Viewer] ROI control attached to non-ROI sensors.
* DSO-9927- [Linux] Fix idle state management to reduce power consumption.
* DSO-9942 / [#1998](https://github.com/IntelRealSense/librealsense/issues/1998) - Y16 "Save snapshot" Crashes RealSense Viewer
* [DQT] Wrong message is presented with no camera connected (DSO-7994) / ( [#1775](https://github.com/IntelRealSense/librealsense/issues/1775), ( [#1580](https://github.com/IntelRealSense/librealsense/issues/1580) )


### Known Issues
* Frame drops when changing depth controls while streaming (DSO-9065)
* Repeatedly changing exposure of d435 brings down a camera ([#1687](https://github.com/IntelRealSense/librealsense/issues/1687))
* Potential alignment issue when using enable_device ([#1504](https://github.com/IntelRealSense/librealsense/issues/1504))
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Artifact generated in depth image/point cloud from SR300 (DSO-9383)
* DSO-9792 - C# query device function doesn't release memory causing memory leak
* DSO-9160 #1514 Inappropriate ioctl - Kernel 4.16 with the new metadata treenode
* DSO-9702 #1587 Issue serializing json in adv mode: Value not found in map! value=8
* DSO-9853 - #1919 problems (framedrop) in rs_convert
* DSO-9802 - #1462, Invalid Depth Band in depth stream is not match to spec
* DSO-9357 - D420 / D430 Cameras w/ FW 5.9.11 wont run LRS 2.11 align capture and pointcloud apps
* DSO-9065 - Frame Drops when changing depth controls while depth streaming

### Other Issues
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).
* Linux Kernel 4.16 is currently not supported due to changes to the media sub-system and specifically metadata nodes.
Patches are available for Ubuntu LTS kernel 4.15.(DSO-9160,[#1514](https://github.com/IntelRealSense/librealsense/issues/1514))



## Release 2.14.0
July 17, 2018

## API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2140-vs-2130) from the previous 2.13.0 versions

### New Features & Improvements
* [Try Wait for Frames](https://github.com/IntelRealSense/librealsense/pull/2049) API added for more intelligent CPU utilization ([#1949](https://github.com/IntelRealSense/librealsense/issues/1949))
* Major rework of [RealSense Unity Sample](https://github.com/IntelRealSense/librealsense/pull/2063) with many new features
* Option to generate Unity package via CMake - [#1974](https://github.com/IntelRealSense/librealsense/pull/1974)
* Significant [optimization of align processing block](https://github.com/IntelRealSense/librealsense/pull/2040) for Intel x86/x64 architecture
* Added API to fix asymmetry in rs::context notifications about devices being added / removed - [#1968](https://github.com/IntelRealSense/librealsense/pull/1968)
* DSO-8309 - Change Plane-fit RMS from mm to % in the Depth Quality tool ([#1975](https://github.com/IntelRealSense/librealsense/pull/1975))
* Viewer - Point-cloud navigation with WASD

### Bug fixes
* DSO-9443 / [#1727](https://github.com/IntelRealSense/librealsense/issues/1727) - Post-processing filters removing Depth metadata
* [#1390](https://github.com/IntelRealSense/librealsense/issues/1390) - Use long PGP ID for debian install instructions
* DSO-9736 / [#1946](https://github.com/IntelRealSense/librealsense/pull/1946) - Setting Depth Units in realsense_viewer fails 
* DSO-9472 / [#1543](https://github.com/IntelRealSense/librealsense/issues/1543) - rs2::pipeline can't playback two IR streams from bag file
* DSO-8086 - insufficient description of Depth Quality Tool distance calculation ([#2030](https://github.com/IntelRealSense/librealsense/pull/2030))
* DSO-9386 / [#1586](https://github.com/IntelRealSense/librealsense/issues/1586) - Deadlock in libuvc backend (Mac OS / Android)
* DSO-9835 / [#2039](https://github.com/IntelRealSense/librealsense/pull/2039) - incorrect multi-camera resolution using libuvc backend (Mac OS / Android)
* [Realsense Viewer] Streaming interrupted when streaming multiple cameras and deactivating one (DSO-9680)

### Known Issues
* [DQT] Wrong message is presented with no camera connected (DSO-7994)
* Frame drops when changing depth controls while streaming (DSO-9065)
* Repeatedly changing exposure of d435 brings down a camera ([#1687](https://github.com/IntelRealSense/librealsense/issues/1687))
* Potential alignment issue when using enable_device ([#1504](https://github.com/IntelRealSense/librealsense/issues/1504))
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Artifact generated in depth image/point cloud from SR300 (DSO-9383)
* DSO-9792 - C# query device function doesn't release memory causing memory leak
* DSO-9160 #1514 Inappropriate ioctl - Kernel 4.16 with the new metadata treenode
* DSO-9702 #1587 Issue serializing json in adv mode: Value not found in map! value=8
* DSO-9927 - camera not moving to Idle - Linux
* DSO-9853 - #1919 problems (framedrop) in rs_convert
* DSO-9802 - #1462, Invalid Depth Band in depth stream is not match to spec
* DSO-9738 - Cannot set Autoexposure ROI on RGB Sensor (incorrect error displayed) 
* DSO-9357 - D420 / D430 Cameras w/ FW 5.9.11 wont run LRS 2.11 align capture and pointcloud apps
* DSO-9942 - #1998 Y16 "Save snapshot" Crashes RealSense Viewer
* DSO-9065 - Frame Drops when changing depth controls while depth streaming

### Other Issues
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).
* Linux Kernel 4.16 is currently not supported due to changes to the media sub-system and specifically metadata nodes.
Patches are available for Ubuntu LTS kernel 4.15.(DSO-9160,[#1514](https://github.com/IntelRealSense/librealsense/issues/1514))

## Release 2.13.0
June 22, 2018

## Important:
* The required CMake version to build librealsense project files was promoted to 3.8.  

## API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2130-vs-2111) from the previous 2.11.1/2.12.0 versions

### New Features & Improvements
* Additional per-frame metadata attributes available for Depth and RGB sensors. (DSO-9517)
* Inter-camera hw sync control for multi-cam setups (DSO-9602)
* Adding [CUDA-optimized implementation](https://github.com/IntelRealSense/librealsense/pull/1866) for Jetson-TX (arm) platform

## Bug Fixes
* Post-processing filters invalidate metadata (DSO-9443, [#1727](https://github.com/IntelRealSense/librealsense/issues/1727))
* Enabling D430 in librealsense Demos (DSO-9397)
* Update kernel patches according to the latest Ubuntu policies (DSO-9817, [#1900](https://github.com/IntelRealSense/librealsense/pull/1900))
* Unity support for cameras without RGB sensor (DSO-8666)
* [Realsense Viewer] Save setting fail (DSO-9543)
* Multi-cam support is broken on some Mac OS systems (DSO-9231,[#1506](https://github.com/IntelRealSense/librealsense/issues/1506))


### Known Issues
* [DQT] Wrong message is presented with no camera connected (DSO-7994)
* [Linux] Double-clicking C interferes with other applications (DSO-8896)
* Frame drops when changing depth controls while streaming (DSO-9065)
* [Linux] Unit-test failure (DSO-9110)
* Multiple cameras in pyrealsense2 (DSO-9112/[#1089](https://github.com/IntelRealSense/librealsense/issues/1089))
* Read device temperature (DSO-9125)
* [MacOS] C Examples freeze (DSO-9386,[#1586](https://github.com/IntelRealSense/librealsense/issues/1586))
* Streaming multiple IR feeds from bag file (DSO-9472)
* [Realsense Viewer] Streaming interrupted when streaming multiple cameras and deactivating one (DSO-9680)
* [Realsense Viewer] Setting Depth Units to 0 pops error-message (DSO-9736)
* Repeatedly changing exposure of d435 brings down a camera ([#1687](https://github.com/IntelRealSense/librealsense/issues/1687))
* playback fails to auto-resolve two IR streams ([#1543](https://github.com/IntelRealSense/librealsense/issues/1543))
* Issue running on Android 7 Odroid XU4 board ((#1534)[https://github.com/IntelRealSense/librealsense/issues/1534])
* Potential alignment issue when using enable_device ([#1504](https://github.com/IntelRealSense/librealsense/issues/1504))
* **[Firmware]** Sporadic errors, only workaround is to physically reconnect camera ([#1213](https://github.com/IntelRealSense/librealsense/issues/1213))
* **[Firmware]** Corrupted color image after pipeline restart ([#1206](https://github.com/IntelRealSense/librealsense/issues/1206))
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Artifact generated in depth image/point cloud from SR300 (DSO-9383)
* In this release OpenMP compile flag is disabled by default, which can reduce the CPU utilization. Please refer to [#744](https://github.com/IntelRealSense/librealsense/issues/744)

### Other Issues
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).
* Linux Kernel 4.16 is currently not supported due to changes to the media sub-system and specifically metadata nodes.
Patches are available for Ubuntu LTS kernel 4.15.(DSO-9160,[#1514](https://github.com/IntelRealSense/librealsense/issues/1514))





## Release 2.12.0
June 5th, 2018

## API Changes
N/A

### New Features & Improvements
* [`rs-convert`](https://github.com/IntelRealSense/librealsense/tree/development/tools/convert) usability tool that transform librealsense records in rosbag format into separate files. The supported outputs format for depth data: raw, binary, csv, png, ply.
* Decimation filter added support for non-depth (IR/RGB) frames. (DSO-9164,DSO-8312)
* Realsense Viewer UI Enhancements:
  - Keyboard binding to facilitate navigation in 3D view ("WASD" mapping) 
  - Point-cloud rendering with Quads\Points to enhance visualization traits
  - Adding close button to notification pop-ups.
  - Point-cloud generation - Occlusion filter options extended (DSO-8513)
* Documentation added:
  - [Depth from Stereo](https://github.com/IntelRealSense/librealsense/blob/development/doc/depth-from-stereo.md) Introductory
  - [Post-processing Filters](https://github.com/IntelRealSense/librealsense/blob/development/doc/post-processing-filters.md) in Librealsense

## Bug Fixes
* [Linux] SR300 streaming with zero-copy is disabled to avoid running out of kernel-allocated memory.
* [Win] Fix power management on stream interrupt event.(DSO-9310)
* [CMake] Unit-test patterns download rules fix to prevent phony failure reports.
* [Wrappers]Unity Demo with Point-Cloud is running out of memory ([#1477](https://github.com/IntelRealSense/librealsense/issues/1477), [#1394](https://github.com/IntelRealSense/librealsense/issues/1394)) 
* Depth Gain control modifies AE mode (DSO-6853)
* [Viewer] ROI method improperly reported ([#1616](https://github.com/IntelRealSense/librealsense/issues/1616))
* High CPU utilization when running the Viewer, Windows and Linux (DSO-9381)
* Laser Power control description update ([#1793](https://github.com/IntelRealSense/librealsense/issues/1793))

* No camera control ([#765](https://github.com/IntelRealSense/librealsense/issues/765)) - Abandoned by user
* [Viewer] Streaming does not resume after wake up from sleep on Windows RS3 (S3) (DSO-8094)
* Relatively high CPU utilization on Linux when running without laser power (DSO-8040)

### Known Issues
* Read device temperature (DSO-9125)
* [Linux] Double-clicking C interferes with other applications (DSO-8896)
* [DQT] Wrong message is presented with no camera connected (DSO-7994)
* [MacOS] C Examples freeze (DSO-9386,[#1586](https://github.com/IntelRealSense/librealsense/issues/1586))
* [Realsense Viewer] Save setting fail (DSO-9543)
* Streaming multiple IR feeds from bag file (DSO-9472)
* Post-processing filters invalidate metadata (DSO-9443, [#1727](https://github.com/IntelRealSense/librealsense/issues/1727))
* [Linux] Unit-test failure (DSO-9110)
* Multiple cameras in pyrealsense2 (DSO-9112/[#1089](https://github.com/IntelRealSense/librealsense/issues/1089))
* Repeatedly changing exposure of d435 brings down a camera ([#1687](https://github.com/IntelRealSense/librealsense/issues/1687))
* playback fails to auto-resolve two IR streams ([#1543](https://github.com/IntelRealSense/librealsense/issues/1543))
* Issue running on Android 7 Odroid XU4 board ((#1534)[https://github.com/IntelRealSense/librealsense/issues/1534])
* Multi-cam support is broken on some Mac OS systems (DSO-9231/[#1506](https://github.com/IntelRealSense/librealsense/issues/1506))
* Potential alignment issue when using enable_device ([#1504](https://github.com/IntelRealSense/librealsense/issues/1504))
* **[Firmware]** Sporadic errors, only workaround is to physically reconnect camera ([#1213](https://github.com/IntelRealSense/librealsense/issues/1213))
* **[Firmware]** Corrupted color image after pipeline restart ([#1206](https://github.com/IntelRealSense/librealsense/issues/1206))
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))


* Unity support for cameras without RGB (DSO-8666)
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* In this release OpenMP compile flag is disabled by default, which can reduce the CPU utilization. Please refer to [#744](https://github.com/IntelRealSense/librealsense/issues/744)

### Other Issues
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).
* Linux Kernel 4.16 is currently not supported due to changes to the media sub-system and specifically metadata nodes.
Patches are available for Ubuntu LTS kernel 4.15.(DSO-9160,[#1514](https://github.com/IntelRealSense/librealsense/issues/1514))


## Release 2.11.1
May 17th, 2018

## API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-2110-to-2111) from the previous 2.11.0 version

### New Features & Improvements
* Support for Ubuntu 18/Bionic Beaver (kernel 4.15). DSO-8769 ([#1700](https://github.com/IntelRealSense/librealsense/issues/1700))
* Realsense [v2.11.0 wrapper for LabView](https://github.com/IntelRealSense/librealsense/tree/development/wrappers/labview#getting-started-with-realsense-sdk20-for-labview)
* Documentation updates (DSO-9164, DSO-9123)
* [New presets](https://github.com/IntelRealSense/librealsense/wiki/D400-Series-Visual-Presets#preset-table) to rectify IR pattern from Left IR imager (DSO-6868)

## Bug Fixes
* USB2/3 enumeration with RedStone3 (DSO-9161)
* Playback failure on unload_device (DSO-9269).
* Wrong height reported with distance demo. DSO-9111 (([#1516](https://github.com/IntelRealSense/librealsense/issues/1516)),([#1667](https://github.com/IntelRealSense/librealsense/issues/1667))).
* Support DMFT-introduced GUIDs on RedStone3 (DSO-9276).
* Post-processing blocks to report error on failure (([#1658](https://github.com/IntelRealSense/librealsense/issues/1658))).
* Calibration formats are not available for D5U (DSO-9382)
* [Depth Quality Tool] When the decimation filter is enabled the ROI window is offset, and the visualization changes to default when the ROI% is changed (DSO-8740)


### Known Issues
* SDK samples fail for D430 (DSO-9397)
* High CPU utilization when running the Viewer, Windows and Linux (DSO-9381)
* Repeatedly changing exposure of d435 brings down a camera ([#1687](https://github.com/IntelRealSense/librealsense/issues/1687))
* playback fails to auto-resolve two IR streams ([#1543](https://github.com/IntelRealSense/librealsense/issues/1543))
* Issue running on Android 7 Odroid XU4 board ((#1534)[https://github.com/IntelRealSense/librealsense/issues/1534])
* Multi-cam support is broken on some Mac OS systems ([#1506](https://github.com/IntelRealSense/librealsense/issues/1506))
* Potential alignment issue when using enable_device ([#1504](https://github.com/IntelRealSense/librealsense/issues/1504))
* Unity Demo with Point-Cloud is running out of memory ([#1477](https://github.com/IntelRealSense/librealsense/issues/1477), [#1394](https://github.com/IntelRealSense/librealsense/issues/1394)) 
* **[Firmware]** Sporadic errors, only workaround is to physically reconnect camera ([#1213](https://github.com/IntelRealSense/librealsense/issues/1213))
* **[Firmware]** Corrupted color image after pipeline restart ([#1206](https://github.com/IntelRealSense/librealsense/issues/1206))
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))
* No camera control ([#765](https://github.com/IntelRealSense/librealsense/issues/765))

* Unity support for cameras without RGB (DSO-8666)
* [Viewer] Streaming does not resume after wake up from sleep on Windows RS3 (S3) (DSO-8094)
* Relatively high CPU utilization on Linux when running without laser power (DSO-8040)

* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* In this release OpenMP compile flag is disabled by default, which can reduce the CPU utilization. Please refer to [#744](https://github.com/IntelRealSense/librealsense/issues/744)

### Other Issues
* The API change introduced in this version is non backward-compatible with the previous v2.11.0.
This may affect Linux users who rely on the Debian versioning compatibility policy - please remove the previous v2.11.0. when installing the current version.
* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939).
* Linux Kernel 4.16 is currently not supported due to changes to the media sub-system and specifically metadata nodes.
Patches are available for Ubuntu LTS kernel 4.15 .


## Release 2.11.0
May 06th, 2018

## API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-2104-to-2110) from the previous 2.10.4 version

### New Features & Improvements
* Playback Repeat control (#1426)
* Exposing Multipin UVC device via pybackend (#1614)
* Post-Processing via Python API (#1502 and #1535)
* SSE optimization of PointCloud processing block (#1633)
* Adding a dedicated Hole-Filling processing block (DSO-9164, #1644)
* Adding USB3.2 descriptor support (DSO-9306)
* Notify user when new firmware is available (#1648)
* Adding processing APIs to the .NET wrapper (DSO-9023)
* New camera info attribute: RS2_CAMERA_INFO_RECOMMENDED_FIRMWARE_VERSION, tracking the
[firmware recommended for D400 devices](https://downloadcenter.intel.com/download/27522/Latest-Firmware-for-Intel-RealSense-D400-Product-Family?v=t)

## Bug Fixes
* playback.seek not working in python ([#1545](https://github.com/IntelRealSense/librealsense/issues/1545))
* [DQT] Fixing Z-accuracy metric calculation in the Depth Quality Tool (DSO-8939)
* Compilation on ARM (#1593 and #1574)
* Holes filling capabilities fix of the Spatial Filter (#1591)
* Syncer crash when using two handles to the same device (#1600)
* [Viewer] Auto-exposure was not being updated in UI after setting exposure value (DSO-8873, #1636)
* [Viewer] Auto-exposure ROI was not correctly visualized with Decimation filter enabled (DSO-9096, #1638)
* Y16 format is not presented for D435 (DSO-8913)

### Known Issues
* playback fails to auto-resolve two IR streams ([#1543](https://github.com/IntelRealSense/librealsense/issues/1543))
* Issue running on Android 7 Odroid XU4 board ((#1534)[https://github.com/IntelRealSense/librealsense/issues/1534])
* rs-measure gives incorrect distance ([#1516](https://github.com/IntelRealSense/librealsense/issues/1516))
* Multi-cam support is broken on some Mac OS systems ([#1506](https://github.com/IntelRealSense/librealsense/issues/1506))
* Potential alignment issue when using enable_device ([#1504](https://github.com/IntelRealSense/librealsense/issues/1504))
* Unity Demo with Point-Cloud is running out of memory ([#1477](https://github.com/IntelRealSense/librealsense/issues/1477), [#1394](https://github.com/IntelRealSense/librealsense/issues/1394)) 
* **[Firmware]** Sporadic errors, only workaround is to physically reconnect camera ([#1213](https://github.com/IntelRealSense/librealsense/issues/1213))
* **[Firmware]** Corrupted color image after pipeline restart ([#1206](https://github.com/IntelRealSense/librealsense/issues/1206))
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))
* No camera control ([#765](https://github.com/IntelRealSense/librealsense/issues/765))

* Unity support for cameras without RGB (DSO-8666)
* [Depth Quality Tool] When the decimation filter is enabled the ROI window is offset, and the visualization changes to default when the ROI% is changed (DSO-8740)
* Detection of USB2 vs USB3 is not working correctly on Windows RS3 (DSO-9109)
* [Viewer] Streaming does not resume after wake up from sleep on Windows RS3 (S3) (DSO-8094)
* Relatively high CPU utilization on Linux when running without laser power (DSO-8040)

* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)
* Potential UV-mapping (align) error using pyrealsense (DSO-9206) 
* In this release OpenMP compile flag is disabled by default, which can reduce the CPU utilization. Please refer to [#744](https://github.com/IntelRealSense/librealsense/issues/744)

### Other Issues

* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)

* Some of the Depth Quality Tool (DQT) metrics will be modified in the next coming releases


## Release 2.10.4
April 18th, 2018

### API Changes 
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-2103-to-2104) from the previous 2.10.3 version

### New Features & Improvements
* [Viewer] Add units to camera controls (DSO-8966)
* Post-processing filters rework and testing automation (DSO-8884)
* Playback and record demo (DSO-8656)
* CTO fixes for D4M modules (#1520)
* [Depth Quality Tool] "save report" to save consistent frames (DSO-8638)
* [Viewer] Allowing to input accurate numbers in the advance mode controls (DSO-6867)

### Bug Fixes
* cpuid.h missing on Arm boards ([#1501](https://github.com/IntelRealSense/librealsense/issues/1501))
* SegFault on Intel CPUs without AVX support ([#1491](https://github.com/IntelRealSense/librealsense/issues/1491))
* [Depth Quality Tool] Cannot load presets ([#1488](https://github.com/IntelRealSense/librealsense/issues/1488), [#1457](https://github.com/IntelRealSense/librealsense/issues/1457), [#1443](https://github.com/IntelRealSense/librealsense/issues/1443), )
* Load JSON crashing on Mac ([#1392](https://github.com/IntelRealSense/librealsense/issues/1392))
* Compilation error for non-optimized builds ([#1237](https://github.com/IntelRealSense/librealsense/issues/1237))
* Linux driver stalls if a signal is received ([#1203](https://github.com/IntelRealSense/librealsense/issues/1203))
* Compilation error with -Wall in clang ([#1292](https://github.com/IntelRealSense/librealsense/issues/1292))
* enable_stream selects right IR in USB2 (DSO-8733)

### Known Issues
* playback.seek not working in python ([#1545](https://github.com/IntelRealSense/librealsense/issues/1545))
* playback fails to auto-resolve two IR streams ([#1543](https://github.com/IntelRealSense/librealsense/issues/1543))
* Issue running on Android 7 Odroid XU4 board ((#1534)[https://github.com/IntelRealSense/librealsense/issues/1534])
* rs-measure gives incorrect distance ([#1516](https://github.com/IntelRealSense/librealsense/issues/1516))
* Multi-cam support is broken on some Mac OS systems ([#1506](https://github.com/IntelRealSense/librealsense/issues/1506))
* Potential alignment issue when using enable_device ([#1504](https://github.com/IntelRealSense/librealsense/issues/1504))
* Post-processing not available for python users ([#1502](https://github.com/IntelRealSense/librealsense/issues/1502))
* Unity Demo with Point-Cloud is running out of memory ([#1477](https://github.com/IntelRealSense/librealsense/issues/1477), [#1394](https://github.com/IntelRealSense/librealsense/issues/1394))
* App crashing when using Sensor.Start using C# ([#1250](https://github.com/IntelRealSense/librealsense/issues/1250))
* **[Firmware]** Sporadic errors, only workaround is to physically reconnect camera ([#1213](https://github.com/IntelRealSense/librealsense/issues/1213))
* **[Firmware]** Corrupted color image after pipeline restart ([#1206](https://github.com/IntelRealSense/librealsense/issues/1206))
* **[Firmware]** Frames didn't arrive error - after improper shutdown ([#1086](https://github.com/IntelRealSense/librealsense/issues/1086))
* Repeated read device temperature fail on Windows ([#866](https://github.com/IntelRealSense/librealsense/issues/866))
* **[Firmware]** RGB-Depth sync ([#774](https://github.com/IntelRealSense/librealsense/issues/774))
* No camera control ([#765](https://github.com/IntelRealSense/librealsense/issues/765))

* [Depth Quality Tool] Z-accuracy distance plot has a sinusoidal pattern mismatching IPDev (DSO-8939)
* Unity support for cameras without RGB (DSO-8666)
* [Depth Quality Tool] When the decimation filter is enabled the ROI window is offset, and the visualization changes to default when the ROI% is changed (DSO-8740)
* Detection of USB2 vs USB3 is not working correctly on Windows RS3 (DSO-9109)
* [Viewer] Streaming does not resume after wake up from sleep on Windows RS3 (S3) (DSO-8094)
* Relatively high CPU utilization on Linux when running without laser power (DSO-8040)
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets (DSO-9162)

### Other Issues

* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)

* Some of the Depth Quality Tool (DQT) metrics will be modified in the next coming releases


## Release 2.10.3
April 4th, 2018

### API Changes 
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-2102-to-2103) from the previous 2.10.2 version

### New Features & Improvements

* Integrated functionality changes in preparation for USB2 firmware support (DSO-8952)

### Bug Fixes
* [MacOS] Changing resolution after first start & stop fails. Reconnect might be required
* Fixing ARM build ([#1472](https://github.com/IntelRealSense/librealsense/pull/1472))
* Fixing compilation error with -Wall in clang ([#1292](https://github.com/IntelRealSense/librealsense/pull/1292))

 
### Known Issues

* Mismatch between post-processing implementation and the guiding requirements (DSO-8884)

* CPU utilization increases with Projector switched off (DSO-8040).

* Unity wrapper limited support for sensors (DSO-8666)
* Memory leak in the Unity wrapper ([#1477](https://github.com/IntelRealSense/librealsense/issues/1477))
* IR Right is selected as default stream  (DSO-8733)
* Snapshots stored by Depth Quality Tool are not aligned with Reports (DSO-8638)

* Realsense Viewer is not streaming after wake up from sleep mode (DSO-8094)
* Latency of 100ms (DSO-7745) - Will be fixed in a later FW release
* The Viewer and the visual examples CPU utilization is high, when streaming depth or color (DSO-7888)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)
* DQT angle is sometime displayed wrong (DSO-8388)
* Color correction parameters are not updated to the device when a setting file is loaded (DSO-8538)
* DQT - When the decimation filter is enabled the ROI window is offset, and the visualization changes to default when the ROI% is changed	(DSO-8740)

* [Firmware] Hardware timestamp on AWGT modules is not consistent across streams (DSO-8880)

* [MacOS] Setting controls is likely to return an exception, even when the control was applied successfully
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets

### Other Issues

* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)

* Some of the Depth Quality Tool (DQT) metrics will be modified in the next coming releases


## Release 2.10.2
March 22st, 2018

### API Changes 
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-2101-to-2102) from the previous 2.10.1 version

### New Features & Improvements

* Improvements to the `rs-terminal` utility [#1356](https://github.com/IntelRealSense/librealsense/pull/1356)
* Enabling to apply post-processing after spatial alignment ([#1278](https://github.com/IntelRealSense/librealsense/pull/1278))
* More comprehensive support for firmware error reporting ([#1403](https://github.com/IntelRealSense/librealsense/pull/1403))
* [Python] Fixing dead-lock in certain callbacks (DSO-8782)
* [Unity] Textured point-cloud implementation ([#1293](https://github.com/IntelRealSense/librealsense/pull/1293))
* [C#] Depth-Disparity processing block added ([#1307](https://github.com/IntelRealSense/librealsense/pull/1307))

### Bug Fixes
* Occasional frame drops from the fisheye camera on the AWGT modules (DSO-8628)
* Slow auto-exposure convergence rate on the AWGT modules (DSO-8853)
* GetBPP returning incorrect value when using software device ([#1377](https://github.com/IntelRealSense/librealsense/issues/1377))
* Better error message when no OpenGL driver is available (DSO-8545)

### Known Issues

* Mismatch between post-processing implementation and the guiding requirements (DSO-8884)

* CPU utilization increases with Projector switched off (DSO-8040).

* Unity wrapper limited support for sensors (DSO-8666)
* IR Right is selected as default stream  (DSO-8733)
* Snapshots stored by Depth Quality Tool are not aligned with Reports (DSO-8638)

* Realsense Viewer is not streaming after wake up from sleep mode (DSO-8094)
* Latency of 100ms (DSO-7745) - Will be fixed in a later FW release
* The Viewer and the visual examples CPU utilization is high, when streaming depth or color (DSO-7888)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)
* DQT angle is sometime displayed wrong (DSO-8388)
* Color correction parameters are not updated to the device when a setting file is loaded (DSO-8424)
* DQT - When the decimation filter is enabled the ROI window is offset, and the visualization changes to default when the ROI% is changed	(DSO-8740)

* [Firmware] Hardware timestamp on AWGT modules is not consistent across streams (DSO-8880)

* [MacOS] Changing resolution after first start & stop fails. Reconnect might be required
* [MacOS] Setting controls is likely to return an exception, even when the control was applied successfully
* [MacOS] File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets

> Some of the issues has been address in [#1452](https://github.com/IntelRealSense/librealsense/pull/1452) but are still being tested at the time of this release

### Other Issues

* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)

* Some of the Depth Quality Tool (DQT) metrics will be modified in the next coming releases

## Release 2.10.1
March 1st, 2018

### API Changes 
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-210.0-to-2101) from the previous 2.10.0 version

### New Features & Improvements
* Adding SIMD AVX2 implementation for YUYV to RGB decoding
* Kernel patches for Ubuntu LTS kernel 4.13 (DSO-8654)
* Updated DKMS debian package : 
    - Support for Ubuntu LTS kernels 4.4, 4.10 and 4.13.
    - Support for TM1 tracking device
    - Package name changed from `**realsense-uvcvideo**` to `librealsense2-dkms`
* Adding repeat capability for playback
* Allow to use JSON files with playback
* A new metadata attribute is available - Actual FPS - in use by syncer.

##### Examples
* Adding Presets example [Community contribution](https://github.com/SirDifferential/minimal_realsense2)

##### Library Improvements   
* Installation guides update for Linux and MacOS

##### Node.js
* Support npm installation on MacOs
* Enhancements and minor API changes
* Add sensor control example

##### Python
* Changing realsence to librealsence in the python wrapper

##### C#
* Add netstandard2.0 support to C# wrapper

##### Additional
* Integration of a contribution by @SirDifferential,  Jan Lukas Gernert and Sebastian Andraos.

### Bug Fixes
* **[Viewer]** Exposure control error raised when changing frame rate with 4 cameras connected (DSO-7775)
* **[Viewer]** Memory leak in sensor's open/close flow (DSO-8362)
* **[Viewer]** Color camera of D415 is reddish for face portrait(DS5U-1891)
* **[TM1]**  HID Custom Sensor fails on Cold Boot (DSO-8398)

### Known Issues
* CPU utilization increases with Projector switched off (DSO-8040).

* Unity wrapper limited support for sensors (DSO-8666)
* IR Right is selected as default stream  (DSO-8733)
* Snapshots stored by Depth Quality Tool are not aligned with Reports (DSO-8638)

* Realsense Viewer is not streaming after wake up from sleep mode (DSO-8094)
* Latency of 100ms (DSO-7745) - Will be fixed in a later FW release
* The Viewer and the visual examples CPU utilization is high, when streaming depth or color (DSO-7888)
  * In this release OpenMP compile flag is disabled by default, which can reduce the CPU utilization. Please refer to [#744](https://github.com/IntelRealSense/librealsense/issues/744)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)
* DQT angle is sometime displayed wrong (DSO-8388)
* Color correction parameters are not updated to the device when a setting file is loaded (DSO-8424)
* DQT - When the decimation filter is enabled the ROI window is offset, and the visualization changes to default when the ROI% is changed	(DSO-8740)

### Known Issues on Mac OS
We are ramping-up our support for Mac OS but unfortunately there are still several known-issues:
* Changing resolution after first start & stop fails. Reconnect might be required
* Setting controls is likely to return an exception, even when the control was applied successfully
* File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets

In addition, many users are reporting the camera identifying as USB2 (`device doesn't support depth streaming!` error), most likely due to cables / dongles combinations.

### Other Issues

* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)

* Some of the Depth Quality Tool (DQT) metrics will be modified in the next coming releases
* In Windows 10, automatic FW update is activated. In case needed to update a diferent FW version, please check the FW and the FW update tool for Windows at:  ([Windows* Device Firmware Update tool for Intel® RealSense™ D400 Product Family](https://downloadcenter.intel.com/download/27408/?v=t )).

## Release 2.10.0
February 8, 2018

### API Changes

[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-291-to-2100) from the previous 2.9.1 version

### New Features & Improvements

##### Examples
* Addes Post Processing Example (Tracked on DSO-8318)

##### Library Improvements   
* Added support to backend-timestamp on windows (related to latency optimizations, Tracked on DSO-8289)
* Removed redundant dependency of `Threads` package
* Improvements to temporal filter/ holes filling mode (Tracked on DSO-8523)
* Raw frame snapshot now use `.raw` extension instead of `.bin`
* Occlusion filter for Pointcloud from RGB and Depth streams (Tracked on DSO-8513)
* Added USE_SYSTEM_LIBUSB flag to CMake file

##### C++
* Adding `rs2::frameset::get_infrared_frame()`

##### Node.js
* Export to PLY
* Missing enums
* Tracking module support


##### Python
* Renamed `align.proccess` to `align.process`
* Binding for missing functions of `stream_profile`:
  * is_default
  * register_extrinsics_to

  Binding for `rsutil.h` projection related functions:
  * `rs2_deproject_pixel_to_point`
  * `rs2_transform_point_to_point`
  * `rs2_project_point_to_pixel`
  * `rs2_fov`
* Allow extrinsics and intrinsics creation and modification

##### Unity
* Initial integration with RealSense SDK 2.0
* Providing streams as textures

##### Additional
* [D400 Series Visual Presets](https://github.com/IntelRealSense/librealsense/wiki/D400-Series-Visual-Presets) Wiki page (Tracked on DSO-7102)
* Integration of community contributions by @BjarneHerland, @UnaNancyOwen, @OTL, @sh0

### Bug Fixes

* DSO-8308 : Undo 0.5 pixel offset when mapping pixel to texture coordinate
* Issue #1087: Linkage error when using `rs2_set_devices_changed_callback`
* Removed multiple `gcc` warnings.
* "Apple Mach-O Linkter (ld) Error" happens when it builds the targets which links glfw.
* Playback panel bug when no other device exists (did not show info icon)
* `Align` in .NET bug fix - no frames after ~10 frames
* Fixed an issue when device_id parameter wasn't actually selected the required device in rs-terminal tool.
* Prevent access to invalid data in v4l backend when trying to read the metadata size of an empty frames.
* Ignore duplicated advanced mode parameters
* Fix compilation under Gentoo
* Fixed memory leak issues
* Issue #1087: Python free() bug
* Fixed an issue with ColorCorrection parameters
* TM1 calibration update
* Enhancements and bug fixes in viewer
* Fix `stderr` redirection in the patch script

### Known Issues
* Realsense Viewer is not streaming after wake up from sleep mode (DSO-8094)
* Latency of 100ms (DSO-7745)
* The Viewer and the visual examples CPU utilization is high, when streaming depth or color (DSO-7888)
  * Disabling the OpenMP using CMake, can reduce the CPU utilization. Please refer to #744
* **[Viewer]** Exposure control error raised when changing frame rate with 4 cameras connected (DSO-7775)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)
* Memory leak when repeatedly closing and opening the device (DSO-8362)
* DQT angle is sometime displayed wrong (DSO-8388)
* Color correction parameters are not updated to the device when a setting file is loaded (DSO-8424)

### Known Issues on Mac OS
We are ramping-up our support for Mac OS but unfortunately there are still several known-issues:
* Changing resolution after first start & stop fails. Reconnect might be required
* Setting controls is likely to return an exception, even when the control was applied successfully
* File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets

In addition, many users are reporting the camera identifying as USB2 (`device doesn't support depth streaming!` error), most likely due to cables / dongles combinations.

### Other Issues

* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)

* Some of the Depth Quality Tool (DQT) metrics will be modified in the next coming releases
* In Windows 10, automatic FW update is activated. In case needed to update a diferent FW version, please check the FW and the FW update tool for Windows at:  ([Windows* Device Firmware Update tool for Intel® RealSense™ D400 Product Family](https://downloadcenter.intel.com/download/27408/?v=t )).

## Release 2.9.1
January 25, 2018

### API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-290-to-291) from the previous 2.9.0 version

### Prerequisites

* A new dependency package `libudev-dev` was added in 2.9.0 to the [installation for Linux OS](https://github.com/IntelRealSense/librealsense/blob/development/doc/installation.md#make-ubuntu-up-to-date) due to a custom `libusb` library that was employed in this release. 

Migration from previous versions requires `sudo apt-get install libudev-dev`

### New Features and Improvements

1. Updated Presets (both content and UX)
2. Improved Record / Playback UX, 
3. Intel® RealSense™ Tracking Module support
4. **[Viewer]** Depth legend (ruler)
5. Added new example: [measure](https://github.com/IntelRealSense/librealsense/tree/master/examples/measure)
6. Added functionality to preserve frames for longer processing
7. Added [Projection](https://github.com/IntelRealSense/librealsense/wiki/Projection-in-RealSense-SDK-2.0) chapter to the Wiki

### Bug Fixes
* rs-fw-logger is not deployed with 'make install' (DSO-8087)
* RGB-Depth texture mapping not aligned (DSO-8308)
* The value of RGB camera "Exposure" is incorrect in Win10 (DSO-8291)

### Known Issues
* Realsense Viewer is not streaming after wake up from sleep mode (DSO-8094)
* Latency of 100ms (DSO-7745)
* The Viewer and the visual examples CPU utilization is high, when streaming depth or color (DSO-7888)
  * Disabling the OpenMP using CMake, can reduce the CPU utilization. Please refer to #744
* **[Viewer]** Exposure control error raised when changing frame rate with 4 cameras connected (DSO-7775)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)
* Memory leak when repeatedly closing and opening the device (DSO-8362)
* DQT angle is sometime displayed wrong (DSO-8388) 
* Color correction parameters are not updated to the device when a setting file is loaded (DSO-8424)

### Known Issues on Mac OS
We are ramping-up our support for Mac OS but unfortunately there are still several known-issues: 
* Changing resolution after first start & stop fails. Reconnect might be required
* Setting controls is likely to return an exception, even when the control was applied successfully
* File-Open / File-Save dialogs are not available in the Viewer / DQT, preventing import of custom presets

In addition, many users are reporting the camera identifying as USB2 (`device doesn't support depth streaming!` error), most likely due to cables / dongles combinations. 

### Other Issues

* Display alignment of the GUI of the Viewer and the DQT can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)

* Some of the Depth Quality Tool (DQT) metrics will be modified in the next coming releases
* In Windows 10, automatic FW update is activated. In case needed to update a diferent FW version, please check the FW and the FW update tool for Windows at:  ([Windows* Device Firmware Update tool for Intel® RealSense™ D400 Product Family](https://downloadcenter.intel.com/download/27408/?v=t )).

## Release 2.9.0
January 2, 2018

### API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-283-to-290) from the previous 2.8.3 version

### Prerequisites
* A new dependency package `libudev-dev` was added to the [installation for Linux OS](https://github.com/IntelRealSense/librealsense/blob/development/doc/installation.md#make-ubuntu-up-to-date) due to a custom `libusb` library that was employed in this release.  
Migration from previous versions requires `sudo apt-get install libudev-dev`
### New Features and Improvements

* Allow Depth Post-Processing filters to operate in disparity domain (DSO-8162)
  * Please note that the Post Processing is enabled by default and increases the CPU utilization
* Rework on the output Panel in the Realsense Viewer (DSO-7197)
* Mac OS: making playback and record functional (DSO-4836) 
* Added API for point-cloud export to PLY [#862](https://github.com/IntelRealSense/librealsense/issues/862)
* Publish documentation for [building and running libralsense on Android](https://github.com/IntelRealSense/librealsense/blob/development/doc/android/Android.md)

### Bug Fixes
* Applied fix reducing multi-cam latency [#935](https://github.com/IntelRealSense/librealsense/issues/935).
* Pointcloude misalignment in 4K display laptop (DSO-7891)

### Known Issues
* Realsense Viewer is not streaming after wake up from sleep mode (DSO-8094)
* Realsense Viewer crash on switching Advanced mode - may be due to wrong installation/permission (DSO-8088)
* rs-fw-logger is not deployed with 'make install' (DSO-8087)
* Streaming two D415 devices on SKL system (DSO-7889)
* Latency of 100ms (DSO-7745)
* The Viewer and the visual examples CPU utilization is high, when streaming depth or color (DSO-7888)
  * Disabling the OpenMP in the makefile, can slightly reduce the CPU utilization. Please refer to [#744](https://github.com/IntelRealSense/librealsense/issues/744)
* **[Viewer]** Exposure control error raised when changing frame rate with 4 cameras connected (DSO-7775)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)

### Other Issues
* Display alignment issues can be fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)

## Release 2.8.3
8 Dec 2017

### API Changes
[API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-282-to-283) from the previous 2.8.2 version

### New Features and Improvements

* Adding Depth Post-Processing filters  
   * Temporal Moving average Filter (DSO-7393)  
   * Spatial Edge-preserving Domain Transform filter(DSO-7392)  
   * Decimation filter (DSO-7394)  
   The filters are integrated into **realsense-viewer** and **depth-quality** tools and appear under "Post-Processing" entry in the control panel.
* Add support for d4m device (D405) : enumeration, depth/IR streaming and controls.
* [PCL wrapper](https://github.com/IntelRealSense/librealsense/pull/854)
* [Additional OpenCV examples](https://github.com/IntelRealSense/librealsense/pull/853)
   * Latency  profiling tool.
   * Integrating Depth with Deep-Neural Network example
* **realsense-viewer**:
   * Pointcloud visualization with colorized depth.
   * Depth post-processing controls: toggle on/off; control filter parameters.
* Performance enhancements

### Bug Fixes
* Support for alignment of any stream to depth - [#858](https://github.com/IntelRealSense/librealsense/issues/858)
* Removing work-around for [#833](https://github.com/IntelRealSense/librealsense/pull/833) - D400 devices require FW v5.8.15 upgrade.
* Saving depth capture (PNG) doesn't save the image - Windows only (DSO-7875)
* **[depth-quality]** tool - Z-accuracy is shown when no GT is selected (DSO-7885)
* Distance calculation is not accurate when there is no plain target in the DQT (DSO-7866)
* Viewer doesn't automatically select the correct Depth stream (DSO-7764)

### Other related fixes
The 2 issues below are fixed with a graphics updated driver, please refer to: [Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)
* UX menu alignment issues with some platforms (DSO-7739)
* **[Viewer]** OpenGL tools and samples don't work with some types of Docking Stations(ThinkPad USB3.0 Pro) (DSO-6674)

### Known Issues
* Streaming two D415 devices on SKL system (DSO-7889)
* Pointcloude misalignment in 4K display laptop (DSO-7891)
* Latency of 100ms (DSO-7745)
* The Viewer and the visual examples CPU utilization is high, when streaming depth or color (DSO-7888)
  * Disabling the OpenMP in the makefile, can slightly reduce the CPU utilization. Please refer to [#744](https://github.com/IntelRealSense/librealsense/issues/744)
* **[Viewer]** Exposure control error raised when changing frame rate with 4 cameras connected (DSO-7775)
* GUI - The Output Viewer window doesn't show the bottom notifications (DSO-7197)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)

### Prerequisites
* **[Firmware]** D400 Firmware Version 5.8.15 is required as the software w/a for v5.8.14 has been removed.





## Release 2.8.2
21 Nov 2017

### API Changes
N/A

### New Features and Improvements

* [Depth Quality Tool](https://github.com/IntelRealSense/librealsense/tree/development/tools/depth-quality) enhancements:  
Replace AVG metric with Plane fit RMS  
Refactor implementation of Z-Accuracy metric to use the rectified depth.

* Adding USB2 support for selected D400 models (DSO-6814)
* Python [example](https://github.com/IntelRealSense/librealsense/blob/v2.8.2/wrappers/python/examples/align-depth2color.py) for Depth2Color registration
* Librealsense with Raspberry Pi platform [tutorial](https://github.com/IntelRealSense/librealsense/blob/v2.8.2/doc/RaspberryPi3.md)
* [LabView](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/labview) wrapper was added

### Bug Fixes
* **Windows OS** Librealsense fails to recognize devices with DMFT installed (DSO-6345)
* **Linux** FPS drops to 50% when streaming RGB formats (DSO-7183)
* Fix left2right stereo imagers extrinsic calculation
* Fixed realsense-viewer crash when running on a PC with no display attached
* Improve frames synchronization flow in the viewer
* Fixed an issue when rs-depth-quality tool crashing as a result of clicking on the window close button
* Added an appropriate message on rs-depth-quality tool when a camera is used by another application.
* Fixed an issue when loading a JSON file failed with unrecognized fields.
* Fixed an issue when using LRS_LOG_LEVEL environment variable didn't enforce the creation of log file
* Fixed an issue on rs-fw-logger tool when 'wait_for_device()' throws an exception
* **Python** add missing initializer in pointcloud demo
* Fixed Firmware issue (ver 5.8.14): Sometimes when RGB and Stereo resolutions are at FHD-HD, the RGB camera streaming stops and doesn't return even after turning the Depth Stereo to Off (DSO-6894)
* Windows - device disconnect events are sometimes not reported (DSO-6813)
* The Viewer and the visual examples CPU utilization is high, when no stream is activated (DSO-7224)
* Depth Quality Tool gets stuck - FPS alert after a few min run (DSO-7859)

### Known Issues
* Saving depth capture doesn't save the image - Windows only (DSO-7875)
* **[DQT]** - Z-accuracy is shown when no GT is selected (DSO-7885)
* UX menu alignment issues with some platforms (DSO-7739)
* Pointcloude misalignment in 4K display laptop (DSO-7891)
* Latency of 100ms (DSO-7745)
* Viewer doesn't automatically select the correct Depth stream (DSO-7764)
* The Viewer and the visual examples CPU utilization is high, when streaming depth or color (DSO-7888)
* Depth data snapshot issue on Windows (DSO-7875)
* Windows - Soft stability issue: start-stop test hangs when RGB and Depth running together after hundreds of cycles (DSO-6930)
* **[Viewer]** Exposure control error raised when changing frame rate with 4 cameras connected (DSO-7775)
* **[Viewer]** OpenGL tools and samples don't work with some types of Docking Stations(ThinkPad USB3.0 Pro) (DSO-6674)
* GUI - The Output Viewer window doesn't show the bottom notifications (DSO-7197)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)
* Distance calculation is not accurate when there is no plain target in the DQT (DSO-7866)

### Limitations
* **[Firmware]** Version 5.8.14 is required to run Advanced mode assignments (DSO-7649)


## Release 2.8.1
1 Nov 2017

> [API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-280-to-281) from previous release

### New Features and Improvements

* [Depth Quality Tools](https://github.com/IntelRealSense/librealsense/tree/development/tools/depth-quality) now includes Z-Accuracy metric based on ground-truth (DSO-6434)
* librealsense CI now includes recorded test cases for the 4 major supported lines of devices - SR300, D415, D435 and other engineering models (DSO-7101)
* New example added showcasing the [Sensor API](https://github.com/IntelRealSense/librealsense/tree/master/examples/sensor-control) (DSO-7016)
* Set of new examples added showcasing working with [C API](https://github.com/IntelRealSense/librealsense/tree/master/examples/C) (DSO-6909)
* Added Python example for working with [D400 Advanced Mode](https://github.com/IntelRealSense/librealsense/blob/master/wrappers/python/python-rs400-advanced-mode-example.py) (DSO-7287)
* Added depth colorization options to the Viewer (and the API) (DSO-7150)

### Bug Fixes
* **[Firmware]** When Advance Mode is changed, the camera requires sometimes to disconnect/reconnect (DSO-7015)
* Pipeline fails to choose the correct device when several devices are connected (DSO-7366)
* When requesting 2 streams (such as color and depth) only one frameset is returned in the pipeline, instead of the 2 synchronized streams. (DSO-7202)

### Known Issues
* **[Viewer]** OpenGL tools and samples don't work with some types of Docking Stations(ThinkPad USB3.0 Pro) (DSO-6674)
* Windows - device disconnect events are sometimes not reported (DSO-6813)
* Windows - Soft stability issue: start-stop test hangs when RGB and Depth running together after hundreds of cycles (DSO-6930)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)
* GUI - The Output Viewer window doesn't show the bottom notifications (DSO-7197)
* Linux - When using IR format that is different than UYVY, the FPS drops to half (DSO-7183)

### Limitations
* **[Firmware]** Sometimes when RGB and Stereo resolutions are at FHD-HD, the RGB camera streaming stops and doesn't return even after turning the Depth Stereo to Off (DSO-6894)

## Release 2.8.0
11 Oct 2017

> [API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-279-to-280) from previous release

### New Features and Improvements

* [Depth Quality Tools](https://github.com/IntelRealSense/librealsense/tree/development/tools/depth-quality) is now available
* Improved pipeline architecture

### Bug Fixes
* rs-data-collect example fails to execute
* **[Viewer]** - Some of the Advance Mode parameters are not updated properly

### Known Issues
* **[Viewer]** OpenGL tools and samples don't work with some types of Docking Stations(ThinkPad USB3.0 Pro) (DSO-6674)
* Windows - device disconnect events are sometimes not reported (DSO-6813)
* Windows - Soft stability issue: start-stop test hangs when RGB and Depth running together after hundreds of cycles (DSO-6930)
* When requesting 2 streams (such as color and depth) only one frameset is returned in the pipeline, instead of the 2 synchronized streams (DSO-7202)
* Changing the gain value while Auto Exposure (AE) is enabled disables AE, this requires manually enabling AE (DSO-6853)
* Linux - When using IR format that is different than UYVY, the FPS drops to half (DSO-7183)
* The Viewer CPU utilization is high, even when no stream is activated (DSO-7224)
* GUI - The Output Viewer window doesn't show the bottom notifications (DSO-7197)

### Limitations
* **[Firmware]** When Advance Mode is changed, the camera requires sometimes to disconnect/reconnect (DSO-7015)
* **[Firmware]** Sometimes when RGB and Stereo resolutions are at FHD-HD, the RGB camera streaming stops and doesn't return even after turning the Depth Stereo to Off (DSO-6894)

## Release 2.7.9
17 Sep 2017

> [API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-277-to-279) from previous release

### New Features And Improvements
* Preliminary [node.js](https://github.com/IntelRealSense/librealsense/tree/development/wrappers/nodejs) integration
* Preliminary [ROS](https://github.com/intel-ros/realsense/releases/tag/2.0.0) integration
* Additional Presets for all resolutions

### Bug Fixes
* **[API]** Color Auto-Exposure Priority Control not available - [RS2_OPTION_AUTO_EXPOSURE_PRIORITY](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L54) was added (DSO-6971)
* **[Viewer]** Support for older versions of serialized settings files (DSO-6677, 6785)
* **[Viewer]** UI scaling on 4K displays (DSO-6817)
* Disable auto-exposure when modifying exposure / gain manually (DSO-6237)
* Save settings file includes the preset (DSO-6785)

### Known Issues
* **[Viewer]** OpenGL tools and samples don't work with some types of Docking Stations (DSO-6674)
* On Windows, device disconnect events are sometimes not reported (DSO-6813)
* rs-data-collect example fails to execute

### Limitations
* **[Firmware]** When Advance Mode is changed, the camera requires sometimes to disconnect/reconnect (DSO-7015)
* **[Firmware]** Sometimes when RGB and Stereo resolutions are at FHD-HD, the RGB camera streaming stops and doesn't return even after turning the Depth Stereo to Off (DSO-6894)
