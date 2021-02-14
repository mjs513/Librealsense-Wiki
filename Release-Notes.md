## Release 2.42.0
Release Date: 14 Feb 2021

### API Changes
https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2420

### Android Releases - User Notification
The Android Distribution Center has been transferred from `bintray.com` to `jfrog` servers starting from Feb 1st.
The [previously available server](https://dl.bintray.com/intel-realsense/librealsense) is not accessible since Jan 24th.
The official releases of the Android apk and Java library can be browsed with `https://egiintel.jfrog.io/artifactory/librealsense/com/intel/realsense/librealsense`  
See [#8280](https://github.com/IntelRealSense/librealsense/pull/8280) for details.  
Note that with the new server is hosting SDK releases v2.41.0+ only. Transfer of older releases is envisioned but not prioritized.

### New Features
* [#8350](https://github.com/IntelRealSense/librealsense/pull/8350) - **[L515] FW update v1.5.4.1**  (RS5-10444) 
* [#8345](https://github.com/IntelRealSense/librealsense/pull/8345) - **[D400] FW update v5.12.11.0**
   - Max time limit for IR sensors (DSO-12884)
   - Customer enhancements (DSO-15098).
* [#8036](https://github.com/IntelRealSense/librealsense/pull/8036) - **[UE] Unreal Engine wrapper is converted to UE4.26**  
This changes makes _unrealengine4_ wrapper to be build against Unreal Engine 4.26 and _introduces some breaking changes_ for engines less than v4.26 according to a new UE API.
* [#8281](https://github.com/IntelRealSense/librealsense/pull/8281) - **[API] Enable rolling log files**  
   Continues the work of @aseelegbaria ([#8212](https://github.com/IntelRealSense/librealsense/issues/8212)
   Log files can have a max size. upon reaching max size new file will be created and current file will be truncated.  
   (RS5-9271)
* [#8211](https://github.com/IntelRealSense/librealsense/pull/8211),[#8240](https://github.com/IntelRealSense/librealsense/pull/8240) - **[SDK] CMake Build transition to HTTPS**  
Librealsense Cmake Build requires downloading and bundling FW images from external server. Starting with v2.42.0 the actual downloads will be queried using Secure Access (https).  
The new resource URLs are retrofitted into CMake and the source tree documentation.  
(DSO-16368, DSO-16444)  
Fix FW download link url in Realsense-viewer (RS5-8513) 
* [#8220](https://github.com/IntelRealSense/librealsense/pull/8220) - **[D400] Auto-Exposure and Gain max limits for IR sensors.**  
The new APIs set the effective upper bound for Exposure and Gain values for Depth Auto-Exposure. This allows to control and limit the changes in FPS rate while enabling for AE auto-adjustments.  
Requires FW5.12.11.0 or later.
* [#8029](https://github.com/IntelRealSense/librealsense/pull/8029) - **[MacOS] IMU data processing via HIDAPI on MacOS**  
   Support of IMU accelerometer and Gyro data on MacOS.  
   s_hid_device class was modified to receive the IMU data via HIDAPI library functions on Mac OS.  
(RS5-9285, RS5-8852, possibly RS5-9121) by [@sokolov19830711](https://github.com/sokolov19830711)
* [#8063](https://github.com/IntelRealSense/librealsense/pull/8063) - **[Core] -Reset logger**
Stop and reset reset logger on demand to cope with huge log files. (RS5-9270)

### Bug Fixes and Enhancements

* [#8289](https://github.com/IntelRealSense/librealsense/pull/8289) - **[DQT] Fix L515 handling in Custom Mode **  
In custom mode we need to update the sensor with sensor mode before start.
* [#8072](https://github.com/IntelRealSense/librealsense/pull/8072) - **[Unity] using SafeHandle in Context class**  
Context class with CriticalFinalizerObject and CER implementation.  
(DSO-13740)
* [#8002](https://github.com/IntelRealSense/librealsense/pull/8002) - **[L515] Remove default preset**  
   1. **Remove default preset**
      -  on LRS start up we calculate if we are in one of the presets and if not we are on custom
      - when loading old Json file if the preset is default the preset will be custom
      - if user try to set preset default he will get an error.
   2. **Reading of defaults values** 
      - on new fw versions( >1.5.3.0) is by get_default command
      - on old fw versions its stay as it was - set_current -1 and than get_current gives the defaults values
   3. **update defaults values of hw options on the following cases**
      - on startup 
      - when changing resolution 
      - when changing gain
   4. **Flow of set preset**
      - set gain according to preset
      - read the default values 
      - set default values to currents
      - set laser according to preset  
(RS5-8999)
* [#8261](https://github.com/IntelRealSense/librealsense/pull/8261) - **[Android] Remove (L515) Confidence stream from settings**  (RS5-8989)
* [#8262](https://github.com/IntelRealSense/librealsense/pull/8262) - **[L515] Deprecate Zero-Order option** (RS5-10182) 
* [#8252](https://github.com/IntelRealSense/librealsense/pull/8252) - **[Core] Fix GCC 5 error/warnings in HDR demo**  
* [#8234](https://github.com/IntelRealSense/librealsense/pull/8234) - **[Linux] Revert "Switch v4l to use memory-mapped files instead of userptr."**  
   Use of mmap leads to sporadic segfault on stream close/frames release.  
   Switch back to user-allocated buffers for v4l data exchange.  
   Addresses [#8154](https://github.com/IntelRealSense/librealsense/issues/8154).  
   (DSO-16453)
* [#8245](https://github.com/IntelRealSense/librealsense/pull/8245) - **[Live555] Fix build_with_network CMake option and other workarounds**  
   - liveMedia update - liveMedia has been upgraded by live555 in 2021-jan-21.   Available as an archive from server only.
   - A workaround for wrong default value about RS2_OPTION_POWER_LINE_FREQUENCY.
   - A workaround for bad parameter when create frame object in Y8 format with network mode.
   - add 'add_to' method for net_device in python wrapper.
* [#8048](https://github.com/IntelRealSense/librealsense/pull/8048) - **[EasyLogging] - add asynchronous handling (Linux)**  
   Handling log messages asynchronously to reduce latencies.  
   ( DSO-16295)
* [#8180](https://github.com/IntelRealSense/librealsense/pull/8180) - **[L515] Frames Filter unit-tests**
   Check that IR frames do not arrive to the user callback if not specifically asked for.  
   (RS5-10249)
* [#8206](https://github.com/IntelRealSense/librealsense/pull/8206) - **[Viewer] Fix FW update exception showed after entering update state**  
   On FW update window we see a recoverable exception string during the FW update process. This PR fixes this behaviour.
   Actions taken:  
   1. Add delay between sending the device command to enter update state and query devices (if we do it too fast we still get the device before it was able to disconnect)
   2. Replace FW update UI exception with log exception  
   (RS5-7900)
* [#8176](https://github.com/IntelRealSense/librealsense/pull/8176) - **[Python] Integrate pybind11 V2.6.1 + replace pybind11 files with clone action**  
   - Clone pybind11  instead of keeping pybind files inside librealsense2 repo  
   - Update pybind version 2.2.1 -> 2.6.1  
   (RS5-9118)
* [#8159](https://github.com/IntelRealSense/librealsense/pull/8159) - **[Examples] HDR demo overhaul**
   - Review and refactoring both in Documentation and in Code.
   - Handle Mosaic View to present stacked frames.
   - Add HDR-specific controls
* [#7661](https://github.com/IntelRealSense/librealsense/pull/7661) - **[L500] Age-update implemented for projection**  (The age is now updated in the DSM on setup.
When AC is run the Age and last AC fields in DSM are updated, the fields that involve the MC are not changed.
* [#8182](https://github.com/IntelRealSense/librealsense/pull/8182) - **Unit-tests fixes**  
   Change the default directory for test logs to build/unit-tests instead of build.  
   Remove from the printing of the call stack when check fails the printing of the calls to the functions inside `test.py`
* [#8142](https://github.com/IntelRealSense/librealsense/pull/8142) - **[Core] Memory Leaks fixes**  (Fixes some memory leaks:
   - In the Linux backend, the deleter of a `std::unique_ptr` didn't call `delete`;
   - The `hdr_config` type and its sensor were holding mutual shared pointers to each other, causing them to not be deleted;
   - In `synthetic-stream.cpp`, the `on_set` method is called on a `ptr_option`, which stores the function passed to that method. However, the lambda passed captures the shared pointer, giving another shared pointer loop.) contributed by [@Rheel17](https://github.com/Rheel17)
* [#8066](https://github.com/IntelRealSense/librealsense/pull/8066) - **[Examples] - rs-kinfu**
   Place OMP pragma before for statement in rs-kinfu app.   Fixes [#5776](https://github.com/IntelRealSense/librealsense/issues/5776). Contributed by [@PeterBowman](https://github.com/PeterBowman)
* [#8084](https://github.com/IntelRealSense/librealsense/pull/8084) - **[Open3D] wrapper examples and tutorial**  
This PR adds a tutorial and some examples for using RealSense devices through the new Open3D wrapper. contributed by [@ssheorey](https://github.com/ssheorey)
* [#8162](https://github.com/IntelRealSense/librealsense/pull/8162) - **[Unit-Tests] Add run-unit-tests delay after acroname reset; add --stdout, --asis**
* [#8145](https://github.com/IntelRealSense/librealsense/pull/8145) - **[Unit-Tests] - Acroname controls in unit-tests**  Disable unit-tests in Travis Linux static build -- the Python version there misbehaved with ModuleNotFoundError and it was to be removed eventually anyway.
* [#8151](https://github.com/IntelRealSense/librealsense/pull/8151) - **[Core] fix realsense2-compression & realsense2-net plugin**
Follow up on [#8141](https://github.com/IntelRealSense/librealsense/pull/8141)  
* [#8141](https://github.com/IntelRealSense/librealsense/pull/8141) - **[Core] amendments**
   `src` removed from include directories of projects that do not need it.
* [#8127](https://github.com/IntelRealSense/librealsense/pull/8127) - **[D400] Detect IMU type (BMI-085 or BMI-055) regardless of device type.**
   - This PR allows the device to set the correct accel frame rate based on the IMU type, instead of the device type.  
   - Requires FW 05.12.10.0 or later.
   - `rs-imu-calibration.py` was tested using this PR in Ubuntu 16.04.  
(DSO-16367)
* [#8135](https://github.com/IntelRealSense/librealsense/pull/8135) - **[Unity] Add log creation**
 Add a `-logFile` parameter to unity export package command for investigation failures
* [#8105](https://github.com/IntelRealSense/librealsense/pull/8105) - **[Unit-Tests] updates**  (RS5-9997)
* [#8133](https://github.com/IntelRealSense/librealsense/pull/8133) - **[Examples] Correcting compression labels in rosbag-inspector tool**  (Compression labels displayed in the tool are swapped) contributed by [@matbb](https://github.com/matbb)
* [#8131](https://github.com/IntelRealSense/librealsense/pull/8131) - **[Python] python subprocess invocation using same python exe**
* [#8061](https://github.com/IntelRealSense/librealsense/pull/8061) - **[L515] IR Reflectivity - hide until value stabilized**  (RS5-9613)
* [#8109](https://github.com/IntelRealSense/librealsense/pull/8109) - **[SDK] REmove redundant Include directories from CMake**
   There was a misuse of the include_directories function where the first argument was a project name. This function should only get the wanted directories as parameters.
   (RS5-9747)
* [#8087](https://github.com/IntelRealSense/librealsense/pull/8087) - **[L515] correct display of advanced controls + UI setting when switching devices**  
   - Fix querying advanced controls with the wrong sensor mode.
   - Fix restoring UI controls from different device
   (RS5-9466)
* [#8073](https://github.com/IntelRealSense/librealsense/pull/8073) - **[Core] Retrofit changes from v2.41 into Development**
* [#8071](https://github.com/IntelRealSense/librealsense/pull/8071) - **[Core] Fix GCC 7.0 compilation error**
* [#8064](https://github.com/IntelRealSense/librealsense/pull/8064) - **[Unit-Tests] enhancements**
   - set-option unit-test fix & bug fix in test.info
   - abort test in case of exception   
   (RS5-9850)
* [#7781](https://github.com/IntelRealSense/librealsense/pull/7781) - **[Examples] Wrap Viewer/DQT error pop up text**
   The error pop up text on Viewer and DQT application is not wrapped, It use a ImGui::InputTextMultiline because the input text is dynamic.
   For static text we can use ImGui API - "ImGui::PushTextWrapPos / ImGui::PopTextWrapPos ".
   (RS5-9465)
* [#8050](https://github.com/IntelRealSense/librealsense/pull/8050) - **[L515] IR Reflectivity - move setting**  
   IR reflectivity option moved to configuration section at the DQT application.  
   (RS5-9612)
* [#8052](https://github.com/IntelRealSense/librealsense/pull/8052) - **[CI] Revert change on Linux parallel build**  
   - Travis CI currently allow VM with 2 cores.
   - Using -j$(($(nproc)-1)) disabled the parallel build on Linux builds.This PR revert this change
* [#8051](https://github.com/IntelRealSense/librealsense/pull/8051) - **[Unit-Tests] fix**  
   Fix unit-test failure and add info for the test. (RS5-9850)
* [#8023](https://github.com/IntelRealSense/librealsense/pull/8023) - **[PyBackend] fix**  
   Deadlock occurs when HID callback invokes from multi-threads
* [#8041](https://github.com/IntelRealSense/librealsense/pull/8041) - **[Unit-Tests] - test.info** (RS5-9754)
* [#7895](https://github.com/IntelRealSense/librealsense/pull/7895) - **[Unit-Tests] serializable_device preset bug fix & unit-test**  
   Added a test for serializable device json serialize and load
   Also changed load_json in l500-serializable so it works with the presets.  (RS5-9630)
* [#8016](https://github.com/IntelRealSense/librealsense/pull/8016) - **[Unit-Tests] Fixed test-FG - remove 1280x720 resolution**  
   Remove test "streaming FG 1280x720". FW support only 800x600 resolution on FG.  (RS5-9894)
* [#8000](https://github.com/IntelRealSense/librealsense/pull/8000) - **[Unit-Tests] frame drops after set_option**  Unit-tests to check if there is any frame drops after set_option in Windows and Linux. (RS5-9850)

### Documentation
* [#8280](https://github.com/IntelRealSense/librealsense/pull/8280) - **[Android] repo updated in java_example and native_example** (DSO-16496)
* [#8238](https://github.com/IntelRealSense/librealsense/pull/8238) - **Tensorflow fix**  Fixed URL in part 3.

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable. (DSO-13700)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) v2.33.1 does not compile with -DBUILDEASYLOGGINGPP=OFF
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-13525) - [D400] 3D viewer moved when sliding the tare calibration sliders


## Release 2.41.0
Release Date: 27 Dec 2020

### API Changes
https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2410


### New Features
* [#7802](https://github.com/IntelRealSense/librealsense/pull/7802) - **[D400] FW Update - 5.12.10.0**
    - Bug fixes and improvements
* [#7808](https://github.com/IntelRealSense/librealsense/pull/7808) - **[L515] FW Update - 1.5.3.0**
    - Bug fixes
* [#7851](https://github.com/IntelRealSense/librealsense/pull/7851) - **[OpenVINO]** Compatibility to both 2019/2020 versions of the openVINO was added.
  Compatibility for 2019 and 2020 versions of the openVINO for the openVINO wrapper examles and realsense-viewer has been added. Addresses [6127](https://github.com/IntelRealSense/librealsense/issues/6127).  

### Bug Fixes and Enhancements
* [#7983](https://github.com/IntelRealSense/librealsense/pull/7983) - **[Linux]** Kernel 5 improvements:  
  Changes in v4l backend implementation applicable for Kernels 4.16+ only:
  - v4l backend - use multiplexing to handle metadata and video payloads
  - Modify UVC_URBs from 5 to 16 to mitigate frame drops in uvcvideo
  - Minor enhancement in manual patching script
  - Frame drops unit-test refactoring  
* [#8005](https://github.com/IntelRealSense/librealsense/pull/8005) - **[Linux]** Fix for video buffers guard
* [#7993](https://github.com/IntelRealSense/librealsense/pull/7993) - **[Network Device]** Update rs-server to the latest Live555.
* [#7977](https://github.com/IntelRealSense/librealsense/pull/7977) - **[Android]** Enabled advanced mode is not supported  
  Display the advanced mode option only when it's actually supported. (RS5-8619)
* [#7911](https://github.com/IntelRealSense/librealsense/pull/7911) - **[D400]** Emitter On /Off and Emitter Always On enabling together avoided (DSO-16064)
* [#7938](https://github.com/IntelRealSense/librealsense/pull/7938) - **[D400]** On-Chip Calibration  - Focal Length Enhancements  
* [#7915](https://github.com/IntelRealSense/librealsense/pull/7915) - **[D400]** On-Chip Calibration support for csharp wrapper
  Add on-chip calibration call in csharp wrapper.) contributed by [@mengyui](https://github.com/mengyui)
* [#7535](https://github.com/IntelRealSense/librealsense/pull/7535) - **[D400]** On-Chip Calibration - Focal Length calibration and merged Tare Ground Truth.
  Added on-chip focal length calibration and merged tare ground truth
* [#7872](https://github.com/IntelRealSense/librealsense/pull/7872) - **[L515]** IR Reflectivity report at 15% resolution  
  IR Reflectivity resolution changes to 15% increments.
  Add `stabilized_value` utility class and use it to smooth low-rate changes to the output value. (RS5-9611)  
* [#7759](https://github.com/IntelRealSense/librealsense/pull/7759) **[SDK]** Convert frame to frameset in post processing filters. Make allocations consistent for all processing blocks. Addresses [#7584](https://github.com/IntelRealSense/librealsense/issues/7584) (DSO-15250)
* [#7339](https://github.com/IntelRealSense/librealsense/pull/7339) - **[Linux]** Update packages error.  
  A solution to issue [#5092](https://github.com/IntelRealSense/librealsense/issues/5092).   
  error : E: Unable to locate package libdrm-amdgpu1-dbg
  I ran `apt-cache search libdrm-amdgpu1-dbg` and it returned libdrm-amdgpu1-dbgsym and libdrm-amdgpu1.  
  Contributed by [@bestaps](https://github.com/bestaps)
* [#7774](https://github.com/IntelRealSense/librealsense/pull/7774) - **[SDK]** input to `try_parse` ROS record method updated** (DSO-16068)  
* [#7931](https://github.com/IntelRealSense/librealsense/pull/7931) - **[MacOS]** IMU was temporarily switched off on Mac OS  Processing of IMU data was temporarily switched off in case of Mac OS usage to prevent the viewer and examples applications crash. Contributed by [@sokolov19830711](https://github.com/sokolov19830711)
* [#7878](https://github.com/IntelRealSense/librealsense/pull/7878) - **[PCL]** Fixes  
  Introduce cmake flag.  
  Add try-catch for main function of pcl-color example.
  Contributed by [@manson](https://github.com/manson)
* [#7876](https://github.com/IntelRealSense/librealsense/pull/7876) - **[PCL]** Fix wrapper building
  Searching procedure for headers and libs of the GLFW libriary was modified for using with the internal version of GLFW. Contributed by [@sokolov19830711](https://github.com/sokolov19830711)
* [#7885](https://github.com/IntelRealSense/librealsense/pull/7885) - **[L515]** Fix error during AC when alt-IR isn't available
* [#7887](https://github.com/IntelRealSense/librealsense/pull/7887) - **[OpenCV]** rotate point cloud example was added. Contributed by [@Allius27](https://github.com/Allius27)
* [#7881](https://github.com/IntelRealSense/librealsense/pull/7881) - **[libusb]** Work-around for libusb breaking changes in Master branch (v1.0.24)
* [#7836](https://github.com/IntelRealSense/librealsense/pull/7836) - **[Python]** Add `run-unit-tests.py` ability to run tests by name  
* [#7842](https://github.com/IntelRealSense/librealsense/pull/7842) - **[Network Device]** Fix for the API usage removed bythe new version of Live555. 
* [#7854](https://github.com/IntelRealSense/librealsense/pull/7854) - **[L515]** Parse additional HW error types.  
  Added additional "Fatal Errors" 18-24. (RS5-9443)
* [#7741](https://github.com/IntelRealSense/librealsense/pull/7741) - **[L515]** Added unitests for alt-IR:
    - Sanity test.
    - Check that AC fails if AltIR was enable before stream start.
    - Check that AC fails if AltIR was enable after stream start.)(RS5-9423)
* [#7812](https://github.com/IntelRealSense/librealsense/pull/7812) - **[Python]** pybind linux - Fix missing debug symbols in RelWithDebug mode.
  The output binary .so file of building pyrealsense2 on Linux and on configuration RelWithDebInfo do not contain debug symbols.
  It was caused due to a known issue with pybind11 version 2.2.1 that is used in librealsense SDK.
  The issue was fixed at [PR1892](https://github.com/pybind/pybind11/pull/1892/files) at pybind11 repo.  
  Linux python 2.7 wheel size before this changes is : ~10 [MB]  
  Linux python 2.7 wheel size after this changes is : ~70 [MB]  
* [#7835](https://github.com/IntelRealSense/librealsense/pull/7835) - **[Python]** stream_profile stream/format output now uses to_string()  
* [#7794](https://github.com/IntelRealSense/librealsense/pull/7794) - **[Unity]** For the L515 device, disabled processing blocks in the `PointCloudProcessingBlocks` scene, except for Temporaral Filter) contributed by [@SergeySPF](https://github.com/SergeySPF)
* [#7840](https://github.com/IntelRealSense/librealsense/pull/7840) - **Fix get_stream_profiles()**
* [#7833](https://github.com/IntelRealSense/librealsense/pull/7833) - **[Java]** Download firmware image file for l500  
  Add missing enum to Java wrapper (RS5-9606)
* [#7832](https://github.com/IntelRealSense/librealsense/pull/7832) - **[Git]** fix merge issue  
  Fix merge from `master` issue of duplicate code
* [#7818](https://github.com/IntelRealSense/librealsense/pull/7818) - **[Git]** Retrofit Development branch with 2.40.0 changes  
* [#7796](https://github.com/IntelRealSense/librealsense/pull/7796) - **L500]** Support for `FG` with debug_stream_sensor    Added API function `get_debug_stream_profiles()` that returns the list of debug formats  (FG).
  The debug format will not be available through the `sensor::get_stream_profiles()` API.
  Added support for python wrapper.
  Added unit tests on python.

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable. (DSO-13700)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) v2.33.1 does not compile with -DBUILDEASYLOGGINGPP=OFF
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-13525) - [D400] 3D viewer moved when sliding the tare calibration sliders
* (RS5-7374) - [L515] Error after performing HW reset
* (DSO-15118) - [D400] Viewer is closed forcibly with cycling start/stop streaming in 3D view.

## Release 2.40.0
Release Date: 18 Nov 2020

**Ubuntu 20 LTS and Ubuntu 18 LTS with kernel 5 known issue**:  
We encountered high level of frame drops with several consecutive, compared to Ubuntu16/Kernel 4.  
Streaming Librealsense with Kernel 5 results in a higher frame drop rate that is intensified by consecutive frame drops, mostly between 2-4 frames in a row, reaching 7 frames in certain cases.  
The recurrence rate at which the drops appear is affected by CPU and resources utilization:  
-	For streaming Depth at VGA resolution, the frame drops may occur in intervals of 5-30 min.  
-	Streaming Depth+IR+RGB+IMU the frame drops will appear within 1-3 minutes.  
-	IMU-enabled devices, such as D435i, D455 and L515 encounter higher rate of frame drops compared to D415 and D435.  

Kernel 5 is currently the backbone of Ubuntu 18 and Ubuntu20, thus the issue would affect most users of those versions.  
Note that the frame drops issue is confirmed in Ubuntu LTS 18 and 20, and it does not affect Ubuntu16 with LTS kernel 4.4.  

<ins>Mitigation Plan and Alternatives</ins>  
Realsense support team is working to resolve the issue on SDK and OS levels, and while the investigation is ongoing, one recommended method to mitigate this is by compiling and running Librealsense SDK with RSUSB backend - 
(`cmake .. -DFORCE_RSUSB_BACKEND`).  
The main limitation of RSUSB backend is that it is not suited for multi-cam scenarios. But whenever applicable - using RSUSB backend allows to bypass the Video4Linux kernel APIs and communicate with the device using generic USB driver.  
Switching to RSUSB backend provides a mitigating for sequential frame drops.  

### API Changes
https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2400


### New Features
* [#7802](https://github.com/IntelRealSense/librealsense/pull/7802) - **[D400] FW Update - 5.12.9.0**
    - Bug fixes
    - Suppportfor DFU counter reset
* [#7808](https://github.com/IntelRealSense/librealsense/pull/7808) - **[L515] FW Update - 1.5.2.0**
    - Bug fixes
    - Alternate IR option

* [#7675](https://github.com/IntelRealSense/librealsense/pull/7675) - **[L500] Add reflectivity estimator to Depth Quality Tool**  
    Calculates and provides LiDAR reflectivity estimation.
    - Add "RS2_NOISE_ESTIMATION" option  
    - Add "RS2_ENABLE_IR_REFLECTIVITY" option  
    - Add reflectivity algorithm class  
    - Add display at the DQT application  
    - Current calculations for display occurs at frame rate  
    _Note: This PR does not contain all logical conditions for activating IR Reflectivity_
    (RS5-9263)  
* [#7672](https://github.com/IntelRealSense/librealsense/pull/7672) - **[L500] Add Alternate IR**  
    Requires firmware_version 1.5.2.0+. (RS5-9266);

* [#7637](https://github.com/IntelRealSense/librealsense/pull/7637) - **[L500] Add Max Usable Range feature**   
    Max Usable Range calculates the maximum range of the camera given the amount of ambient light in the scene.
    - Added to Viewer + LibRS API (not DQT)
    - New option : RS2_OPTION_MAX_USABLE_RANGE
    - New LibRS API function "rs2_get_max_usable_range"
    - Add sensor extension "RS2_EXTENSION_MAX_USABLE_RANGE_SENSOR"
    - Wrappers handling (tested on C#, Python, C++)
    - Requires FW version >= 1.5.0.0 (added NEST (Noise-Estimation) value to temperatures)  
    (RS5-9263)   

* [#7692](https://github.com/IntelRealSense/librealsense/pull/7692) - **Ubuntu 20 (Focal) Support**  
    Alpha level - see above note.  
    Update the patches list with Ubuntu Focal configuration. (DSO-16026)
* [#7518](https://github.com/IntelRealSense/librealsense/pull/7518) - **Add support for Jetson Xavier**  
    Adding kernel patches for V4L driver for Jetson with Ubuntu18, tested with L4T version 4.2.3, 4.3 and 4.4 Jetson installation guide update.  
    (DSO-15132)
* [#7470](https://github.com/IntelRealSense/librealsense/pull/7470) - **Tensorflow Examples**  (DSO-15262)


### Bug Fixes and Enhancements
* [#7706](https://github.com/IntelRealSense/librealsense/pull/7706) - **[L500] Add Reflectivity option restrictions**
    - When changing resolution (sensor mode) during streaming and Enable IR Reflectivity on , IR reflectivity will be disabled (With no error pop up window)
    - ROI restriction is not addressed on this PR  
    (RS5-8358)  
* [#7724](https://github.com/IntelRealSense/librealsense/pull/7724) - **[L500] Disable AC if Alt IR is on.** Throw exception when "Alt IR" is on and user asks for AC.
* [#7718](https://github.com/IntelRealSense/librealsense/pull/7718) - **Trim newlines utility function**  
* [#7635](https://github.com/IntelRealSense/librealsense/pull/7635) - **Udev rules power down**  (On kernel 5.x.x.x there is an issue with iio sensors - some of them does not reduce power consumption after connection.
    This udev-rules correction disables the sensor after it's initial connection.
    (DSO-15863)  
* [#7548](https://github.com/IntelRealSense/librealsense/pull/7548) - **Update rsutil.h**  (In order to remove a warning generated by Rust bindgen) contributed by [@neilyoung](https://github.com/neilyoung)  
* [#7693](https://github.com/IntelRealSense/librealsense/pull/7693) - **Fix Platform Camera streaming  and controls**  
    - Reenable Webcam streaming, with YUYV/2 and MJPEG formats.  
    - Present USB type field.  
    - Extract UVC Header timestamp (metadata) when applicable.  
* [#7687](https://github.com/IntelRealSense/librealsense/pull/7687) - **Fix `Resource deadlock avoided` exception on thread join**  (It's illegal to call **_thread->join();** in capture_loop().
    Setting **_is_capturing = false** breaks to outer while loop, and the thread should be terminated.) contributed by [@Domos](https://github.com/Domos)
 * [#7689](https://github.com/IntelRealSense/librealsense/pull/7689) - **Colorizer - fix division by zero**  (RS5-8689)  
* [#7698](https://github.com/IntelRealSense/librealsense/pull/7698) - **[Viewer] Fix out-of order resources deallocation**  Continued from [#7647](https://github.com/IntelRealSense/librealsense/issues/7647). (DSO-15827)  
* [#7700](https://github.com/IntelRealSense/librealsense/pull/7700) - **[Viewer] Fix playback Resuming in 3D viewer**  (Fixed :
    - Resuming of playback  and 3D viewer are now coupled , when resuming playback - 3D automatically promoted from pause to to play.
    - Stop uploading texture when playback is running and 3D viewer is resumed.  
    (DSO-12584)
* [#7673](https://github.com/IntelRealSense/librealsense/pull/7673) -  **[D400] Skip enabling HDR if already enabled**  (DSO-15909)  
* [#7697](https://github.com/IntelRealSense/librealsense/pull/7697) - **[Java] Fix syntax error on Option.java.**
* [#7674](https://github.com/IntelRealSense/librealsense/pull/7674) - **ROS dependencies update**
    Remove some dependencies to be build dependencies. (DSO-15133)
* [#7558](https://github.com/IntelRealSense/librealsense/pull/7558) - **[D400] HDR-merge and sequence-id-filter proc blocks
    Also add ROS recorder read/write (DSO-15980)  
* [#7619](https://github.com/IntelRealSense/librealsense/pull/7619) - **Fw logger tool adding sleep**  
    Adding a sleep between each fw log polling. Default value is hardcoded in the tool's code. Can be passed from command line with -s <sleep_in_ms> flag
    (DSO-15939)  
* [#7645](https://github.com/IntelRealSense/librealsense/pull/7645) - **Fix colorizer - Get depth units from depth_sensor API.**  
    Get depth units from depth_sensor API instead of disparity_info to support also l500.
[[#7089](https://github.com/IntelRealSense/librealsense/issues/7089)](https://github.com/IntelRealSense/librealsense/issues/7089)  
    Disabling histogram equalization leads depth map to void. (RS5-8868)  
* [#7668](https://github.com/IntelRealSense/librealsense/pull/7668) - **[Python] Fix Python API backwards compatibility for "lld_temperature"**  
    Python API to support both lld_temperature and ldd_temperature. (RS5-9334)  
* [#7543](https://github.com/IntelRealSense/librealsense/pull/7543) - **[D400] HDR live tests update** 
    Checking lrs version, FW support options and metadata available.  
* [#7649](https://github.com/IntelRealSense/librealsense/pull/7649) - **[Viewer] Improve IR stream footer text.**  
    Remove the equal mark from IR stream footer text on mouse picking. (DSO-15449)
* [#7301](https://github.com/IntelRealSense/librealsense/pull/7301) - **[MacOS] define SQLITE_HAVE_ISNAN so xcode 10 will compile**  
    When trying to build librealsense using xcode 10 on macOS 10.14 I ran into the following build error: "SQLite will not work correctly with the -ffast-math option of GCC.   
    The following stackoverflow post suggests defining SQLITE_HAVE_ISNAN in order to fix that error:  https://stackoverflow.com/questions/48917320/getting-gcc-error-when-using-sqlite-and-fast-math-sqlite-will-not-work-correct .  
    contributed by [@robtherich](https://github.com/robtherich)
* [#7573](https://github.com/IntelRealSense/librealsense/pull/7573) - **[NodeJS] Resolve errors and deprecated warnings when build wrapper on nodejs 12**  
    - Updated jsdoc to 3.6.6 to support nodejs 12, but it drop compatibility with nodejs 6.  
    - Update nan for latest version.  
    contributed by [@whsol](https://github.com/whsol)
* [#7648](https://github.com/IntelRealSense/librealsense/pull/7648) - **[Viewer] Remove dots from some of the controls tool tip.**  (DSO-15513)  
* [#7650](https://github.com/IntelRealSense/librealsense/pull/7650) - **[L500] Spelling fix for LDD option**  
    Fixed spelling mistake of LDD Temperature option on get_string(),   The enum value cannot be changed due to backward compatibility. (RS5-8371 )  
* [#7653](https://github.com/IntelRealSense/librealsense/pull/7653) - **Improve the description of alternating_emitter_option.**  (DSO-15512)
* [#7367](https://github.com/IntelRealSense/librealsense/pull/7367) - **rs-convert tool supports extracting frame\time ranges** (DSO-11742) 
* [#7613](https://github.com/IntelRealSense/librealsense/pull/7613) - **[cmake] Add MULTITHREADED/APARTMENTTHREADED selector flag.**  
    Sets the param passed to CoInitializeEx call (Windows only) (DSO-15197)  
* [#7625](https://github.com/IntelRealSense/librealsense/pull/7625) - **[Unity] Adapting wrapper to Unity 2018-2020**  
    - Deleted GUI Layer from some scenes  
    - Added AR Background Resitrictions for  prevent using old classes in Unity 2020)  
    contributed by [@SergeySPF](https://github.com/SergeySPF)  
* [#7632](https://github.com/IntelRealSense/librealsense/pull/7632) - **[NodeJS] Add missing enums to nodejs wrapper and python script for check enums**  
    contributed by [@whsol](https://github.com/whsol)  
* [#7604](https://github.com/IntelRealSense/librealsense/pull/7604) - **Handle exception in uvc_sensor::acquire_power**  
    Reduce the reference counter in case that exception throws in acquire_power (RS5-9071)  
* [#7627](https://github.com/IntelRealSense/librealsense/pull/7627) - **Filter only intel product line on DQT tool**  
    DQT recognizes platform camera when no Realsense  device connected. (DSO-15662)  
* [#7600](https://github.com/IntelRealSense/librealsense/pull/7600) - **[L515] - Add temperature fetcher thread**  
    Periodic read of temperatures and noise estimation values once depth sensor is on.  
    Precondition for reflectivity tool + max range  
    *Description:*
    - A new temperature fetcher thread is created on depth sensor start and closed on stop.
    - All of temperature clients get it from a "get_temperatures" new function 
    - get_temperatures function return the protected fetcher values or read directly from the FW is no fresh values from the thread
    - N-Est values are exposed only with FW ver 1.5.0.0+
    (RS5-9263)  
* [#7610](https://github.com/IntelRealSense/librealsense/pull/7610) - **[Viewer] FW update error popup fix**  (DSO-15557)  
* [#7563](https://github.com/IntelRealSense/librealsense/pull/7563) - **[L515] Add digital gain option that replaces ambient light option** 
    * Add digital gain option at same option value as ambient light.  
    * Add comment on LRS API option ambient light that it is deprecated.  
    * Replace ambient light option registration with digital gain option (same value for both) from L515 depth sensor  
    * Add it to all wrappers  
    * Add special case for python wrapper for dealing with 2 options with the same value  
    * no ambient == high gain  
    (RS5-9152)
* [#7598](https://github.com/IntelRealSense/librealsense/pull/7598) - **Fix humidity option compilation**  (Fix for PR [7474](https://github.com/IntelRealSense/librealsense/pull/7474) compilation issue)
* [#7474](https://github.com/IntelRealSense/librealsense/pull/7474) - **Add description to l500-options**  (RS5-8665)
* [#7572](https://github.com/IntelRealSense/librealsense/pull/7572) - **Added default ctor and initialized valid**  
    Added a default constructor for thermal_calibration_table class, and in non-default constructor added an initialization of _header.valid.
* [#7554](https://github.com/IntelRealSense/librealsense/pull/7554) - **Enable BUILD_EASYLOGGINGPP=OFF**  contributed by [@hsuys](https://github.com/hsuys)
* [#7452](https://github.com/IntelRealSense/librealsense/pull/7452) - **Add time utility classes + UT**  
    * Add a space for common utility classes.  
    * Take timer helper functions from rendering.h , refactor + add functionality and place on timer.h utility file  
    * Replace all time functions usage with new classes  
    * Add unit tests for 3 new classes)  
* [#7551](https://github.com/IntelRealSense/librealsense/pull/7551) - **[L500] Pick K_th fixes**  
* [#7542](https://github.com/IntelRealSense/librealsense/pull/7542) - **[HDR] Return nullptr instead of throwing exception**
* [#7437](https://github.com/IntelRealSense/librealsense/pull/7437) - **Identify L515 USB2 DFU mode**  
    L515 Units with old payload 0 on the device connected with USB2 is identify as D4xx device on DFU mode.
    This PR use the DFU version to determine is the DFU device is L515 or D4xx.
    (RS5-8812)
* [#7493](https://github.com/IntelRealSense/librealsense/pull/7493) - **Fix Viewer GUI freeze due to DFU and SW update pop ups interference**  
    Both processes try to open a popup modal from the same popup tree level, which
is not supported in ImGui.  
    - Handle error message during SW update process (Do not allow pop up from inside a pop up).  
    - Display SW update popup only when no other expended notification is being displayed.  
    (RS5-8934)  
* [#7500](https://github.com/IntelRealSense/librealsense/pull/7500) - **Fix sporadic spinning bug in rs-motion.cpp**
    If the first gyro frame is received before the first accel frame the "first" flag is cleared and the timestamp value is incorrect. This separates the flags to be method specific.  
    Addresses [#4915](https://github.com/IntelRealSense/librealsense/issues/4915))   
* [#7512](https://github.com/IntelRealSense/librealsense/pull/7512) - **Fix error poller method.**  
    - Support graceful sensors closure on switching to DFU mode.  
    - Minor formatting and wording corrections.  
    (RS5-8661)  
* [#7522](https://github.com/IntelRealSense/librealsense/pull/7522) - **[HDR]  Enhancements**  
    Replace exceptions with log writing when accessing affected controls while in HDR mode.  
    Adding HDR unit-tests suite.  
    (DSO-15603), (DSO-15592)
* [#7514](https://github.com/IntelRealSense/librealsense/pull/7514) - **[L500] Fix GlobalTimer**  
    Fix FW clock readings. Addresses [#7508](https://github.com/IntelRealSense/librealsense/issues/7508) (RS5-9117)  
* [#7023](https://github.com/IntelRealSense/librealsense/pull/7023) - **Fix warning C4005 macro redefinition**  
    ex: warning C4005: 'WIN32_LEAN_AND_MEAN': macro redefinition. contributed by [@chadbramwell](https://github.com/chadbramwell)  
* [#7515](https://github.com/IntelRealSense/librealsense/pull/7515) - **Fix black pixel at upper left corner** 
    Remove setting upper left pixel on viewer to 0,0,0 (Black) (RS5-8960)
* [#7501](https://github.com/IntelRealSense/librealsense/pull/7501) - **[Python] Add D455 product id to python-rs400-advanced-mode-example.py**  
    Even though a hardcoded list of magic numbers is a bad practice, the example should work with the new D455 sensor. contributed by [@Petrox](https://github.com/Petrox)
* [#7440](https://github.com/IntelRealSense/librealsense/pull/7440) - **[Viewer] make snapshots for IMU and pose frames.**  (RS5-8691)  
* [#7490](https://github.com/IntelRealSense/librealsense/pull/7490) - **Add L515 humidity temperature option**  (RS5-9069)
* [#7468](https://github.com/IntelRealSense/librealsense/pull/7468) - **Fix depth stream freeze in post-processing**
    Use streams_origin to find out the origin ID of stream in case the frame is after some post-processing.  
* [#7451](https://github.com/IntelRealSense/librealsense/pull/7451) - **Fix stuck depth scene in texture mapping** (RS5-8690)  
 [#7413](https://github.com/IntelRealSense/librealsense/pull/7413) - **Improve the message at the end of the recording** (RS5-8698) 
* [#7297](https://github.com/IntelRealSense/librealsense/pull/7297) - **[L500] Krgb-thermal support**  
    Reading k-thermal table from FW and use it to correct k-rgb according to current humidity temp, the k-rgb that written to FW is without the thermal correct ,but user will get the corrected one.  
* [#7438](https://github.com/IntelRealSense/librealsense/pull/7438) - **added CMake error when BUILD_WITH_TM2 is on but IMPORT_DEPTH_CAM_FW is off**  (RS5-8833)  
* [#7412](https://github.com/IntelRealSense/librealsense/pull/7412) - **Improve error message**  
    Improve the error message in custom preset when sensor_mode is incompatible with requested resolution. (RS5-8797 )  

 ### Documentation
* [#7725](https://github.com/IntelRealSense/librealsense/pull/7725) - **update installation.md for Udev rules power down**  
    add "at" installation to installation.md
* [#7061](https://github.com/IntelRealSense/librealsense/pull/7061) - **Document the order of the coefficients in rs2_intrinsics::coeffs**  
    I could not find the order of the distortion coefficients in the Realsense documentation so I am adding them to it. I am assuming that they follow the order that is used in OpenCV for its distortion coefficients. contributed by [@foohyfooh](https://github.com/foohyfooh)
* [#7329](https://github.com/IntelRealSense/librealsense/pull/7329) - **Fix documentation in C API examples**  
    Fix some comments in the documentation of C API examples. contributed by [@gsaponaro](https://github.com/gsaponaro)  
* [#7382](https://github.com/IntelRealSense/librealsense/pull/7382) - **Fixed Typos in Documentation**  contributed by [@harshmittal2210](https://github.com/harshmittal2210)


### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable. (DSO-13700)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) v2.33.1 does not compile with -DBUILDEASYLOGGINGPP=OFF
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-13525) - [D400] 3D viewer moved when sliding the tare calibration sliders
* (RS5-7374) - [L515] Error after performing HW reset
* (DSO-15118) - [D400] Viewer is closed forcibly with cycling start/stop streaming in 3D view.
* (DSO-15250) - [Viewer] with OpenVINO stops the RGB stream when IMU is activated


## Release 2.39.0
Release Date: 1 Oct 2020

### API Changes
https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2390


### New Features
* [#7453](https://github.com/IntelRealSense/librealsense/pull/7453) - **D4xx Firmware - v5.12.8.200** 
  - **Important: the firmware is intended to be used with SDK v2.39.0(+) and is not compatible with the previous Librealsense releases**
  - Add RGB stream from Left IR imager (D455).
  - HDR Functionality for D400 Depth sensors
* [#7466](https://github.com/IntelRealSense/librealsense/pull/7466) - **L515 Firmware -  v1.5.1.3**  
  - Support for USB2
  - Support QVGA resolution
  - Controls and stability improvements

* [#6916](https://github.com/IntelRealSense/librealsense/pull/6916) - **[D455] Add synthetic RGB from left imager**
* [#7205](https://github.com/IntelRealSense/librealsense/pull/7205) - **[Android] Enable USB weak host workaround to improve android stability**  
Enable L515 android stability workaround. Current USB buffer settings in device require large number of small USB transactions from device to USB host controller, some hosts with relatively weak host cannot handle this many transactions quickly, results in stability issues, camera disappear from os enumeration or one of the streams dies during stream, etc. This workaround uses larger buffer settings to reduce the number of transaction and improve performance and stability.
Workaround is enabled by default for all android platforms. Requires additional firmware command support in new firmware release.
(RS5-8011)
* [#7354](https://github.com/IntelRealSense/librealsense/pull/7354) - **Depth HDR Functionality (Alpha Release)** 
A new Depth enhancement feature implemented in both Host and the Device Firmware that allows to improve Depth data in adverse light conditions by merging data from consecutive frames.
At its core the feature allows to configure and run Depth and IR stream with per-frame specified exposure and gain values (sequence of 2 frames). Dedicated metadata attributes allow to associate the arriving frames with the configuration established by user.  
When arrived on host a specially-designed `Merge` processing block shall be utilized to fuse depth data from the incoming frames.
Additionally a `Filtered Id` processing block is provided that allows to forward Depth and IR frames that correspond to even/odd frames of the sequence.  
The feature is integrated with `Realsense-Viewer` application via a set of dedicated controls and post-processing blocks.  
It is an Alpha release, and will be followed by a White Paper for in-depth presentation and usage guidance.  
(DSO-15603)  
Complementary PRs:   
    * [#7257](https://github.com/IntelRealSense/librealsense/pull/7257) - **[HDR] Split/Merge processing blocks infrastructure**  
    * [#7354](https://github.com/IntelRealSense/librealsense/pull/7354) - **[HDR] Support for sub-preset configuration**
    * [#7397](https://github.com/IntelRealSense/librealsense/pull/7397) - **[HDR] Adjust metadata names**  
    * [#7404](https://github.com/IntelRealSense/librealsense/pull/7404) - **[HDR] Update metadata sequence id**  
* [#7385](https://github.com/IntelRealSense/librealsense/pull/7385) - **[Network-device] support for D455 and L515, update list of supported streaming configurations**

### Bug Fixes and Enhancements
* [#7409](https://github.com/IntelRealSense/librealsense/pull/7409) - **[Python] Reverting the parametrized `get_depth_frame`**
* [#7403](https://github.com/IntelRealSense/librealsense/pull/7403) - **[Windows] Fix crash on stop sensors**  Use auto reset event instead of manual event (RS5-8921)
* [#7368](https://github.com/IntelRealSense/librealsense/pull/7368) - **[Android] Correct  the order in the extensions list**  Change in `rs_extension` had been done while the new enums were added out of order.
* [#6564](https://github.com/IntelRealSense/librealsense/pull/6564) - **[Core] Min Distance can't get higher value than the Max Distance**   Affects Threshold Filter and Depth Visualization (DSO-12346, DSO-12163)
* [#7344](https://github.com/IntelRealSense/librealsense/pull/7344) - **[L515] Disable unsigned FW update for unlocked units**
* [#7330](https://github.com/IntelRealSense/librealsense/pull/7330) - **Refactor error polling with shared/weak ptr instead of unique_ptr.**  (Switch to shared/weak ptr model for active object handler. Follow up on [#7272](https://github.com/IntelRealSense/librealsense/issues/7272). (DSO-15542)
* [#7334](https://github.com/IntelRealSense/librealsense/pull/7334) - **[L515] Fix DFU crash**  DFU update on L515 is generating an exception and fails the update process. The Asic serial number structure retrieved from the DFU FW has reversed bytes order then expected. This PR address this issue and treat the data at the real FW implementation order.
(RS5-8843)
* [#7323](https://github.com/IntelRealSense/librealsense/pull/7323) - **[Viewer] Fix SW update crash**  (When connecting a device, the SW Update checks whether a new version is available.
  - Use a weak ptr for the SW update detached thread
  - Reduce the DB download tried to 1 (still 5 seconds timeout)
(RS5-8694)
* [#7325](https://github.com/IntelRealSense/librealsense/pull/7325) - **[L515] Remove SW limitation of noise filter range**  (Previous SW min limit=2 for noise filter option) 
* [#7272](https://github.com/IntelRealSense/librealsense/pull/7272) - **Stability enhancemets** Follow up on [#7330](https://github.com/IntelRealSense/librealsense/pull/7330).
* [#7246](https://github.com/IntelRealSense/librealsense/pull/7246) - **[L515] Callback receives depth+infrared when only depth is requested**  (Add test: "test-depth-only" - checks that if depth is the only profile specified when opening a sensor, the callback given at sensor.start() will be called for depth frames only)
* [#7294](https://github.com/IntelRealSense/librealsense/pull/7294) - **[Viewer] SW Updates - Fix UI issue + allow use of local DB file**  
  - Overcome `ImGui` issue that cause an error pop_up closing the updates window. (always force open it unless no need)
 -Allow local version's DB file use. (Treat "file://" prefix as local file path)
* [#7269](https://github.com/IntelRealSense/librealsense/pull/7269) - **[L515] Filter IR frames if were not requested by the user**  (RS5-8734)
* [#7203](https://github.com/IntelRealSense/librealsense/pull/7203) - **[L515] Fix GVD fields for S.N. & lock statuses**  (RS5-8550)
* [#7293](https://github.com/IntelRealSense/librealsense/pull/7293) - **[L515] Fix crash when connecting L515 device to the Viewer application**  
   - Addresses issue caused on [PR 7126](https://github.com/IntelRealSense/librealsense/pull/7126/files) caused by a virtual function call from inside L515 ctor -- replaced with a member variable.
* [#7278](https://github.com/IntelRealSense/librealsense/pull/7278) - **Report reason for stream stop (HW errors)**  (RS5-7657)
* [#7259](https://github.com/IntelRealSense/librealsense/pull/7259) - **[Linux] named_mutex: release if exception occurs while locking.**  (Addresses deadlock in viewer when unplugging camera while streaming and then plugging it back
 Add to unit-tests (multicam_streaming test) - test streaming of depth only due to known issues with alternate streaming of color. (DSO-15623)
* [#7248](https://github.com/IntelRealSense/librealsense/pull/7248) - **[Tools] Print FW logs with host clock**  () contributed by [@ashrafabuesba](https://github.com/ashrafabuesba)
* [#7241](https://github.com/IntelRealSense/librealsense/pull/7241) - **Bundled firmware update no longer fail if backup step fail**  (The flash backup was a mandatory step at the firmware update. At this PR we allow to proceed with the update even if the backup step fail. (DSO-15599)
* [#7213](https://github.com/IntelRealSense/librealsense/pull/7213) - **Fix a wrong argument in "CreateEvent" call** contributed by [@libdavid](https://github.com/libdavid)
* [#7238](https://github.com/IntelRealSense/librealsense/pull/7238) - **Add rs2_cah_trigger_to_string to realsense.def** 
* [#6304](https://github.com/IntelRealSense/librealsense/pull/6304) - **BUILD_EASYLOGGING = OFF **  (compiles with -DBUILD_EASYLOGGINGPP=OFF and unit_tests pass. Addresses [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) 
* [#7207](https://github.com/IntelRealSense/librealsense/pull/7207) - **[Viewer] Fix crash on Fw update**  enhancement over PR7165. (DSO-15554)
* [#7186](https://github.com/IntelRealSense/librealsense/pull/7186) - **[Viewer] Prevent imGui state corruption in Viewer**  by encapsulating exception handling. (DSO-15542)
* [#7184](https://github.com/IntelRealSense/librealsense/pull/7184) - **Fix SW update links**  (The SW Update links filling were mistakenly comment out on a LLVM unused variable warning fix This PR undo it and removed the unused variables.)
* [#7158](https://github.com/IntelRealSense/librealsense/pull/7158) - **[L515] Remove depth invalidation option** 
* [#7165](https://github.com/IntelRealSense/librealsense/pull/7165) - **[Viewer] Disable click on fw update buttons when streaming**  (DSO-15554)
* [#7171](https://github.com/IntelRealSense/librealsense/pull/7171) - **Uncomment "message" call**  (Call to message(STATUS "Checking internet connection...") was commented.) contributed by [@libdavid](https://github.com/libdavid)
* [#7161](https://github.com/IntelRealSense/librealsense/pull/7161) - **Fix backward button issue with viewer.**  (the function rs2_playback_seek behind the playback::seek function can't receive negative timestamps. (DSO-15533)
* [#7164](https://github.com/IntelRealSense/librealsense/pull/7164) - **Add OpenCV license to NOTICE** 
* [#7147](https://github.com/IntelRealSense/librealsense/pull/7147) - **[L515] Fix CAH unit-tests file separators in Linux**
* [#7148](https://github.com/IntelRealSense/librealsense/pull/7148) - **added 'using std::abs' in types.h to avoid Linux bug**  (This fixes a bug where compilation occurs on Ubuntu 16, where GCC decides to use abs(int) and this obviously causes bad results. The global ::abs() should really never be used, but I found no good way of removing it.
(RS5-8641)
* [#7133](https://github.com/IntelRealSense/librealsense/pull/7133) - **[Viewer] Fix ctrl+Num keys not rendering on viewer terminal**  
  - Viewer application does not support special keys like '_' (all of shift + Num keys) as inputs. The code that was removed on this PR is the reason. It was inserted as part of the terminal feature to allow copy-paste capabillity.
* [#7131](https://github.com/IntelRealSense/librealsense/pull/7131) - **Occlusion bug fix**  Addresses [#6990](https://github.com/IntelRealSense/librealsense/issues/6990). (RS5-8522)
* [#7126](https://github.com/IntelRealSense/librealsense/pull/7126) - **[L515] Update tagged profiles for USB2**  
  - Remove raw resolutions processing blocks
  - Update L515 tagged profiles to support USB2 resolutions
  - Remove viewer resolutions + FPS constrains for USB 2 (behavior stayed the same due to tagged profiles)
(RS5-8384)
* [#7097](https://github.com/IntelRealSense/librealsense/pull/7097) - **Fix sensor mode exception on QVGA resolution (USB2)**
  - Sensor default mode change from XGA to [USB3 -> VGA], [USB2 -> QVGA]. (RS5-8352)
* [#7105](https://github.com/IntelRealSense/librealsense/pull/7105) - **[L515] Fixed bug on manual trigger:**  (movement_from_last_success is always true in manual trigger.) 
* [#7094](https://github.com/IntelRealSense/librealsense/pull/7094) - **[L515] Handle dynamic number of intrinsic tables for USB2 support**  On L515 device we get 2 depth resolutions on USB3 and 1 on USB2.
This PR replace sharing the FW raw data vector with a physical preallocated full size buffer (Support up to 5 resolutions)
Same change apply for depth and color intrinsic tables handling.
* [#7072](https://github.com/IntelRealSense/librealsense/pull/7072) - **[L515] Set default values for color sensor controls for calibration**  (For better results the CAH process require default values to some of the RGB sensor controls.
When the CAH process need to open the color sensor, it will check and set the sensor controls to it's default values if needed.
When the CAH need to stop the color sensor or if the user will open the sensor while CAH opened it, it will restore the values to it's previous ones if needed.
)
* [#7092](https://github.com/IntelRealSense/librealsense/pull/7092) - **Call to callback from optimize() and optimize_p(), also on non debug mode.**  (Call to callback from optimize() and optimize_p() also on non debug mode, to enable stop in time if needed)
* [#7075](https://github.com/IntelRealSense/librealsense/pull/7075) - **Small optimization in CAH plus removal of two annoying repetitive messages in Viewer**
* [#7074](https://github.com/IntelRealSense/librealsense/pull/7074) - **[L515] New CAH limiters & handling per VAL request**
* [#7076](https://github.com/IntelRealSense/librealsense/pull/7076) - **[Python] Fix GIL locks in calibrated_sensor APIs which can cause frame drops**
* [#7071](https://github.com/IntelRealSense/librealsense/pull/7071) - **[L515] Disable auto CAH by default and update bundled L515 FW version to 1.4.1.2**

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable. (DSO-13700)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) v2.33.1 does not compile with -DBUILDEASYLOGGINGPP=OFF
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-13525) - [D400] 3D viewer moved when sliding the tare calibration sliders
* (RS5-7374) - [L515] Error after performing HW reset
* (DSO-15118) - [D400] Viewer is closed forcibly with cycling start/stop streaming in 3D view.
* (DSO-15250) - [Viewer] with OpenVINO stops the RGB stream when IMU is activated


## Release 2.38.1
Release Date: 27 Aug 2020

### API Changes
https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2381

### New Features
* [#6970](https://github.com/IntelRealSense/librealsense/pull/6970) - **D4xx Firmware - v5.12.7.100**
* [#6997](https://github.com/IntelRealSense/librealsense/pull/6997) - **L515 Firmware -  v1.5.0.0**  

  - Controls and stability improvements
  

### Bug Fixes and Enhancements
* [#6150](https://github.com/IntelRealSense/librealsense/pull/6150) - **global_timestamp_reader: no blocking.**.  Prevent calls for get_device_time_ms from frame thread. Continue system_time-hw_time equation through time loop.
* [#7017](https://github.com/IntelRealSense/librealsense/pull/7017) - **Fix reporting distance with SW device**  (DSO-15441)
* [#6933](https://github.com/IntelRealSense/librealsense/pull/6933) - **Release CComPtr cause to access violation** 
* [#6926](https://github.com/IntelRealSense/librealsense/pull/6926) - **Fw logger bug fix**.  Fixing timestamp in new fw logger message (DSO-15394) 
* [#6945](https://github.com/IntelRealSense/librealsense/pull/6945) - **Android stability fixes** -  Camera app performance/stability issues:
1. fix pipe.stop() issues
   a) problem: null pointer segfault
       cause: thread synchronization in dispatcher
       fix: add additional lock in invoke_and_wait.
  b) problem: invalid address segfault in uvc_streamer, active_object, dispatcher flows
      cause: double release of memory in destructors due to synchronization issue in watchdog, active_object, dispatcher, and primarily uvc_streamer.
      fix: add additional state check and synchronization.
  c) problem: invalid address segfault in pipeline flows
     cause: double release of memory in pipeline destructor to stop pipeline twice, the extra stop come from JNI code when handle is deleted and invokes destructor which tries to run stop() again.
     fix: do shared pointer reset when profile active (also this is when they are initialized).
   d) problem: invalid address segfault at various points depends on workload
      cause: uvc_streamer shared pointers cleared at the wrong time, not cleared when stream stopped, so it tries to stop the streamer a second time during destruction
      fix: destroy uvc_streamers after stream is stopped and no active profiles
   e) problem: invalid address segfault in device info destructor through JNI stack
       cause: appears to be double releasing as JNI stack references the pointer
       fix: avoid delete in JNI, need to confirm it's released on native stack.
2. problem: invalid address segfault related to stream profiles
   cause: profile data array copy in JNI, jlong is 64-bit but pointer could be 32-bit, should not xcopy the entire buffer
   fix: copy array elements
3. problem: invalid address segfault related to query sensors
   cause: sensor data array copy in JNI, jlong is 64-bit but pointer could be 32-bit, should not xcopy the entire buffer
   fix: copy array elements
4. problem: camera app performance degradation and stability issues after repeated device disconnect/connect
   app cannot recover if device disconnected in middle of starting streaming
   cause: activity operations executed multiple times due to activity instances and sequence issue
   fix: create single activity instance, manage its creation and destruction, and correct sequence.  
(RS5-8219, DSO-15293, DSO-15294, DSO-15358, DS5U-4588)
* [#7008](https://github.com/IntelRealSense/librealsense/pull/7008) - **Query Projector capability from FW**  (DSO-15453)
* [#7000](https://github.com/IntelRealSense/librealsense/pull/7000) - **Increase logs queue size on viewer**  (The current queue is at default size of 10, that means that at a viewer cycle when the logs queue is full after 10 logs the output window will miss logs.
This PR increase the logs to 100 in order to display a peek of logs.) 
* [#6567](https://github.com/IntelRealSense/librealsense/pull/6567) - **Viewer starts without Documents directory**.  Fixes [#5707](https://github.com/IntelRealSense/librealsense/issues/5707)
(DSO-13589) 
* [#6950](https://github.com/IntelRealSense/librealsense/pull/6950) - **Fix viewer error while trying to replay a bag file with confidence stream**  
* [#6929](https://github.com/IntelRealSense/librealsense/pull/6929) - **Remove dependency on fts.h**  (`fts.h` is included in these two backend-v4l2 files but not actually used.) contributed by [@dbolkensteyn](https://github.com/dbolkensteyn)
* [#6954](https://github.com/IntelRealSense/librealsense/pull/6954) - **Fix extrinsics related log_warnings while recording on L515**  (Fix a log warning when recording RGB / Confidence streams on L515 devices) 
* [#6998](https://github.com/IntelRealSense/librealsense/pull/6998) - **Set L500 Depth Invalidation flag to false by default**  
* [#6999](https://github.com/IntelRealSense/librealsense/pull/6999) - **Remove Y8I conditional invocation for USB2**  (DSO-15468)
* [#7007](https://github.com/IntelRealSense/librealsense/pull/7007) - **Add missing string to rs_sensor_mode enum**
* [#7046](https://github.com/IntelRealSense/librealsense/pull/7046) - **Always open IR stream with depth on L515**
* [#7004](https://github.com/IntelRealSense/librealsense/pull/7004) - **Disable CAH buttons on viewer device menu** 


### Documentation
* [#7034](https://github.com/IntelRealSense/librealsense/pull/7034) - **Link fix**  () contributed by [@fburak](https://github.com/fburak)
* [#7011](https://github.com/IntelRealSense/librealsense/pull/7011) - **Update imu calibration white paper public web link**  (The latest IMU white paper refresh was published to a different web link than previously documented in read.md. This change is to update the link. No impact to calibration script or user.)


## Pre-Release 2.37.0
Release Date: 27 Jul 2020

* [#6872](https://github.com/IntelRealSense/librealsense/pull/6872) - *Adjusting Unity package to work with L515 out of the box* (This PR is introducing couple of small changes with regards to IR stream indexing to ensure Unity sample works with both D400 and L500 families of cameras. Following-up on [#6579](https://github.com/IntelRealSense/librealsense/issues/6579) and [#6859](https://github.com/IntelRealSense/librealsense/issues/6859) 
* [#6891](https://github.com/IntelRealSense/librealsense/pull/6891) - *Adjust windows cmake build to v3.6+*
* [#6848](https://github.com/IntelRealSense/librealsense/pull/6848) - *pointcloud::calculate add const specifier* contributed by [@ohadmen](https://github.com/ohadmen)
* [#6884](https://github.com/IntelRealSense/librealsense/pull/6884) - *Pyrealsense2-net wrapper* (follow-up on https://github.com/IntelRealSense/librealsense/pull/6171 by @lramati. Adds `pyrealsense2-net` wrapper for `realsense2-net` extension module)
* [#6889](https://github.com/IntelRealSense/librealsense/pull/6889) - *Re-enable Thermal Compensation loop* (Requires FW v5.12.7+
Tracked on:DSO-14980)
* [#6645](https://github.com/IntelRealSense/librealsense/pull/6645) - *Fix rs-tracking-and-depth with T265* contributed by [@pjessesco](https://github.com/pjessesco)
* [#5800](https://github.com/IntelRealSense/librealsense/pull/5800) - Fix a bug concerning connection to multiple cameras by several threads or processes with V4L2 backend (Linux). Tracked on: DSO-13745
* [#6880](https://github.com/IntelRealSense/librealsense/pull/6880) - *Adding GPIOs state to metadata* (Field added in metadata in order to support GPIO Input Data. Triggered by jira ticket: DSO-15379)
* [#6793](https://github.com/IntelRealSense/librealsense/pull/6793) - *Controls emitter options list changed to dynamic* (Triggered by jira ticket: DSO-15273. In android camera application, the relevant values for the emitter options are now dynamic. This implements also the requirements due to jira ticket: RS5-8168)
* [#6818](https://github.com/IntelRealSense/librealsense/pull/6818) - Android Wrapper - Projection API functions added. Triggered by jira ticket: DSO-15199
* [#6858](https://github.com/IntelRealSense/librealsense/pull/6858) - *Improved Error Handling for SDK tools* (On Windows, the Viewer & DQT could silently fail in certain situations, now all errors will be reported with an option to submit as a new GitHub ticket)
* [#6786](https://github.com/IntelRealSense/librealsense/pull/6786) - *Fix the return value of poll_for_frames in MATLAB wrapper*  contributed by [@mengyui](https://github.com/mengyui)
* [#6809](https://github.com/IntelRealSense/librealsense/pull/6809) - *remove rs_terminal_parser.h - obsolete file*
* [#6779](https://github.com/IntelRealSense/librealsense/pull/6779) - *Auto-exposure Priority Mode tooltip text corrected* (Tooltip text corrected so that the user would understand the implications of turning ON/OFF the Auto Exposure Priority button in realsense viewer.
Tracked on: DSO-13683)

## Release 2.36.0
Release Date: 9 Jul 2020

### API Changes
https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2360


### New Features
* [#6782](https://github.com/IntelRealSense/librealsense/pull/6782) - **New 4xx FW v5.12.6.0** - Stability and performance enhancements
* [#6694](https://github.com/IntelRealSense/librealsense/pull/6694) - **New L515 FW v1.4.1.2** - Stability and performance enhancements  
  - * (RS5-6586) - [L515] Corrupted Depth and IR  
* [#6679](https://github.com/IntelRealSense/librealsense/pull/6679),[#6623](https://github.com/IntelRealSense/librealsense/pull/6623),[#6666](https://github.com/IntelRealSense/librealsense/pull/6666),[#6743](https://github.com/IntelRealSense/librealsense/pull/6743) - **RealSense-Viewer Enhancements**  
  - Firmware logs window to streamline profyling and debugging (DSO-14959)
  - Terminal for Firmware commands and calibration data window (DSO-15212)
* [#6587](https://github.com/IntelRealSense/librealsense/pull/6587) - **[L515] Add IMU Calibration and Motion Correction support**
  - Support L515 IMU calibration and motion correction
  - Updated L515 extrinsic
  - Keep lazy design, use default intrinsic in case valid calibration data is not available on device
  - Calibration instruction aligned for all D400 and L515 devices with IMU  
(RS5-7834)
* [#6594](https://github.com/IntelRealSense/librealsense/pull/6594) - **Android intrisics extrinsics added to wrapper**  (Adding Intrisic and Extrinsic libRS API to the Android wrapper)  
  - rs2_get_extrinsics
  - rs2_get_video_stream_intrinsics
  - rs2_get_motion_intrinsics  
Resolves [#4580](https://github.com/IntelRealSense/librealsense/issues/4580) (DSO-14957) 

### Bug Fixes and Improvements
* [#6680](https://github.com/IntelRealSense/librealsense/pull/6680) - **[C#] Add L500 preset enum**   -Add enum similar to `Rs400VisualPreset` to easily set `Option.VisualPreset` for L500 devices. contributed by [@jangernert](https://github.com/jangernert)
 
* [#6615](https://github.com/IntelRealSense/librealsense/pull/6615) - **[C#] fix L500 intrinsic initialization**. Addresses [#6609](https://github.com/IntelRealSense/librealsense/issues/6609) contributed by [@jangernert](https://github.com/jangernert)
* [#6709](https://github.com/IntelRealSense/librealsense/pull/6709) - **[Linux] Update patch-arch.sh**   - Fix for on Manjaro Linux. Extending the patch for Depth Metadata. contributed by [@puzzlepaint](https://github.com/puzzlepaint)
* [#6727](https://github.com/IntelRealSense/librealsense/pull/6727) - **[L515] NUM_OF_DEPTH_RESOLUTIONS reverted."**  (return NUM_OF_DEPTH_RESOLUTIONS to 2 for backward compatibility. 
* [#6722](https://github.com/IntelRealSense/librealsense/pull/6722) - **[MacOS] Fix imGui Font, habdle LLVM warnings**:
  - Adding new imGui font results in artifact similar to [#4558](https://github.com/IntelRealSense/librealsense/issues/4558);  
  - remove unused variables; 
  - re-order ctor init lists to rectify potential out-of order value initialization
* [#6723](https://github.com/IntelRealSense/librealsense/pull/6723) - **[L515] Resolutions alignment and Algo recording**
  - Update the num of resolutions.
  - Separate the dir of  algo recording from files names
* [#6700](https://github.com/IntelRealSense/librealsense/pull/6700) - **[L515] Fix Confidence Stream handling**  (Enabling confidence stream causes missing depth frames)
* [#6699](https://github.com/IntelRealSense/librealsense/pull/6699), [#6693](https://github.com/IntelRealSense/librealsense/pull/6693) - **[Android] WaitForFrames timeout adjustment for L515**  (switched to 5sec default)
* [#6622](https://github.com/IntelRealSense/librealsense/pull/6622) - **MSVC screening** 
  - static casts; unused variables; excessive #define usage
* [#6668](https://github.com/IntelRealSense/librealsense/pull/6668) - **[L515] Provision for additional streaming profiles** - USB2 mode.  (RS5-7992)
* [#6644](https://github.com/IntelRealSense/librealsense/pull/6644) - **[Unity] Fix the value of RS2_OPTION_FILTER_MAGNITUDE**  contributed by [@mengyui](https://github.com/mengyui)
* [#6654](https://github.com/IntelRealSense/librealsense/pull/6654) - **Linux Updates and Fixes**
  - Fix streaming CNF4 with kernel 4.19+
  - Add patches for kernel 5.4 LTS (Bionic)
  - Retrofit FG/INZC/PAIR/Z16H FourCC into patches to eliminate irrelevant warnings.
  - Patches script - fix Ubuntu tag selection to filter 4-digit kernel versions.
  - Fix patches for the deprecated Bionic/4.18 branch.  
(RS5-8037)
* [#6672](https://github.com/IntelRealSense/librealsense/pull/6672) - **[Android] fix stability issue on strea.stop**  (fix invoke_and_wait regression (caused by https://github.com/IntelRealSense/librealsense/pull/6203).  
(RS5-7999), (DSO-15084)
* [#6220](https://github.com/IntelRealSense/librealsense/pull/6220) - **[Python] Move bindings into separate cmake target**  (* Move python bindings into a separate cmake target so we can install them separately. Also install the python bindings into python's sitearch, not in `/usr/lib64` (or `/usr/local/lib64`)  
Resolves [#6124](https://github.com/IntelRealSense/librealsense/issues/6124). contributed by [@morxa](https://github.com/morxa)
* [#6617](https://github.com/IntelRealSense/librealsense/pull/6617) - **[L500] Block return to Default Preset + cancel max_range on stream start**  (**System requirement** - Trying to return to visual preset "Default" should generate an error on the viewer + exception on the API. (RS5-7898)
* [#6639](https://github.com/IntelRealSense/librealsense/pull/6639) - **[Viewer] Fix UI crash when disabling measurement**  (On the viewer/depth quality tool if a user pressed on "Measure" button while a measurement is active, the application crashed.
* [#6629](https://github.com/IntelRealSense/librealsense/pull/6629) - **[SDK Core] Hexify helper method name in test changed to char2hex**  (Same name of helper function in global namespace lead to failure in linkage.)
* [#6625](https://github.com/IntelRealSense/librealsense/pull/6625) - **[L515] UI Adjustments**  Cosmetic changes for l515 (RS5-7661)
* [#6621](https://github.com/IntelRealSense/librealsense/pull/6621) - **[Viewer]: Fix Depth ROI button for D4xx**  (DSO-15009)
* [#6593](https://github.com/IntelRealSense/librealsense/pull/6593) - **Add capability to override the official SW update server url** - Debugging Capability
* [#6581](https://github.com/IntelRealSense/librealsense/pull/6581) - **[CUDA] Fix broken compilation**  (Fix gcc-pedantic remarks). Resolves [#6573](https://github.com/IntelRealSense/librealsense/issues/6573) (DSO-15134)
* [#6405](https://github.com/IntelRealSense/librealsense/pull/6405) - **[Core SDK] Move to Catch2 version 2.12.1**  (Only affects unit-testing)  
  - Catch2 changes the way we do approximate-equals comparisons, and we now define our own approx() (rather than the Catch Approx()) for customizability.
  - Also fixed some warnings.
* [#6595](https://github.com/IntelRealSense/librealsense/pull/6595) - **[CI] Travis update nodeJs version to  10.15.3**  (regression on travis-cs nodeJs build)
  - Mocha latest verison no longer support NodeJs version 6 https://github.com/mochajs/mocha/releases [#4164](https://github.com/IntelRealSense/librealsense/issues/4164):
  - Mocha v8.0.0 now requires Node.js v10.0.0 or newer. Mocha no longer supports the Node.js v8.x line ("Carbon"), which entered End-of-Life at the end of 2019)

## Documentation
* [#6747](https://github.com/IntelRealSense/librealsense/pull/6747) - **monitor the dmesg change**   contributed by [@wwppyy](https://github.com/wwppyy)
* [#6678](https://github.com/IntelRealSense/librealsense/pull/6678) - **Fixed "depth" typo**  (L110: depht -> depth) contributed by [@AndreiCostinescu](https://github.com/AndreiCostinescu)
* [#6592](https://github.com/IntelRealSense/librealsense/pull/6592) - **Fixed typo in examples/cmake/readme.md**  (applicatoin -> application) contributed by [@AndreiCostinescu](https://github.com/AndreiCostinescu)

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable. (DSO-13700)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) v2.33.1 does not compile with -DBUILDEASYLOGGINGPP=OFF
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-13525) - [D400] 3D viewer moved when sliding the tare calibration sliders
* (RS5-7374) - [L515] Error after performing HW reset
* (DSO-15118) - [D400] Viewer is closed forcibly with cycling start/stop streaming in 3D view.
* (DSO-15250) - [Viewer] with OpenVINO stops the RGB stream when IMU is activated
* (RS5-8167) - [Viewer] Firmware Update process may generate unnecessary warning/popup message that must be clicked to proceeds
* (RS5-8011) - [Android] L515 looses connection under stress streaming.

## Release 2.35.2
Release Date: 10 Jun 2020

### API Changes
N/A

### New Features
* [#6487](https://github.com/IntelRealSense/librealsense/pull/6487) - **Introduce L515 Depth Camera** official support. 
* [#6480](https://github.com/IntelRealSense/librealsense/pull/6480) - **L515**: Firmware version 1.4.1.0.  
   - Fix Horizontal shift of depth map. 
   - Recommended firmware with this release.  
* [#6423](https://github.com/IntelRealSense/librealsense/pull/6423) - **Viewer** 3D view enhancements:
   - 3D interactive measurements
   - Shading with Diffuse Light mode
   - Updated UI
* [#6457](https://github.com/IntelRealSense/librealsense/pull/6457), [#6548](https://github.com/IntelRealSense/librealsense/pull/6548) - **Viewer**: Add check-for-updates capability to streamline SW updates. The feature would provide notification in case of software changes/new version releases (RS5-7674).


### Bug Fixes and Improvements
* [#6488](https://github.com/IntelRealSense/librealsense/pull/6488) - **Linux**: Remove libusb warning on device removal.
* [#6484](https://github.com/IntelRealSense/librealsense/pull/6484) - **Core**: fix memory leak in occlusion-filter. (RS5-7793).
* [#6467](https://github.com/IntelRealSense/librealsense/pull/6467) - **Core**: Fix Multi-camera behavior with RSUSB backend. Follow up on [5615](https://github.com/IntelRealSense/librealsense/pull/5615).  Should address [#5614](https://github.com/IntelRealSense/librealsense/issues/5614), [#5935](https://github.com/IntelRealSense/librealsense/issues/5935), [#6084](https://github.com/IntelRealSense/librealsense/issues/6084).
* [#6487](https://github.com/IntelRealSense/librealsense/pull/6487) - **L515** Fixes and enhancements:
   - PID update + enable metadata support.
   - Remove unnecessary froms from `validator` (RS5-7628)
   - Fix memory leak in `validator` (RS5-7715)   
   - Fix playback crash (RS5-7726)  
* [#6492](https://github.com/IntelRealSense/librealsense/pull/6492) - **L515**: Viewer to include recommended FW for the said SKU (RS5-7866).
* [#6492](https://github.com/IntelRealSense/librealsense/pull/6492) - **L515**: Adjust projector power default mode  (RS5-7780).
* [#6500](https://github.com/IntelRealSense/librealsense/pull/6500) - **L515**: IMU Calibration script to support said SKU. (RS5-7793).
* [#6503](https://github.com/IntelRealSense/librealsense/pull/6503) - **Linux**: Adjust fix for build with GCC 5.3.
* [#6539](https://github.com/IntelRealSense/librealsense/pull/6539) - **Libcurl**: Fix for non-default build configurations.

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable. (DSO-13700)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) v2.33.1 does not compile with -DBUILDEASYLOGGINGPP=OFF
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-13525) - [D400] 3D viewer moved when sliding the tare calibration sliders
* (RS5-7374) - [L515] Error after performing HW reset
* (RS5-6586) - [L515] Corrupted Depth and IR  
* (DSO-15118) - [D400] Viewer is closed forcibly with cycling start/stop streaming in 3D view.

## Release 2.35.0
Release Date: 31 May 2020

### API Changes
https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2350

### New Features
* [#6480](https://github.com/IntelRealSense/librealsense/pull/6480) - **D4xx**: Firmware version 5.12.5.0.
* [#6176](https://github.com/IntelRealSense/librealsense/pull/6176) - **T265**: Firmware version 0.2.0.951.
   - Make initial yaw consistent when starting forward, backward, up and down.
   - Fix intermittent descriptor/imu corruption
* [#6205](https://github.com/IntelRealSense/librealsense/pull/6205) - **Extended cam sync mode to support full slave and genlock modes**

### Bug Fixes and Improvements
* [#6470](https://github.com/IntelRealSense/librealsense/pull/6470) - **Android**: Detach event was generated instead of Attach event. Addresses [#6452](https://github.com/IntelRealSense/librealsense/issues/6452), (DSO-15065,DSO-14493).
* [#6318](https://github.com/IntelRealSense/librealsense/pull/6318) - **MATLAB**: Add missing mapping for depth_frame::get_units()  contributed by [@mengyui](https://github.com/mengyui).
* [#6321](https://github.com/IntelRealSense/librealsense/pull/6321) - **Linux**: Fix aarch64/arm detection. Depending on the compiler, `-dumpmachine` can output any `aarch64-*` or `arm-*`, such as `aarch64-suse-linux` or `arm-suse-linux-gnueabi`, not only `aarch64-linux-gnu` or `arm-linux-gnueabihf`.) contributed by [@ggardet](https://github.com/ggardet).
* [#6434](https://github.com/IntelRealSense/librealsense/pull/6434) - **DQT**: UI fixes and enhancements (DSO-14283).
   - Fix UI units.
   - Log Plane Fit RMS % error metric) 
* [#6429](https://github.com/IntelRealSense/librealsense/pull/6429) - **Support FW Flash scheme 106**  (Required for FW v5.12.4.+).
* [#6308](https://github.com/IntelRealSense/librealsense/pull/6308) - **rs-convert** rework 
   - Switch to sensor callback API (except for ply export)
   - Assign file names based on frame timestamp (instead of frame number)
   - Generate metadata text file per frame
* [#6427](https://github.com/IntelRealSense/librealsense/pull/6427) - **Fix dead-lock on multi-threaded log invocations**  Addresses [#6231](https://github.com/IntelRealSense/librealsense/issues/6231), [#6393](https://github.com/IntelRealSense/librealsense/issues/6393) (DSO-15016).
* [#6420](https://github.com/IntelRealSense/librealsense/pull/6420) - **LRS Network Extensions**: Live555 3rd party compilation fix.
* [#6417](https://github.com/IntelRealSense/librealsense/pull/6417) - **Fix Memory Leak in frame-validator PB** (RS5-7715)
* [#6375](https://github.com/IntelRealSense/librealsense/pull/6375) - **Fix Syncer Memory Leak**  (Fix for [#6337](https://github.com/IntelRealSense/librealsense/issues/6337) contributed by [@MojamojaK](https://github.com/MojamojaK)
* [#6350](https://github.com/IntelRealSense/librealsense/pull/6350) - **Thermal Compensation** option provisioning (DSO-14980).
* [#6355](https://github.com/IntelRealSense/librealsense/pull/6355) - **Manual gain setting to override AE** (changing gain manually with Auto-Exposure on should disable AE instead of error), addresses [#5952](https://github.com/IntelRealSense/librealsense/issues/5952) 
(DSO- 14638).
* [#6328](https://github.com/IntelRealSense/librealsense/pull/6328), [#6188](https://github.com/IntelRealSense/librealsense/pull/6188) - **LRS Network Extensions**: Hot Fixes.
* [#6315](https://github.com/IntelRealSense/librealsense/pull/6315) - **Disable creation of unnecessary log files** Configure filename for logging ONLY if it was requested, in which case `minimum_file_severity` is different than `RS2_LOG_SEVERITY_NONE`.) contributed by [@AndrejOrsula](https://github.com/AndrejOrsula).
* [#6299](https://github.com/IntelRealSense/librealsense/pull/6299) - **GlSL occlusion**  (implement occlusion removal on gpu with glsl.
* [#6305](https://github.com/IntelRealSense/librealsense/pull/6305) - **Add notification for L500 corrupted frames**.
* [#6143](https://github.com/IntelRealSense/librealsense/pull/6143) - **Android**: Fix YUYV preview for the RGB stream in camera app.
* [#6288](https://github.com/IntelRealSense/librealsense/pull/6288) - **CMake** Set depth invalidation enabled by default.
* [#6290](https://github.com/IntelRealSense/librealsense/pull/6290) - **Win metadata script** fix
(DSO-14805, DSO-14653).
* [#6203](https://github.com/IntelRealSense/librealsense/pull/6203) - **Fix RSUSB messaging takes 20 msec**  (fix signalling in concurrency.h invoke_and_wait function. Was waiting until timeout and missing the signal, Addresses [#6206](https://github.com/IntelRealSense/librealsense/issues/6206).
* [#6198](https://github.com/IntelRealSense/librealsense/pull/6198) - **Python: add log_to_callback** add rs2::log_message, rs2::log_to_callback() and rs2::log() to python wrapper.


### Documentation
* [#6450](https://github.com/IntelRealSense/librealsense/pull/6450) - **Update rs_frame.hpp**  (Clarify get_timestamp()'s behavior.) contributed by [@krazycoder2k](https://github.com/krazycoder2k).
* [#6263](https://github.com/IntelRealSense/librealsense/pull/6263) - **Fixes Typos**  () contributed by [@himanshugarg](https://github.com/himanshugarg).
* [#6200](https://github.com/IntelRealSense/librealsense/pull/6200) - **Fixed minor comment typo**. Resolves  [#5872](https://github.com/IntelRealSense/librealsense/issues/5872) contributed by [@krazycoder2k](https://github.com/krazycoder2k).


### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable. (DSO-13700)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) v2.33.1 does not compile with -DBUILDEASYLOGGINGPP=OFF
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-13524) - Viewer crash when running Update Unsigned FW with signed FW image (unlocked units only)
* (DSO-13525) - 3D viewer moved when sliding the tare calibration sliders

## Release 2.34.0
Release Date: 31 Mar 2020

### API Changes
https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2340

### New Features and Enhancements
* [#6136](https://github.com/IntelRealSense/librealsense/pull/6136) - **RealSense Device over Ethernet**  (from [#5999](https://github.com/IntelRealSense/librealsense/pull/5999)) (CAMOE-11) *Alpha*
  - `rs-server` tool is a stand-alone application for streaming Depth and RGB sensors. Currently the server provides partial functionality for D415 and D435 cameras, on Linux only. 
  - A new extension module `realsense2-net` was introduced to encapsulate depth camera streaming and management over network. Configured with `BUILD_NETWORK_DEVICE` Cmake flag, currently limited to Linux and Windows OS. 
* [#6026](https://github.com/IntelRealSense/librealsense/pull/6026) - **OpenVINO Face Detection** toolkit is integrated into `realsense-viewer` (DSO-13910) - Requires Windows SDK Installer, not included in the standalone viewer. 
* [#6097](https://github.com/IntelRealSense/librealsense/pull/6097) - **On-Chip Calibration (OCC) fine-tuning** (DSO-14650):  
  - OCC health check error for values <0  is now based on error magnitude.
  - OCC More Options, White Wall is set as default for D415.
  - Tare-cal, The Avg step default values when you hover on the name are now compatible with the number shown (20).
  - Tare is set to last value the user typed.
  - Error messages is shifted slightly to the left and the box is bigger.
  - Progress bar during Tare is updated.
* [#6118](https://github.com/IntelRealSense/librealsense/pull/6118) - [Software Device] **Add API to break circular dependency with Active Object**  
  - The new `rs2_software_sensor_detach` function should be called on all instances of `rs2::software_sensor` stored inside the Active Object.
* [#6000](https://github.com/IntelRealSense/librealsense/pull/6000) - [L500] **Add HW Sync Enable control** (RS5-6978)
* [#6109](https://github.com/IntelRealSense/librealsense/pull/6109) - [rs-fw-logger] **Parse parametric floating point input** (RS5-7008)
* [#6098](https://github.com/IntelRealSense/librealsense/pull/6098) - [CMake] **Make firmware URL overrideable**  (as proposed in [5114](https://github.com/IntelRealSense/librealsense/issues/5114) by [@mikepurvis](https://github.com/mikepurvis))  
  - Permits the firmware binaries to be mirrored on-site for more restrictive CI environments that do not permit external network access at build time.  
* [#5996](https://github.com/IntelRealSense/librealsense/pull/5996) - [API] **Add depth_frame::get_units()**  convenience API  
* [#5997](https://github.com/IntelRealSense/librealsense/pull/5997) - [SR305] **Fix device designation** (DSO-14170) 
* [#6006](https://github.com/IntelRealSense/librealsense/pull/6006) - [D400] **Added emmitter always on option** (DSO-14265)  
* [#5879](https://github.com/IntelRealSense/librealsense/pull/5879) - [Core] **Establish 0x0B5B, 0xB5C SKUs** (DSO-14577)  
* [#5961](https://github.com/IntelRealSense/librealsense/pull/5961) - [API] Add **rs2_allocate_synthetic_motion_frame** (DSO-14645)  

 ### Bug Fixes and Improvements
* [#6161](https://github.com/IntelRealSense/librealsense/pull/6161) - [Video4Linux] **Fix broken activation of custom deleter in RAII**.  Ensure custom deleter is called by passing non-null pointer in ctor. Contributed by [@anmelleSlamcore ](https://github.com/anmelleSlamcore).
* [#6149](https://github.com/IntelRealSense/librealsense/pull/6149) - [Software Device] **invoke pixels deleter**.  Make sure frame deleter is called even if no streaming is active.
* [#6151](https://github.com/IntelRealSense/librealsense/pull/6151) - [Python] **revert save_to_ply options to properties** (using properties with getter functions fixes static compilation)
* [#6137](https://github.com/IntelRealSense/librealsense/pull/6137) - [EasyLogging] **Fix logger activation** (Fix typo)
* [#6133](https://github.com/IntelRealSense/librealsense/pull/6133) - [MSVC] **Visual Studio 2019 compilation fix**
* [#6040](https://github.com/IntelRealSense/librealsense/pull/6040) - [RaspberryPi4] **Update installation script for Raspbian Buster**
* [#6043](https://github.com/IntelRealSense/librealsense/pull/6043) - [Global Time] **Handle get_device_time delay**  (occasionally the may takes up to ~250 ms resulting in frame drops).
* [#6037](https://github.com/IntelRealSense/librealsense/pull/6037) - [Metadata] **Fix time domain handling** (DSO-13182, DSO-14314) 
  - (Track and update metadata presence continuously to handle cases where v4l driver produces zeros
* [#6083](https://github.com/IntelRealSense/librealsense/pull/6083) - **Fix 100% CPU usage when using libusb**  
  - Replace broken dispatcher with a thread to fix 100% CPU usage. Addresses [#5783](https://github.com/IntelRealSense/librealsense/issues/5783), [#6062](https://github.com/IntelRealSense/librealsense/issues/6062).
* [#6029](https://github.com/IntelRealSense/librealsense/pull/6029) - [D435i] **Fix imu motion correction**  
  - Motion Correction is calculated and to be applied in the same CS as the depth sensor
* [#6022](https://github.com/IntelRealSense/librealsense/pull/6022) - **Odroid kernel patch scripts update** contributed by [@chlakshminarayana](https://github.com/chlakshminarayana)
* [#5991](https://github.com/IntelRealSense/librealsense/pull/5991) - [Android]**Fix for USB disconnect-recovery flow** (DSO-14132)
* [#6064](https://github.com/IntelRealSense/librealsense/pull/6064) - []API **Fix Emitter_On option** (DSO-14265)
* [#6044](https://github.com/IntelRealSense/librealsense/pull/6044) - [Matlab] **Fix broken include in wrapper**
* [#6021](https://github.com/IntelRealSense/librealsense/pull/6021) - [Python] **Add missing cpp file into CMakeLists**
* [#5922](https://github.com/IntelRealSense/librealsense/pull/5922) - [C++] **Dynamic cast compatibility** contributed by [@militaryCoder](https://github.com/militaryCoder)
* [#5970](https://github.com/IntelRealSense/librealsense/pull/5970) - [Matlab] **Matlab bindings fixes**  (Address [#5906](https://github.com/IntelRealSense/librealsense/issues/5906), [#4453](https://github.com/IntelRealSense/librealsense/issues/4453), [#5236](https://github.com/IntelRealSense/librealsense/issues/5236) (DSO-14313)
* [#5977](https://github.com/IntelRealSense/librealsense/pull/5977) - [Metadata] **Minor fixes and enhancements**  
  - Fix the behaviour of "Enable Metadata" button on Windows
  - Add horizontal and vertical FOV to `rs-enumerate-devices`
* [#5988](https://github.com/IntelRealSense/librealsense/pull/5988) - [T265] **Fix default USB permissions for T265 (Android)**  contributed by [@smartynenko](https://github.com/smartynenko)
* [#5622](https://github.com/IntelRealSense/librealsense/pull/5622) - [C#] **C# Wrapper Reference Counting for Sensor/Device**.  Fixes [#5369](https://github.com/IntelRealSense/librealsense/issues/5369), contributed by [@JBBee](https://github.com/JBBee)
* [#5333](https://github.com/IntelRealSense/librealsense/pull/5333) - [Software Device] **Enhancement**  Fix python wrapper FW update callback (DSO-14348)
* [#5579](https://github.com/IntelRealSense/librealsense/pull/5579) - [T265] **Updated T parameters in rotated camera odometry example.** contributed by [@krazycoder2k](https://github.com/krazycoder2k)
* [#5483](https://github.com/IntelRealSense/librealsense/pull/5483) - [ROS] **remove rosdep 'linux-headers-generic'**  contributed by [@christian-rauch](https://github.com/christian-rauch)
* [#5665](https://github.com/IntelRealSense/librealsense/pull/5665) - [C++] **notification registration route to base sensor**.  Fixes [#5479](https://github.com/IntelRealSense/librealsense/issues/5479)  
* [#5853](https://github.com/IntelRealSense/librealsense/pull/5853) - [C#] **Add the missing  distortion fisheye model**  contributed by [@mengyui](https://github.com/mengyui)  
* [#5910](https://github.com/IntelRealSense/librealsense/pull/5910) - [Android] **Handle Resources deallocation**  
* [#5921](https://github.com/IntelRealSense/librealsense/pull/5921) - [Core] **Downgrade UVC warning messages**  
* [#5929](https://github.com/IntelRealSense/librealsense/pull/5929) - [Core] **Typo in `rs-ar-advanced.cpp`**  contributed by [@pjessesco](https://github.com/pjessesco)


### Documentation
* [#6158](https://github.com/IntelRealSense/librealsense/pull/6158) - **Depth cameras support matrix**  migrated to https://dev.intelrealsense.com/docs/sdk-knowledge-base

### Known Issues
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable. (DSO-13700)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [#6009](https://github.com/IntelRealSense/librealsense/issues/6009) v2.33.1 does not compile with -DBUILDEASYLOGGINGPP=OFF
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-13524) - Viewer crash when running Update Unsigned FW with signed FW image (unlocked units only)
* (DSO-13525) - 3D viewer moved when sliding the tare calibration sliders


## Release 2.33.1
Release Date: 1 Mar 2020

### Enhancements

* [#5946](https://github.com/IntelRealSense/librealsense/pull/5946) - **FW 5.12.3.0 for D4xx Devices**  Stability and Power Management fixes and enhancements

* [#5741](https://github.com/IntelRealSense/librealsense/pull/5741) - **Visual presets and new options for L500** (RS5-6455):  
        **Options:**  
        - confidence,  
        - post_processing_sharpness ,  
        - pre_processing_sharpness ,  
        - noise_filtering ,
        - avalanche_photo_diode,  
        - laser_gain,  
        - min_distance,
        - invalidation_bypass,  
        - ambient_light  
        **Presets:**  
        - RS2_L500_VISUAL_PRESET_NO_AMBIENT,  
        - RS2_L500_VISUAL_PRESET_LOW_AMBIENT,  
        - RS2_L500_VISUAL_PRESET_MAX_RANGE,  
        - RS2_L500_VISUAL_PRESET_SHORT_RANGE  
        **Serialization support:**  
        - save and load options/presets with JSON.

* [#5584](https://github.com/IntelRealSense/librealsense/pull/5584) - **log_to_callback + unit-tests**:  
Fixes OpenVino test-cases in static (non-shared) builds.  
Fixes some of the warnings repeatedly given (from headers) during compilation.  
Travis "Linux - cpp" build is now "Linux - cpp - static" and uses static (non-shared; BUILD_SHARED_LIBS is off) compilation.  
Added unit-testing mechanism:
  - Any test-\*.cpp (and, in future, test-*.py, etc.) under unit-tests/ is a unit-test
  - Tests can be nested inside directories
  - Each test creates its own project (in Visual Studio under Unit-Tests, with same nested structure)   and thus its own executable
  - A script (unit-tests/run-unit-tests.py) runs all unit-tests and exits with status 1 or 0
  - Unit-tests can be specifically shared or static
- Unit-tests are now run in Travis, in both shared and static builds
- BUILD_SHARED_LIBS is now a compiler definition, too
- Added rs2::log_to_callback, rs2_log_to_callback, rs2_log_to_callback_cpp
  - Minimum level can be set for a callback (e.g., warnings and above)
  - Added RS2_LOG_SEVERITY_ALL, same as _DEBUG, so it's easier to say "log all messages"
  - 21 unit-tests under unit-tests/log/

* [#5751](https://github.com/IntelRealSense/librealsense/pull/5751) - **Linux Kernel 5 and 5.3 fixes and enhancements** (DSO-14299):  
 - Fixes:
    - UVC and metadata node matching shall use non-lexicographic sort in v4l. Applicable for kernels 4.16+.  
   - Enforce Video/Metadata sync by using two-stage blocking calls. This replaces I/O multiplexing to ensure the pairing of video and meta nodes payloads.  
   - Check libusb return value to prevent null de-referencing and segfault.  
   - Enforce Metadata  polling is performed when invalid video buffer is encountered to ensure Video/Metadata node sync.
   - Fix hardware fps calculation when the frame number being reset internally by the FW, such as in `SCP Overflow` case.  
 - Enhancements:
   - Make unified kernel patches for LTS v5.0 and v5.3.
   - Re-enable unattended patch by overriding `patch --merge` inconsistency with try/apply. Github [#5710](https://github.com/IntelRealSense/librealsense/issues/5710)
   - Adjust metadata validation heuristics in SKU-neutral manner to allow for D400, SR300 and L500 md payloads.
   - Check  Metadata/Video nodes buffers synchronization by comparing the kernel sequence buffers
- Addresses [#5319](https://github.com/IntelRealSense/librealsense/issues/5319), [#4543](https://github.com/IntelRealSense/librealsense/issues/4543). Relevant for the following ROS issues [1024](https://github.com/IntelRealSense/realsense-ros/issues/1024), [1047](https://github.com/IntelRealSense/realsense-ros/issues/1047), [1060](https://github.com/IntelRealSense/realsense-ros/issues/1060), [492](https://github.com/IntelRealSense/realsense-ros/issues/492).

* [LabVIEW Package](https://realsense-hw-public.s3-eu-west-1.amazonaws.com/Releases/RS4xx/Windows/labview_2_33_0.zip) ** update with SDK v2.33.0**  

* [#5796](https://github.com/IntelRealSense/librealsense/pull/5796) - **Syncer to bypass IMU frames for L500** (RS5-5558):  
  - Added composite_identity_matcher that passes frames to callback without synchronize them.

* [#5792](https://github.com/IntelRealSense/librealsense/pull/5792) - **Android streamer start time increase fix** (DS5U-4538, DSO-14302):
   -   (Autoclosable try added for getting device into Updatable - bug was only in the Android wrapper.

* [#5789](https://github.com/IntelRealSense/librealsense/pull/5789) - **Android multicam fix** (DSO-14133):
  - Start/stop multicam application fixed

* [#5780](https://github.com/IntelRealSense/librealsense/pull/5780) - **RS2_OPTION_FREEFALL_DETECTION_ENABLED** (RS5-6461):
  - When an L500 camera experiences free-fall (is dropped) a safety mechanism is triggered and turns off the depth sensor to protect moving parts inside the camera.

* [#5698](https://github.com/IntelRealSense/librealsense/pull/5698) - **#4297 Multicamera IMU data mix up** (DSO-13711):  
  - HID devices now use the unique-ID assigned to their parent node (which is the USB node), letting them be properly associated with the proper composite device.  
  - Multiple HID cameras should be identified correctly.
  - Addresses [#4297](https://github.com/IntelRealSense/librealsense/issues/4297)

* [#5801](https://github.com/IntelRealSense/librealsense/pull/5801) - **rs-fw-logger - regression fix** (DSO-14405) 

* [#5716](https://github.com/IntelRealSense/librealsense/pull/5716) - **rs-enumerate-devices fixes and enhancements** (DSO-14190):  
 Revert `-s` option to invoke a one-line description per device.  
 Add `-S` to provide the device node data (used to be `-s`)  
 Addresses [#5423](https://github.com/IntelRealSense/librealsense/issues/5423)  
 
* [#5768](https://github.com/IntelRealSense/librealsense/pull/5768) - **On-Chip and Tare Calibration Fixes**:  
Minor fixes and quality of life improvements for OCC and Tare features
  
* [#5791](https://github.com/IntelRealSense/librealsense/pull/5791) - **Disable all L500 depth processing blocks except for the Temporal Gilter**

* [#5785](https://github.com/IntelRealSense/librealsense/pull/5785) - **Fix typo**  (apriltag_pose_destory -> apriltag_pose_destroy) contributed by [@pjessesco](https://github.com/pjessesco)
* [#5645](https://github.com/IntelRealSense/librealsense/pull/5645) - **T265 Serial Number Compatability**:  
  Keep the serial number of the T265 compatible with the `libtm` format (`8XXXXXXXXXXX` rather than `00008XXXXXXXXXXX`).  By [@radfordi](https://github.com/radfordi)
* [#5889](https://github.com/IntelRealSense/librealsense/pull/5889) - **Fix memory leak** in v4l2 backend with kernel 4.16+. 
* [#5923](https://github.com/IntelRealSense/librealsense/pull/5923) - **License for  Windows INF file** update.  Addresses [#5809](https://github.com/IntelRealSense/librealsense/issues/5809)


**Community Contribution**:  
* [#5750](https://github.com/IntelRealSense/librealsense/pull/5750) - **Ill-defined for loop fix**. by [@JTrantow](https://github.com/JTrantow)
* [#5769](https://github.com/IntelRealSense/librealsense/pull/5769) - **Update camera renderer**:  
 Make SR305 and L500 appear correctly in the 3D view.

 * [#5623](https://github.com/IntelRealSense/librealsense/pull/5623) - **One Viewer Context**:  
Avoid creating multiple unused `rs2::context`s.
* [#5747](https://github.com/IntelRealSense/librealsense/pull/5747) - **Remove the std::move() on const. See Issue5746.**:  
  Resolves [#5746](https://github.com/IntelRealSense/librealsense/issues/5746)) contributed by [@JTrantow](https://github.com/JTrantow)
* [#5702](https://github.com/IntelRealSense/librealsense/pull/5702) - **Fix for conversion from RGB to BGR in the OpenCV wrapper helpers file**:  
  Related to [#5701](https://github.com/IntelRealSense/librealsense/issues/5701).  
  Without converting to a seperate `cv::Mat` object, the conversion would not happen on my machine. This seems to be the case for other users, see [this example.](https://answers.opencv.org/question/199603/problem-with-intel-realsense-sdk-20-and-cvcvtcolor/)). Contributed by [@cedriclmenard](https://github.com/cedriclmenard)
* [#5724](https://github.com/IntelRealSense/librealsense/pull/5724) - **Fix typos**.  Contributed by [@ruffsl](https://github.com/ruffsl)
* [#5734](https://github.com/IntelRealSense/librealsense/pull/5734) - **Fix what appears to be a copy/paste redundant code problem**:  
Addresses [#5733](https://github.com/IntelRealSense/librealsense/issues/5733) - Change second conditional to test values_ir.size(). By [@JTrantow](https://github.com/JTrantow)


## Release 2.32.1
Release Date: 23 Jan 2020

### Enhancements

[#5678](https://github.com/IntelRealSense/librealsense/pull/5678) - **Enable metadata with a single click on Windows**
UVC frame metadata on Windows is causing a lot of questions and confusion, adding a single click solution that would be applicable from within the Viewer.  contributed by [@dorodnic](https://github.com/dorodnic)

[#5700](https://github.com/IntelRealSense/librealsense/pull/5700) - **Upgrade D4XX firmware to 5.12.2.100** 
- Maintenance update: performance and stability improvements

[#5687](https://github.com/IntelRealSense/librealsense/pull/5687) - **Upgrade T265 firmware to 0.2.0.926** 
- Fix map load hangs
- Fix USB serial number (remove trailing zeros)
- Support for `remove_static_node`
- Fix map export hangs based on map sizes ([#5394](https://github.com/IntelRealSense/librealsense/issues/5394))
- Fix immediate NaNs based due to a specific initial condition
- Fix export without import or start
- Allow export of imported but not started maps

[#5213](https://github.com/IntelRealSense/librealsense/pull/5213) - **Replace libtm with direct communication with T265**  This PR removes libtm completely and makes T265 a first class driver in librealsense. In more detail, it:
- Removes libtm and remnants of older products and directly communicates with T265
- Uses the librealsense usb abstraction for booting T265 and communicating with it
- Unifies firmware download into common/fw
- Fixes many issues on macOS
- Fixes multi-process issues caused by libtm greedily claiming the device
- Adds hardware reset support
- Allows export of map while running
- Logs an error when the user tries to stream video data over USB 2 connections
- Fixes the pipeline resolution bug mentioned in [#4506](https://github.com/IntelRealSense/librealsense/issues/4506)

Contributed by [@bfulkers-i](https://github.com/bfulkers-i)

[#5356](https://github.com/IntelRealSense/librealsense/pull/5356) - **T2XX sample: new `ar-advanced` sample to show map import/export and get/set static node APIs**  
* Import localization map from raw data file before starting T2xx tracking.
* Export localization map to raw data file after T2xx tracking ended.
* Command line options to specify raw data file paths for the above map import/export.
* Set up a callback to receive relocalization event from the device and action after the event.
* Get static node from imported localization map after relocalization event detected.
* Set static node before localization map exported.

Contributed by [@honpong](https://github.com/honpong)

[#5468](https://github.com/IntelRealSense/librealsense/pull/5468) - **Add sensor extensions** 
Add color_sensor, motion_sensor and fisheye_sensor extensions.
Enable the option to `dev.first<rs2::color_sensor>()` or `sensor.is<rs2::color_sensor>()` etc. Contributed by [@doronhi](https://github.com/doronhi)

[#5529](https://github.com/IntelRealSense/librealsense/pull/5529) - **.NET VideoStreamProfile.Clone added**  
Cloning a profile is sometimes needed when writing custom processing blocks. Contributed by [@ogoshen](https://github.com/ogoshen)

[#5419](https://github.com/IntelRealSense/librealsense/pull/5419) - **Merge Android development branch** 
Adds the following features:
- Terminal
- FW Logger
- FW Backup
- Extend stream stats
- Basic Controls tab - Emitter mode only for now

Fixes issues:
- Pipeline memory leak
- Recordings functionality
- Permissions issues

### Bug Fixes

[#5691](https://github.com/IntelRealSense/librealsense/pull/5691) - **Fix possible bug in device-hid detection**
Comparison to capacity(), which can be greater than size(), can lead to wrong logic contributed by [@maloel](https://github.com/maloel)

[#5639](https://github.com/IntelRealSense/librealsense/pull/5639) - **T265 time sync: filter outliers**
Global timestamp will show deviation due to global timestamp base adjustment every 500ms, contributed by [@cchen6](https://github.com/cchen6)

[#5597](https://github.com/IntelRealSense/librealsense/pull/5597) - **VAAPI HEVC Main10 hardware depth encoding example** contributed by [@bmegli](https://github.com/bmegli)

[#5586](https://github.com/IntelRealSense/librealsense/pull/5586) - **Add support for POWER9 CPUs on Linux**
Tested on a Raptor Computing Blackbird motherboard with an IBM POWER9 CPU, running Void Linux PPC. Contributed by [@AlbertoGP](https://github.com/AlbertoGP)

[#5626](https://github.com/IntelRealSense/librealsense/pull/5626) - **Adding links to community projects**
* Linking to [Raspberry Pi Handheld 3D Scanner](https://eleccelerator.com/pi-handheld-3d-scanner/) blog-post by @frank26080115
* Linking to  [Erwhi Hedgehog](https://gbr1.github.io/erwhi_hedgehog.html) by @gbr1

[#5589](https://github.com/IntelRealSense/librealsense/pull/5589) - **L500 duplicated IR frame fix**  
IR frame was processed from both IR-id and from zero order processing blocks.
Now IR frame is not passed-through by default when zero order is disabled
Tracked-on: RS5-6159

[#5677](https://github.com/IntelRealSense/librealsense/pull/5677) - **Prevent UVC frame overflow with v4l**  Add heuristic to drop UVC overflow frames with v4l kernel prior to v4.16
Handle GCC pedantic
Tracked on: DSO-14370

[#5627](https://github.com/IntelRealSense/librealsense/pull/5627) - **Remove Accelerometer 50Hz profile**  (Tracked-on: RS5-5473)

[#5636](https://github.com/IntelRealSense/librealsense/pull/5636) - **Fix for memory overrun when parsing metadata** 
Trim frame size when the metadata is present but invalid
Add heuristics to validate metadata existence. (assume d4xx format)
Tracked on : DSO-14292

[#5637](https://github.com/IntelRealSense/librealsense/pull/5637) - **Include stddef in usbhost.h** 
`usbhost.h` uses `size_t`, which is defined in `stddef.h`. This change includes `stddef.h` header. Contributed by [@jonberling](https://github.com/jonberling)

[#5534](https://github.com/IntelRealSense/librealsense/pull/5534) - **Fix motion and motion correction routines**  
- Fix reported HID frame size required for unpacker
- Motion correction and handling:
- Query motion correction option at run-time
- Assign the intrinsic data to the processing block and switch to cached data
- Fix data flow management
- Move exception handling to initialization
- Assign default MM axis rotation for unsupported SKUs
Addresses  [#5515](https://github.com/IntelRealSense/librealsense/issues/5515), possibly [#5496](https://github.com/IntelRealSense/librealsense/issues/5496), [#5498](https://github.com/IntelRealSense/librealsense/issues/5498)) contributed by [@ev-mp](https://github.com/ev-mp)

[#5574](https://github.com/IntelRealSense/librealsense/pull/5574) - **Added action_delayer and remove gamma correction control.**  
1. Added action_delayer to enable delayed action
2. Remove gamma correction control from RGB sensor

[#5264](https://github.com/IntelRealSense/librealsense/pull/5264) - **Update installation_osx.md**  (Make it work on Catalina) contributed by [@neilyoung](https://github.com/neilyoung)

[#5155](https://github.com/IntelRealSense/librealsense/pull/5155) - **update pyglet to 1.4.x** 
The pyglet class pyglet.clock.ClockDisplay has removed in 1.4.x. Use pyglet.window.FPSDisplay instead. Addresses [#255](https://github.com/los-cocos/cocos/issues/255). Apply the changes from [#3887](https://github.com/IntelRealSense/librealsense/issues/3887)
Contributed by [@mengyui](https://github.com/mengyui)

[#5387](https://github.com/IntelRealSense/librealsense/pull/5387) - **polling_device_watcher: fix race between construction and start**
Device watchers do not notify for devices that already exist when they are constructed (e.g. `win_event_device_watcher`), but polling_device_watcher was also not notifying if devices were added between construction and start. This aligns polling_device_watcher with `win_event_device_watcher`.
Contributed by [@bfulkers-i](https://github.com/bfulkers-i)

[#5444](https://github.com/IntelRealSense/librealsense/pull/5444) - **CMake: unix_config, set CMAKE_POSITION_INDEPENDENT_CODE**  
And remove manually set `fPIC`. `CMAKE_POSITION_INDEPENDENT_CODE` properly sets `fPIC` for libraries and `fPIE` for executables.
Contributed by [@jirislaby](https://github.com/jirislaby)

[#5443](https://github.com/IntelRealSense/librealsense/pull/5443) - **common: fw-update-helper, don't compare addresses**  
`create_default_fw_table` tries to compare `""` with another string. But both are addresses. Use `strlen` in that case. Issue: [#5525](https://github.com/IntelRealSense/librealsense/issues/5525), Contributed by [@tylerjw](https://github.com/tylerjw)

[#5521](https://github.com/IntelRealSense/librealsense/pull/5521) - **Fix extrinsics commutativity**  
Manually create a new stream profile for every clone needed by the sensor while initializing the stream profiles, instead of cloning via the raw profile. Cloning the profiles caused extrinsic registration with incomplete profiles.
Addresses [#5451](https://github.com/IntelRealSense/librealsense/issues/5451)

[#5522](https://github.com/IntelRealSense/librealsense/pull/5522) - **Fix recording crash** 
Recording unsubscribe signal was not called properly, causing sensor hooks to be called even after the record device object was destroyed.

[#5421](https://github.com/IntelRealSense/librealsense/pull/5421) - **Typo removed**  
Contributed by [@neilyoung](https://github.com/neilyoung)


## Release 2.31.0
Release Date: 9 Dec 2019

### API Changes
TBD

### Bug-fixes and Enhancements

* [#5402](https://github.com/IntelRealSense/librealsense/pull/5402) - *Promote recommended D400 firmware to 5.12.1.0* contributed by [@ev-mp](https://github.com/ev-mp)
* [#5360](https://github.com/IntelRealSense/librealsense/pull/5360) - *Add rs-dnn-vino sample* (rs-dnn-vino
This example demonstrates OpenVINO™ toolkit integration with object detection, using
basic depth information to approximate distance) contributed by [@maloel](https://github.com/maloel)
* [#5377](https://github.com/IntelRealSense/librealsense/pull/5377) - *Change default RGB resolution* (Default change to HD 30) contributed by [@arilowen](https://github.com/arilowen)
* [#5386](https://github.com/IntelRealSense/librealsense/pull/5386) - *Warning fixes* (Fixes a few minor warnings encountered on macOS) contributed by [@bfulkers-i](https://github.com/bfulkers-i)
* [#5399](https://github.com/IntelRealSense/librealsense/pull/5399) - *Fix xhci_build flags handling* (Limit the xhci_patch to LTS v4.4 only, improve robustness. The bug fix resolved in v4.18 is being actively back-ported by Ubuntu, e.g 4.4.0-170. Assume that this may occur for other kernel branches as well) contributed by [@ev-mp](https://github.com/ev-mp)
* [#5380](https://github.com/IntelRealSense/librealsense/pull/5380) - *fix openni2 wrapper convertDepthToColorCoordinates* (Оnly intrinsics are used in the function `Rs2Stream::convertDepthToColorCoordinates`, which leads to a small error due to the fact that the depth and color cameras are offset relative to each other) contributed by [@DarkCon](https://github.com/DarkCon)
* [#5325](https://github.com/IntelRealSense/librealsense/pull/5325) - *Update t265_rpy.py* (Reverting regression regarding negative signs introduced with last commit to this PR. The negation of z and y is required in order to obtain similarity to the previous sample code (used in the ArduPilot project)) contributed by [@neilyoung](https://github.com/neilyoung)
* [#5208](https://github.com/IntelRealSense/librealsense/pull/5208) - *Option to preserve T265 maps in memory for subsequent starts* contributed by [@radfordi](https://github.com/radfordi)
* [#5370](https://github.com/IntelRealSense/librealsense/pull/5370) - *Update tinyfiledialog to v3.4.1 and set map extension* (The version of tinyfiledialog we have doesn't allow by extension file selection on macOS (see [#5245](https://github.com/IntelRealSense/librealsense/issues/5245) and [#5196](https://github.com/IntelRealSense/librealsense/issues/5196)). Even the newest version doesn't seem to allow `*.*` selection, so this PR introduces the `.map` extension of T265 localization maps) contributed by [@bfulkers-i](https://github.com/bfulkers-i)
* [#5283](https://github.com/IntelRealSense/librealsense/pull/5283) - *Openvino sample* (This example demonstrates OpenVINO™ toolkit integration with facial detection, using
basic depth information to approximate distance) contributed by [@maloel](https://github.com/maloel)
* [#5346](https://github.com/IntelRealSense/librealsense/pull/5346) - *Added API for depth auto calibration.* (Added auto_calibrated_device extension for on-chip (plane fit RMS) and tare calibration (absolute distance). Use this API in viewer and added example on python for auto calibration. Fixed viewer to put the default resolution on top and fixed default resolution in D435) contributed by [@aangerma](https://github.com/aangerma)
* [#5344](https://github.com/IntelRealSense/librealsense/pull/5344) - *Android add pipeline profile partial support* (Only get device function is supported for now) contributed by [@arilowen](https://github.com/arilowen)
* [#5352](https://github.com/IntelRealSense/librealsense/pull/5352) - *Version compatibility enhancement*. Relax version compatibility constrain from strict identity to the standardized convention: 
  1. The versions are compatible when the majors align and the version minors hold (lib_ver >= exe_ver) 
  2. Patch number version does not affect compatibility. 
* [#5353](https://github.com/IntelRealSense/librealsense/pull/5353) - *Synchronize D400 devices using timestamp by default, and not frame counter* contributed by [@arilowen](https://github.com/arilowen)
* [#5234](https://github.com/IntelRealSense/librealsense/pull/5234) - *Upgrade T265 firmware to 0.2.0.879*  contributed by [@radfordi](https://github.com/radfordi)
  1. Double map size. 
  2. Fix loading maps with a previously loaded map that hadn't relocalized [#4593](https://github.com/IntelRealSense/librealsense/issues/4593) 
  3. Relocalization significantly improved for areas up to 50 sq. m: testing indicates fast (< 5 seconds) relocalization for typical environments and usage with non-static T265 device.
  4. Addressing [#4593](https://github.com/IntelRealSense/librealsense/issues/4593) – [T265] Map corruption after repeated export and import
* [#4275](https://github.com/IntelRealSense/librealsense/pull/4275) - *Fixed inconsistent return type* (Fixes the following error (GNU Make 4.2.1): `error: inconsistent types 'bool' and 'int' deduced for lambda return type`) contributed by [@battlecry231](https://github.com/battlecry231)
* [#5331](https://github.com/IntelRealSense/librealsense/pull/5331) - *Fix global timestamp domain query crash* (DSO-13980 - Add missing global timestamp case to timestamp domain enum.) contributed by [@arilowen](https://github.com/arilowen)
* [#5334](https://github.com/IntelRealSense/librealsense/pull/5334) - *Fix a minor bug in sorting streams* (Assumes the ordering should be by format first, then index, then
stream number.) contributed by [@bfulkers-i](https://github.com/bfulkers-i)
* [#5336](https://github.com/IntelRealSense/librealsense/pull/5336) - *Fix save_to_ply symbols in python* (The core issue is that `static const` members are not instantiated anywhere python can access, so taking a reference to them doesn't work. Fix that by creating lambdas that return the value) contributed by [@bfulkers-i](https://github.com/bfulkers-i)
* [#5337](https://github.com/IntelRealSense/librealsense/pull/5337) - *Add __version__ to python wrapper*  contributed by [@bfulkers-i](https://github.com/bfulkers-i)
* [#5312](https://github.com/IntelRealSense/librealsense/pull/5312) - *Android multicam example* (- GLSurface cleans its view before each frame arrives. a. Extend wrapper API. b. Add support for multi cameras. c. Add multicamera example) contributed by [@arilowen](https://github.com/arilowen)
* [#5170](https://github.com/IntelRealSense/librealsense/pull/5170) - *.NET Development* (fix for [#5054](https://github.com/IntelRealSense/librealsense/issues/5054), [#5071](https://github.com/IntelRealSense/librealsense/issues/5071). Revert some c# sensor API changes back to non-generic) contributed by [@ogoshen](https://github.com/ogoshen)
* [#5200](https://github.com/IntelRealSense/librealsense/pull/5200) - *Add new functions to Python wrapper, update some more documentation* (Addresses [#5173](https://github.com/IntelRealSense/librealsense/issues/5173)) contributed by [@lramati](https://github.com/lramati)
* [#4720](https://github.com/IntelRealSense/librealsense/pull/4720) - *Automatically set supported profiles in viewer* (Added functionality to the realsense viewer: when the user picks a value (resolution / fps / format / stream) that isn't compatible with the current configuration, a new configuration that supports the chosen value is set) contributed by [@AnnaRomanov](https://github.com/AnnaRomanov)
* [#4396](https://github.com/IntelRealSense/librealsense/pull/4396) - *Smooth GlobalTimeStamp's corrections.* (prevents cases where, due to jumps in sampling, global timestamps difference is much greater then the original hw timestamp difference) contributed by [@doronhi](https://github.com/doronhi)
* [#5198](https://github.com/IntelRealSense/librealsense/pull/5198) - *Alternative, possibly simpler approach for obtaining pitch, roll and yaw from T265 pose in python* contributed by [@neilyoung](https://github.com/neilyoung)
* [#5244](https://github.com/IntelRealSense/librealsense/pull/5244) - *Wheeled Odometry Calibration Setup Examples* (Added basic wheeled odometry description / sample drawings/json to T265 documentation. ) contributed by [@krazycoder2k](https://github.com/krazycoder2k)
* [#5278](https://github.com/IntelRealSense/librealsense/pull/5278) - *Fix SR300 enumeration on linux* (DSO-13973, 
[#5230](https://github.com/IntelRealSense/librealsense/issues/5230), [#5233](https://github.com/IntelRealSense/librealsense/issues/5233), [#5219](https://github.com/IntelRealSense/librealsense/issues/5219)) contributed by [@matkatz](https://github.com/matkatz)
* [#5053](https://github.com/IntelRealSense/librealsense/pull/5053) - *Adding Support-Matrix and updating Jetson docs*. This PR introduces two new documentation enhancements: 
  1. Rewrite of [installation_jetson.md](https://github.com/dorodnic/librealsense/blob/jetson_doc/doc/installation_jetson.md) 
  2. Addition of [support-matrix.md](https://github.com/dorodnic/librealsense/blob/jetson_doc/doc/support-matrix.md) trying to capture the big picture of what features are available on which platforms)
* [#5111](https://github.com/IntelRealSense/librealsense/pull/5111) - *Sensor refactoring* (DSO-13626) 
  contributed by [@arilowen](https://github.com/arilowen)
  - Add Synthetic Sensor class.
  - Replace unpackers with processing blocks.
  - Add composite processing blocks
* [#5110](https://github.com/IntelRealSense/librealsense/pull/5110) - *Enhanced PLY exporter* contributed by [@AnnaRomanov](https://github.com/AnnaRomanov)
* [#5205](https://github.com/IntelRealSense/librealsense/pull/5205) - *Kernel patch adjustment for 4.4 branch* (The patch provides a new option to incorporate additional 4.13-upstreamed patches for usbcore and xhci-hcd modules on top of the basic patches suite. The additional patch is a retrofit of [patchwork.kernel.org/patch/11095737](https://patchwork.kernel.org/patch/11095737/). The patches allow to avoid sporadic errors reproduced during stress start/stop tests that can affect certain SKUs. Tracked on: RS-5440) contributed by [@ev-mp](https://github.com/ev-mp)
* [#5204](https://github.com/IntelRealSense/librealsense/pull/5204) - *Zero the high 32 bit of 64 bit imu timestamp.* contributed by [@aangerma](https://github.com/aangerma)
* [#5202](https://github.com/IntelRealSense/librealsense/pull/5202) - *Disable GLOBAL_TIME option* (Disable global timestamp by default for specific SKU) contributed by [@aangerma](https://github.com/aangerma)
* [#5179](https://github.com/IntelRealSense/librealsense/pull/5179) - *Include USB Host license* contributed by [@matkatz](https://github.com/matkatz)
* [#5190](https://github.com/IntelRealSense/librealsense/pull/5190) - *Fix link in t265.md* contributed by [@levingerdes](https://github.com/levingerdes)
* [#5306](https://github.com/IntelRealSense/librealsense/pull/5306) - *UE4 wrapper 4.24 update and Linux build* contributed by [@gaborpapp](https://github.com/gaborpapp)

## Release 2.30.0
Release Date: 4 Nov 2019

### API Changes
[link](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2300)

### New Features & Improvements
* [#4975](https://github.com/IntelRealSense/librealsense/pull/4975) - New Cross-platform user-space implementation for supported USB protocols named `rsusb`. The refactored classes replace the multiplicity of UVC device per-platform implementations (Windows, Unix, Android) with a single cross-platform code infrastructure.
  In order to support the UVC device requirements, some modification were introduced into `rsusb` API, mainly adding asynchronous API to the USB messenger.
  Core Features:
  - Asynchronous API added to `rsusb` (USB request).
  - Multiple implementations of libuvc (Win7 / Linux / Android) replaced with single implementation
  - HID device modified to work with the new asynchronous API.
  Impact:
  - A new CMake option named `FORCE_RSUSB_BACKEND` added replaces the `FORCE_LIBUVC` and `FORCE_WINUSB_UVC` flags are now marked as deprecated. 
  - An update to WinUSB driver was implemented. **Important** - The new driver must be installed in order to use librealsense 2.30.0 or newer SDK version on Windows 7. Installation of the new driver is performed via [librealsense Windows 7 installer](https://github.com/IntelRealSense/librealsense/releases/download/v2.30.0/Intel.RealSense.SDK-WIN7-2.30.0.1174.exe).

* [#5169](https://github.com/IntelRealSense/librealsense/pull/5169) - [T265] Firmware Upgrade to 0.2.0.857:
   - Numerical stability improvements in various NaN pose scenarios, can have positive effect on issues [#4518](https://github.com/IntelRealSense/librealsense/issues/4518), [#5101](https://github.com/IntelRealSense/librealsense/issues/5101), [realsense-ros #955](https://github.com/IntelRealSense/realsense-ros/issues/955)
   - Minor relocalization improvements (including better cross-device map compatibility), toward upcoming greater relocalization update.
* [#4936 ](https://github.com/IntelRealSense/librealsense/pull/4936 ) -	[T265] New notification category.(RS2_NOTIFICATION_CATEGORY_POSE_RELOCALIZATION), produced on first relocalization to an imported map
* [#5109](https://github.com/IntelRealSense/librealsense/pull/5109) - [T265] display USB port chain in physical port info. by @BriceRenaudeau
* [#4966](https://github.com/IntelRealSense/librealsense/pull/4966) - New face detection and depth-enabled anti-spoofing demo exhibiting machine learning algorithms with [DLIB](http://dlib.net/) toolkit (DSO-13630).
* [#4889](https://github.com/IntelRealSense/librealsense/pull/4889) - [T265] Adding Wheel Odometry python sample.
* [#4953](https://github.com/IntelRealSense/librealsense/pull/4953) - A link to community project that builds Android 
application with librealsense. @cabelo 
* [#4907](https://github.com/IntelRealSense/librealsense/pull/4907) - [Realsense-Viewer] User notification improvement when the rendering format is not supported.

### Bug Fixes
* [#5157](https://github.com/IntelRealSense/librealsense/pull/5157) - Prevent hex formatting contamination.
* [#5106](https://github.com/IntelRealSense/librealsense/pull/5106) - Acquire depth units from intrinsic. (RS5-5486)
* [#5077](https://github.com/IntelRealSense/librealsense/pull/5077) - On-chip calibration crash fix
* [#5066](https://github.com/IntelRealSense/librealsense/pull/5066) - [rosbag-inspector] Crash fix. (DSO-13665, DSO-13562). Addresses [#4704](https://github.com/IntelRealSense/librealsense/issues/4704), [#4932](https://github.com/IntelRealSense/librealsense/issues/4932)
* [#5065](https://github.com/IntelRealSense/librealsense/pull/5065) - Memory leak in hid sensor (DSO-13080, DSO-13712, DSO-13639). Fixes [#4332](https://github.com/IntelRealSense/librealsense/issues/4332)
* [#5025](https://github.com/IntelRealSense/librealsense/pull/5025) - Raspbian Buster build fix. Fix IMU streams handling. Addresses [#4986](https://github.com/IntelRealSense/librealsense/issues/4986), [#4979](https://github.com/IntelRealSense/librealsense/issues/4979), [#4950](https://github.com/IntelRealSense/librealsense/issues/4950), [#4818](https://github.com/IntelRealSense/librealsense/issues/4818).
* [#5028](https://github.com/IntelRealSense/librealsense/pull/5028) - [Realsense-Viewer] Configuration file default path with white spaces was not handled properly (DSO-13701). Fixes [#3779](https://github.com/IntelRealSense/librealsense/issues/3779)
* [#4987](https://github.com/IntelRealSense/librealsense/pull/4987) - Rename `foreach` to `foreach_rs` to avoid namespace collisions with QT's "foreach" macro. [#4461](https://github.com/IntelRealSense/librealsense/issues/4461). Proposed by @cgpadwick's
* [#4981](https://github.com/IntelRealSense/librealsense/pull/4981) - Fix min Z offset for disparity domain colorization mode by @TetsuriSonoda
* [#4967](https://github.com/IntelRealSense/librealsense/pull/4967) - [Depth Quality Tool/Viewer] Metrics record fixes and 
improvements. Fixes [#4913](https://github.com/IntelRealSense/librealsense/issues/4913), [#4948](https://github.com/IntelRealSense/librealsense/issues/4948)
* [#4945](https://github.com/IntelRealSense/librealsense/pull/4945) - [rs-ar-basic] Fix extrinsic pose to camera transformation
* [#4914](https://github.com/IntelRealSense/librealsense/pull/4914) - Fix White Balance control for Rolling shutter sensor.
* [#4910](https://github.com/IntelRealSense/librealsense/pull/4910) - Robustness improvement: `get_distance` to verify user-provided pixel indexes. [#4877](https://github.com/IntelRealSense/librealsense/issues/4877)

### Known Issues
* [#2809](https://github.com/IntelRealSense/librealsense/issues/2809) - Advanced C# examples bug
* [#2356](https://github.com/IntelRealSense/librealsense/issues/2356) - [Python] missing python example of alignment with post-processing. (DSO-10681)
* [#2860](https://github.com/IntelRealSense/librealsense/issues/2860) - Memory-leak in Pointcloud processing block.
* [#3433](https://github.com/IntelRealSense/librealsense/issues/3433) - Valgrind: Conditional jump or move depends on uninitialized variable.
* [#4297](https://github.com/IntelRealSense/librealsense/issues/4297) - [Windows] Multi-camera IMU Mix up. (DSO-13711)
* [#4261](https://github.com/IntelRealSense/librealsense/issues/4261) - [T265] Add ability to open multiple devices from different processes.
* [#4505](https://github.com/IntelRealSense/librealsense/issues/4505). - Global Timestamps wrong after long use. (DSO-13418)
* [#4518](https://github.com/IntelRealSense/librealsense/issues/4518) – [T265] Pose data produces `NaNs`. Can still occur in some cases. If detected, please attempt to make a raw data (images + IMU) recording using the [recorder tool](https://github.com/IntelRealSense/librealsense/tree/master/tools/recorder), and attach a link to it in the github issue, to assist our resolution.
* [T265][Mac] - Start after stop is not working on Mac with the T265 camera
* (DSO-9065)  - Frame Drops when changing depth controls while depth streaming.
* (DSO-12940) - IMU jitters and drops events
* (DSO-12942) - Global Timestamp: first 15 seconds of frames timestamps are unstable.
* (DSO-13524) - Viewer crash when running Update Unsigned FW with signed FW image (unlocked units only)
* (DSO-13525) - 3D viewer moved when sliding the tare calibration sliders
* (DSO-13539) - [Android] Camera disconnected after streaming some duration with Android Camera Sample
* (DSO-13541) - On-Chip Calibration stuck at 0% when in USB2 mode
* (DSO-13072) - Firmware Update on Linux - backup procedure may takes up to two minutes 
* (DSO-13078) - Firmware Update with `rs-fw-update` tool. The firmware update process may fail when additional librealsense application runs in background. Make sure to close any librealsense-based application during the Firmware Update routine

## Release 2.29.0
Release Date: 26 Sep 2019

### API Changes
[link](https://github.com/IntelRealSense/librealsense/wiki/API-Changes#version-2290)

### Bug Fixes
* [#4886](https://github.com/IntelRealSense/librealsense/pull/4886) - [Pcl] Fix typo in documentation by @fburakk. 
* [#4909](https://github.com/IntelRealSense/librealsense/pull/4909) - Fixed bug on record-playback. (RS5-3373)
* [#4925](https://github.com/IntelRealSense/librealsense/pull/4925) - [Realsense-Viewer] Fix Tare-Calibration UI. (DSO-13537) 
* [#4927](https://github.com/IntelRealSense/librealsense/pull/4927) - Update doxygen of pose_sensor.


### Known Issues
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
* (DSO-13539) - [Android] Camera disconnected after streaming some duration with Android Camera Sample
* (DSO-13525) - 3D viewer moved when sliding the tare calibration sliders
* (DSO-13524) - Viewer crash when running Update Unsigned FW with signed FW image (unlocked units only)
* (DSO-13418) - Global Timestamps wrong after long use [#4505](https://github.com/IntelRealSense/librealsense/issues/4505).

## Release 2.28.1
Release Date: 22 Sep 2019

### API Changes
No API changes - a maintenance release. 

### New Features & Improvements
* [#4808](https://github.com/IntelRealSense/librealsense/pull/4786) - [Realsense-Viewer] Set Decimation off by default for 
RGB streams (DSO-13570)
* [#4826](https://github.com/IntelRealSense/librealsense/pull/4826) - [rs-fw-logger] support extended XML scheme for dedicated SKUs.(RS5-5315)
* [#4836](https://github.com/IntelRealSense/librealsense/pull/4836) - [Android] Add sensor ROI support to the wrapper. (DSO-13473)
* [#4863](https://github.com/IntelRealSense/librealsense/pull/4863) - Change Depth Invalidation default to false.
* [#4773](https://github.com/IntelRealSense/librealsense/pull/4773) - Allow `frame_queue` to automatically keep frames
instead of requesting the user code to call `frame.keep()` explicitly for each required frame.


### Bug Fixes
* [#4808](https://github.com/IntelRealSense/librealsense/pull/4808) - [Python] Fix A-factor access in the wrapper. Addresses [#4807](https://github.com/IntelRealSense/librealsense/issues/4807)
* [#4809](https://github.com/IntelRealSense/librealsense/pull/4809) - Fixes for `save_single_frameset`. Related to [#4801](https://github.com/IntelRealSense/librealsense/issues/4801), [#4020](https://github.com/IntelRealSense/librealsense/issues/4020), [#3704](https://github.com/IntelRealSense/librealsense/issues/3704), [#3671](https://github.com/IntelRealSense/librealsense/issues/3671), [#2588](https://github.com/IntelRealSense/librealsense/issues/2588).
* [#4830](https://github.com/IntelRealSense/librealsense/pull/4830) - Wheel odometry unit-test fix.
* [#4851](https://github.com/IntelRealSense/librealsense/pull/4851) - [Python] Fix typo in `align-depth2color.py` example by  @BenDavisson.
* [#4866](https://github.com/IntelRealSense/librealsense/pull/4866) - Fix RGB distortion coefficients assignment (RS5-5354).
* [#4867](https://github.com/IntelRealSense/librealsense/pull/4867) - On-Chip Calibration adjustments


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
* (DSO-13418) - Global Timestamps wrong after long use [#4505](https://github.com/IntelRealSense/librealsense/issues/4505).

## Release 2.28.0
Release Date: 5 Sep 2019

### API Changes
N/A

### New Features & Improvements
* [#4786](https://github.com/IntelRealSense/librealsense/pull/4786) - [Realsense-Viewer] Set Decimation off by default for 
RGB streams (DSO-13570)
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
