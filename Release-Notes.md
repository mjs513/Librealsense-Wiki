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
* Fix export to PNG.
* Support for alignment of any stream to depth - [#858](https://github.com/IntelRealSense/librealsense/issues/858)
* Removing work-around for [DSO-7649](https://github.com/IntelRealSense/librealsense/pull/833) - D400 devices require FW v5.8.15 upgrade.
* Saving depth capture doesn't save the image - Windows only (DSO-7875)
* **[depth-quality]** tool - Z-accuracy is shown when no GT is selected (DSO-7885)
* Distance calculation is not accurate when there is no plain target in the DQT (DSO-7866)

### Other related fixes
The 2 issues below are fixed with a graphics updated driver, pelase refer to:[Intel® Graphics Driver for Windows* [15.60]](https://downloadcenter.intel.com/download/27266/Graphics-Intel-Graphics-Driver-for-Windows-15-60-?product=80939)
* UX menu alignment issues with some platforms (DSO-7739)
* **[Viewer]** OpenGL tools and samples don't work with some types of Docking Stations(ThinkPad USB3.0 Pro) (DSO-6674)

### Known Issues
* D4m device not recognized on startup (DSO-7883)
* Streaming two D415 devices on SKL system (DSO-7889)
* Depth-quality tool: invalid UI selections (DSO-7884)

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
