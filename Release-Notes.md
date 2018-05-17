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
* librealsense CI now includes recorded test cases for the 4 major supported lines of devices - SR300, D415, D435 and D460 (DSO-7101)
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
