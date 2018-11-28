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
