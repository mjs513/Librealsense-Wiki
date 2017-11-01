## Release 2.8.1
1 Nov 2017

> [API changes](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#from-280-to-281) from previous release

TBD

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
