## Version [2.22.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.22.0)

* Global Camera Timestamp:
 - Add `rs2_timestamp_domain::RS2_TIMESTAMP_DOMAIN_GLOBAL_TIME` [enumeration type](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_frame.h#L23) that will be used as default when the HW timestamp is available via the appropriate metadata attribute.
 - Add `rs2_sensor* rs2_get_frame_sensor` [function](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_frame.h#L108)
 - Add `RS2_OPTION_GLOBAL_TIME_ENABLED` [option](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L77)
* Depth units transformation - Processing block
 - `rs2_processing_block* rs2_create_units_transform` [function](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L69)
 - Add `rs2_format::RS2_FORMAT_DISTANCE` synthetic stream [format](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L78)
 - Add `units_transform` [class](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/hpp/rs_processing.hpp#L524)

 - Add `rs2_error * rs2_create_error` [functionality](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_types.h#L240)
 - Add `pose_stream_profile` [class](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/hpp/rs_frame.hpp#L284) to handle T265 pose sensor.
 - Add `frame::get_sensor()` [functionality](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/hpp/rs_frame.hpp#L420)
 - Add ` sensor_from_frame(frame f)`  [functionality](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/hpp/rs_sensor.hpp#L332)


* GLSL Processing Blocks Module:
 - New header files with new API for GLSL-supported modules are added to [include/librealsense2-gl](https://github.com/IntelRealSense/librealsense/tree/development/include/librealsense2-gl) directory


## Version [2.20.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.20.0) to [2.21.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.21.0)

New IR format introduced to D415 - `W10`:
- Rectified, 10 bit per-pixels (packed) IR stream
- FullHD configuration only 30 fps
- Can be configured for use in conjunction with Depth stream (which is limited to 720p)
- Available as:
   - parsed 10 bit per pixel [RS2_FORMAT_Y10BPACK](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L77)
   - Raw packed data (4pixel/5bytes) according to [V4L2-PIX-FMT-Y10BPACK](https://www.linuxtv.org/downloads/v4l-dvb-apis-old/V4L2-PIX-FMT-Y10BPACK.html) specification



## Version [2.19.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.19.0) to [2.20.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.20.0)

New Lens distortion model support added for T265 optical sensors -  
[RS2_DISTORTION_KANNALA_BRANDT4](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_types.h#L51).  
The model is utilized in [Project/Deproject](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/rsutil.h#L84) routines

[rs2_send_wheel_odometry](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L525) - Wheel odometer API velocity type updated from angular to **linear**.


## From version [2.19.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.19.0) to [2.19.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.19.1)

No API changes

## From version [2.18.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.18.0) to [2.19.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.19.0)

### Added
#### Processing blocks/filters:
1. [`rs2_get_recommended_processing_blocks`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L446) Retrieving an ordered list of processing blocks/filters that are recommended to be used for a specific sensor. For instance, for the Depth sensor the list may include (Decimation->Disparity->Spatial->Temporal->HoleFilling->Disparity``) sequence.
2. [`rs2_get_recommended_processing_blocks_count`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L463) Retrieving the number of elements on the processing blocks list
3. [`rs2_get_processing_block` ](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L455) Extracting a specific processing block from the list
4. [`rs2_delete_recommended_processing_blocks`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L469) Deleting the processing blocks list. The function shall be used in conjunction with `rs2_get_recommended_processing_blocks` mentioned above to explicitly release the allocated resources.
5. [`rs2_supports_processing_block_info`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L254) Test for attribute availbility without throwing exception
6. [`rs2_get_processing_block_info`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L245) Retrieve processing block attribute
7. [`rs2_is_processing_block_extendable_to`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L263) Check API extension support
8. [`rs2_create_zero_order_invalidation_block`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L236) Adding zero order invalidation processing block


#### Options API:  
9. [`rs2_get_options_list`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L146) Dynamic discovery of the options supported by a librealsense entity (sensor/processing_block/etc`).
10. [`rs2_get_options_list_size`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L153) Retrieve the number of elements in the options list.
11. [`rs2_get_option_name`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L162) Return human-readable option's name attribute.
12. [`rs2_get_option_from_list`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L169) Return an indexed element from the lsit
13. [`rs2_delete_options_list`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L175) Deleting the processing blocks list. The function shall be used in conjunction with `rs2_get_options_list` to explicitly release previously allocated resources.
14. Extending RS2_OPTIONS enumeration list with:  
[`RS2_OPTION_ZERO_ORDER_POINT_X`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L71),
 [`RS2_OPTION_ZERO_ORDER_POINT_Y`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L72),
 [`RS2_OPTION_LLD_TEMPERATURE`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L73),
 [`RS2_OPTION_MC_TEMPERATURE`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L74), 
[`RS2_OPTION_MA_TEMPERATURE`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L75)  
  
#### Device management
15. [`rs2_get_stereo_baseline`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L169) Retrieve Stereo-based Depth sensor baseline
17. [`rs2_context_add_software_device`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_context.h#L64) Inject a software (mockup) device into the SDK's context to be discoverable via `query_devices` API call.

#### T265-specific APIs
18. [`rs2_context_unload_tracking_module`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L169) Unload all perviously acquired tracking device instances. A device query for T265 will automatically take ownership of the connected device.
This new API allows to explicitly release the devices so that they will be available for use by external processes.
19. [`rs2_export_localization_map`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L489) Advanced feature that allows to export the localization map for later reuse.
20. [`rs2_import_localization_map`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L479) Import previously-obtained localization map into device.
21. [`rs2_set_static_node`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L500) Add a positional bookmark (name&location) for positional referencing.
22. [`rs2_get_static_node`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L511) Retrieve previously stored bookmark position.
23. [`rs2_load_wheel_odometry_config`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L517) Load the robot platform configuration and calibration data into device. The data includes the rigid body transformation as well as calibration parameters.
24. [`rs2_send_wheel_odometry`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L525) Feed odometer data generated by a third-party sensor into the tracking device.

### To be deprecated
1. `rs2_option_to_string` - For existing options it will return option name, but for future API additions the user should call rs2_get_option_name instead


## From version [2.17.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.17.0) to [2.18.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.18.0)

### Added
1. [`rs2_create_yuy_decoder`](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L54) Adding YUY2 to RGB processing block [#3056](https://github.com/IntelRealSense/librealsense/pull/3056) :
2. [`rs2_create_error`](https://github.com/IntelRealSense/librealsense/blame/d39b5139ce62efffddee4cd11a87e8927ecdfa0c/src/api.h#L35) Exposing librealsense error to avoid cross-boundary new/delete operations:
3. [`rs2_create_threshold`](https://github.com/IntelRealSense/librealsense/blob/d39b5139ce62efffddee4cd11a87e8927ecdfa0c/include/librealsense2/h/rs_processing.h#L62) Adding depth min/max clamp filter (processing block):
4. [`RS2_OPTION_EMITTER_ON_OFF`](https://github.com/IntelRealSense/librealsense/pull/2829) - adding `RS2_OPTION_EMITTER_ON_OFF` to options enumeration
5. [`rs2_processing_block_register_simple_option`](https://github.com/IntelRealSense/librealsense/pull/2830/files#diff-c47ed929a30eaaa0bfce02ecdcfa2701R64) - adding ability to register custom processing block options
6. Adding [`save_to_ply`](https://github.com/IntelRealSense/librealsense/pull/2830/files#diff-883f598ceaa739d7473cdc28d7995e23R17) and [`save_single_frameset`](https://github.com/IntelRealSense/librealsense/pull/2830/files#diff-883f598ceaa739d7473cdc28d7995e23R161) processing blocks to C++ headers only (staging to be added to the API) under [rs_export.hpp](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/hpp/rs_export.hpp).

### Removed

1. [set_devices_changed_callback](https://github.com/IntelRealSense/librealsense/pull/2823) - was removed from C++ header files

## From version [2.16.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.16.0) to [2.17.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.17.0)

### Added

* [#2773](https://github.com/IntelRealSense/librealsense/pull/2773) introduced asynchronous pipeline API (recommended for high frequency data such as IMU). This change is limited to adding new overloads to `pipeline.start` method:
1. [rs2_pipeline_start_with_callback](https://github.com/matkatz/librealsense/blob/a2406a5c7713bb9de5cd0b28e8558e85a63a19b1/include/librealsense2/h/rs_pipeline.h#L147) - pipeline start with C function pointer and user data, similar to `sensor.start`
2. [rs2_pipeline_start_with_callback_cpp](https://github.com/matkatz/librealsense/blob/a2406a5c7713bb9de5cd0b28e8558e85a63a19b1/include/librealsense2/h/rs_pipeline.h#L160) - pipeline start with C++ frame callback object, similar to `sensor.start`
3. [rs2_pipeline_start_with_config_and_callback](https://github.com/matkatz/librealsense/blob/a2406a5c7713bb9de5cd0b28e8558e85a63a19b1/include/librealsense2/h/rs_pipeline.h#L180) - pipeline start with callback and config
4. [rs2_pipeline_start_with_config_and_callback_cpp](https://github.com/matkatz/librealsense/blob/a2406a5c7713bb9de5cd0b28e8558e85a63a19b1/include/librealsense2/h/rs_pipeline.h#L199) - pipeline start with callback and config (C++ frame callback object)

* [#2687](https://github.com/IntelRealSense/librealsense/pull/2687) introduces new API to control recording compression: 

1. [rs2_create_record_device_ex](https://github.com/belkinirena/librealsense/blob/9d8d3a690ebd5fd4b60c3d3c73a6e11e901f14bc/include/librealsense2/h/rs_record_playback.h#L49) - create recorder and explicitly enable or disable compression. By default, compression will be enabled based on device type. D435i and T265 devices that provide high FPS streams disable compression by default to avoid frame drops during recording. 

* [#2673](https://github.com/IntelRealSense/librealsense/pull/2673) adds API to generate IMU and pose data with `software_device`:

Added support for IMU stream and recording IMU frames in software sensor:

- stream_profile **add_motion_stream**(rs2_motion_stream motion_stream)
- rs2_stream_profile* **rs2_software_sensor_add_motion_stream**(rs2_sensor* sensor, rs2_motion_stream motion_stream, rs2_error** error);
- void **on_motion_frame**(rs2_software_motion_frame frame)
- void **rs2_software_sensor_on_motion_frame**(rs2_sensor* sensor, rs2_software_motion_frame frame, rs2_error** error);

Added support for pose stream and recording pose frames in software sensor:

- stream_profile **add_pose_stream**(rs2_pose_stream pose_stream)
- rs2_stream_profile* **rs2_software_sensor_add_pose_stream**(rs2_sensor* sensor, rs2_pose_stream pose_stream, rs2_error** error);
- void **on_pose_frame**(rs2_software_pose_frame frame)
- void **rs2_software_sensor_on_pose_frame**(rs2_sensor* sensor, rs2_software_pose_frame frame, rs2_error** error);

### Renamed

* [#2757](https://github.com/IntelRealSense/librealsense/pull/2757) is splitting C++ `processing_block` class into `processing_block` and `filter` classes, with `filter` being derived from `processing_block`.
`processing_block` abstraction offers `start` and `invoke` operations and does not guaranty results will be immediately available (`processing_block` can chose to **delay** frames). `filter` is special type of processing block that performs its operation immediately. This lets users compose filters using `apply_filter` operation. 

## From version [2.15.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.15.0) to [2.16.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.16.0)

### Added
* [rs2_project_color_pixel_to_depth_pixel](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/rsutil.h#L117) - map pixel in the color image to pixel in depth image

* [rs2_allocate_points](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_frame.h#L288) - allows the user to write custom processing block that outputs frame of type points

* [frame::apply_filter](https://github.com/IntelRealSense/librealsense/blob/v2.16.0/include/librealsense2/hpp/rs_frame.hpp#L509) - this method allows unified application of processing blocks, regardless of processing or frame type. This allows easy composition of processing blocks. 

### Removed

* [`processing_block::operator()(frame f) const`](https://github.com/IntelRealSense/librealsense/blob/v2.15.0/include/librealsense2/hpp/rs_processing.hpp#L151) was removed to reduce the overall ways processing block can be invoked. All processing blocks still contain `invoke` method for async processing (that sends the results to callback), and can be applied using added `apply_filter` method, in addition to helper methods like `colorize` and `calculate` specific to each block.

## From version [2.14.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.14.0) to [2.15.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.15.0)

### Added
* [rs2_query_devices_ex](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_context.h#L87) - provide a list of connected devices with user-specified mask. This allows to cherry-pick specific types (e.g D400/SR300) during device acquisition stage. 


## Version [2.14.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.14.0) vs [2.13.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.13.1)

### Added

* [rs2_try_wait_for_frame](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/h/rs_processing.h#L143), [rs2_pipeline_try_wait_for_frames](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/h/rs_pipeline.h#L91) - wait_for_frames overload that does not throw an exception on timeout

* [was_added](https://github.com/BrendanDrew/librealsense/blob/12b42d3eb8d6cd44167134737d96d1b06ea0e8eb/include/librealsense2/hpp/rs_context.hpp#L40) and [get_new_devices](https://github.com/BrendanDrew/librealsense/blob/12b42d3eb8d6cd44167134737d96d1b06ea0e8eb/include/librealsense2/hpp/rs_context.hpp#L57) methods added to [event_information](https://github.com/BrendanDrew/librealsense/blob/12b42d3eb8d6cd44167134737d96d1b06ea0e8eb/include/librealsense2/hpp/rs_context.hpp#L13) C++ class 

## Version [2.13.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.13.0) (vs [2.11.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.11.1))

### Added 

* [rs2_option::RS2_OPTION_INTER_CAM_SYNC_MODE](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_option.h#L66) - Master/Slave control for multi-cam setup synchronization.

* [rs2_frame_metadata_value](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_frame.h#L42-L59) - Extending available attributes:
    - Depth Sensor:
       - Laser Power, Laser Power Mode, Exposure Priority, Exposure ROI.
    - RGB Sensor:
       - Brightness, Contrast, Saturation, Sharpness, Backlight_Compensation, Hue, Gamma, White_Balance_Mode & Temperature, Powerline Frequency and Low Light Compensation.



## From [2.11.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.11.0) to [2.11.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.11.1)

### Modified

* [rs2_camera_info::RS2_CAMERA_INFO_RECOMMENDED_FIRMWARE_VERSION](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_sensor.h#L26) - Field was moved next to RS2_CAMERA_INFO_FIRMWARE_VERSION.


## From [2.10.4](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.4) to [2.11.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.11.0)

### Added 

* [rs2_create_processing_block_fptr](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L61) - Allows to create custom processing blocks using C-bindings (C, LabView, .NET)
* [rs2_start_processing_fptr](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L78) - Allows to start a processing block with a callback
* [rs2_config_enable_device_from_file_repeat_option](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_pipeline.h#L259) - Allows to configure pipeline to play from recording while controlling playback-repeat behavior 
* [rs2_create_hole_filling_filter_block](https://github.com/IntelRealSense/librealsense/blob/development/include/librealsense2/h/rs_processing.h#L177) - Hole-Filling filter supports three modes of operation:
  - Fill from left - fill the hole by the value from an immediate left neighbor
  - Fill from Far - select one of the up/down/left/right pixel neighbors farthest away from the camera
  - Fill from Near - select one of the up/down/left/right neighbors closest to the camera.  
  It is recommended to use this post-processing block last in the filters chain.
The functionality is integrated and can be reviewed in realsense-viewer/post-processing section


## From [2.10.3](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.3) to [2.10.4](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.4)

No API changes

## From [2.10.2](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.2) to [2.10.3](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.3)


### Modified
Adding `RS2_CAMERA_INFO_USB_TYPE_DESCRIPTOR` enumeration to detect USB2 vs USB3 mode (when supported by the firmware). 

## From [2.10.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.1) to [2.10.2](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.2)


### Modified
Adding `RS2_OPTION_AUTO_EXPOSURE_CONVERGE_STEP` enumeration to control the FishEye Auto-Exposure algorithm
The option is available for TM1-enabled devices only.


## From [2.10.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.0) to [2.10.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.1)

No API changes

## From [2.9.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.9.1) to [2.10.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.0)

### Added

* [rs2::frameset::get_infrared_frame()](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/hpp/rs_frame.hpp#L691) - Simpler way for users to get infrared frames from a `rs2::frameset`

### Changed

* Fixed [`rs2_set_devices_changed_callback`](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/h/rs_context.h#L42) - missing `const` specifier and `void** user` parameter were added.
* Change the 'Holes Filling' control for Temporal Post-Processing filter to be activated with `RS2_OPTION_HOLES_FILL` instead of `RS2_OPTION_FILTER_MAGNITUDE`

## From [2.9.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.9.0) to [2.9.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.9.1)

### Added 

* [rs2_keep_frame](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/hpp/rs_frame.hpp#L269) - this function can be used to preserve specific frame for longer processing. Calling it signals the intention to not return this frame to the pool within next 100ms. 

## From [2.8.3](https://github.com/IntelRealSense/librealsense/releases/tag/v2.8.3) to [2.9.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.9.0)

### Added
* [rs2_create_disparity_transform_block](https://github.com/IntelRealSense/librealsense/blob/v2.9.0/include/librealsense2/h/rs_processing.h#L152) A depth data conversion class that transforms depth data info/from disparity domain for stereo-based depth sensors (D400 series). This functionality allows to run post-processing filters in disparity domain to enhance the filtered outcome.

* [rs2_depth_stereo_frame_get_baseline](https://github.com/IntelRealSense/librealsense/blob/v2.9.0/include/librealsense2/h/rs_sensor.h#L158) Retrieve the stereoscopic baseline in mm for stereo-based depth camera.

* [rs2_export_to_ply](https://github.com/IntelRealSense/librealsense/blob/v2.9.0/include/librealsense2/h/rs_frame.h#L171)
Making the export functionality publicly available, also addressing [#862](https://github.com/IntelRealSense/librealsense/issues/862)



## From [2.8.2](https://github.com/IntelRealSense/librealsense/releases/tag/v2.8.2) to [2.8.3](https://github.com/IntelRealSense/librealsense/releases/tag/v2.8.3)

### Added
* [rs2_log](https://github.com/IntelRealSense/librealsense/blob/v2.8.3/include/librealsense2/rs.h#L80) - Usability function that allows the user to add logs to librealsense internal logger. The feature is useful in debugging and profiling scenarios.

Post-processing depth filters:
* [rs2_create_decimation_filter_block](https://github.com/IntelRealSense/librealsense/blob/v2.8.3/include/librealsense2/h/rs_processing.h#L133) - Down-sampling filter that effectively reduces the depth map resolution.
* [rs2_create_spatial_filter_block](https://github.com/IntelRealSense/librealsense/blob/v2.8.3/include/librealsense2/h/rs_processing.h#L145) - Spatial edge-preserving depth filter.
* [rs2_create_temporal_filter_block](https://github.com/IntelRealSense/librealsense/blob/v2.8.3/include/librealsense2/h/rs_processing.h#L139) - Temporal filter that rectifies depth values based on previously-available frames.

The filters have been integrated into the **realsense-viewer**  and **depth-quality** tools.
    

## From [2.8.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.8.1) to [2.8.2](https://github.com/IntelRealSense/librealsense/releases/tag/v2.8.2)

No API changes introduced


## From [2.8.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.8.0) to [2.8.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.8.1)

### Added
* [rs2_start_processing_queue](https://github.com/IntelRealSense/librealsense/tree/v2.8.1/include/librealsense2/h/rs_processing.h#L67) - convenience function that lets the user target the output of a processing block (for example **align**) directly into a **frame_queue**. This helps in languages where function pointers are not available, such as LabView 

> Signature of **rs2_is_option_read_only**, **rs2_get_option**, **rs2_set_option**, **rs2_supports_option**, **rs2_get_option_description** and **rs2_get_option_value_description** was changed. First parameter used to be pointer to **rs2_sensor** and now is pointer to **rs2_options**. However, it is 100% safe to cast pointer to **rs2_sensor** to pointer to **rs2_options**. 

## From [2.7.9](https://github.com/IntelRealSense/librealsense/releases/tag/v2.7.9) to [2.8.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.8.0)

### Moved
> See [Pipeline Changes](https://github.com/IntelRealSense/librealsense/pull/672) pull-request for explanation
* [rs2_stop_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L64)
is now available as [rs2_pipeline_stop](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L40)
* [rs2_start_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L40)
is now available as [rs2_pipeline_start](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L94)
* [rs2_pipeline_get_device](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L33)
is now available as [rs2_pipeline_profile_get_device](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L142)
* [rs2_pipeline_get_active_streams](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L112)
is now available as [rs2_pipeline_profile_get_streams](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L151)
* [rs2_enable_pipeline_stream](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L75)
is now available as [rs2_config_enable_stream](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L201)
* [rs2_enable_pipeline_device](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L77)
is now available as [rs2_config_enable_device](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L231)
* [rs2_disable_stream_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L82)
is now available as [rs2_config_disable_stream](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L265)
* [rs2_disable_all_streams_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L87)
is now available as [rs2_config_disable_all_streams](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L287)

### Added
* [rs2_pipeline_start_with_config](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L115)
* [rs2_pipeline_get_active_profile](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L127)
* [rs2_delete_pipeline_profile](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L158)
* [rs2_create_config](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L171)
* [rs2_delete_config](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L178)
* [rs2_config_enable_all_stream](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L219)
* [rs2_config_enable_device_from_file](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L243)
* [rs2_config_enable_record_to_file](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L253)
* [rs2_config_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L307)
* [rs2_config_can_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L318)
* [rs2_config_disable_indexed_stream](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L277)

### Removed
* [rs2_get_stream_profile_size](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_sensor.h#L357) - This function was intended to offer an estimate of USB bandwidth, however USB3 performance is affect by factors other then bytes/second, rendering this method useless
* [rs2_open_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L42) - This function was offered to force pipeline configuration prior to streaming. This can be more effectively achieved by [rs2_config_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L307) and [rs2_config_can_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L318) 
* [rs2_start_pipeline_with_callback](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L49) -
 and [rs2_start_pipeline_with_callback_cpp](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L57) - Pipeline is always performing synchronization at the moment. If you wish to get minimum latency you can use callback API of the individual sensors
* [rs2_pipeline_get_selection_count](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L120), [rs2_pipeline_get_stream_selection](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L129),  [rs2_pipeline_get_stream_type_selection](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L139),  [rs2_pipeline_delete_selection](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L145) - These methods were redundant


***


## From [2.7.7](https://github.com/IntelRealSense/librealsense/releases/tag/v2.7.7) to [2.7.9](https://github.com/IntelRealSense/librealsense/releases/tag/v2.7.9)

### Moved
* [rs2_get_context_time](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_context.h#L38)
is now available as [rs2_get_time](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/rs.h#L82)
* [rs2_create_pipeline_with_device](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_pipeline.h#L32)
is now available as [rs2_enable_pipeline_device](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L77)
* [rs2_enable_stream_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_pipeline.h#L82)
is now available as [rs2_enable_pipeline_stream](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L75)
* [rs2_pipeline_get_selection](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_pipeline.h#L141)
is now available as [rs2_pipeline_get_active_streams](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L112)

### Added
* [rs2_playback_device_stop](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_record_playback.h#L168)
* [rs2_start_queue](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_sensor.h#L223)
* [rs2_open_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L42)

### Removed
* [rs2_can_enable_stream_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_pipeline.h#L95) - This method, while useful, was not 100% clearly defined. The same goal was more cleanly achieved in a later release - [rs2_config_can_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L318)
* [rs2_pipeline_get_extrinsics](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_pipeline.h#L133) - Extrinsics can be queried between stream profiles, and don't require the pipeline or context.
* [rs2_pipeline_get_context](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_pipeline.h#L176) - Context can be passed to pipeline constructor for dependency injection, but should not be required for anything useful later on.

### Signature Changed
* [rs2_create_pointcloud](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_processing.h#L41) used to accept 2 parameters but
[rs2_create_pointcloud](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_processing.h#L41) accepts 1 parameters!
* [rs2_create_processing_block](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_processing.h#L51) used to accept 3 parameters but
[rs2_create_processing_block](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_processing.h#L51) accepts 2 parameters!
* [rs2_create_align](https://github.com/IntelRealSense/librealsense/tree/v2.7.7/include/librealsense2/h/rs_processing.h#L118) used to accept 3 parameters but
[rs2_create_align](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_processing.h#L118) accepts 2 parameters!
