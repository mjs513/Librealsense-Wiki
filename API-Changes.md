## From [2.10.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.0) to [2.10.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.1)

N/A


## From [2.9.1](https://github.com/IntelRealSense/librealsense/releases/tag/v2.9.1) to [2.10.0](https://github.com/IntelRealSense/librealsense/releases/tag/v2.10.0)

### Added

* [rs2::frameset::get_infrared_frame()](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/hpp/rs_frame.hpp#L691) - Simpler way for users to get infrared frames from a `rs2::frameset`

### Changed

* Fixed [`rs2_set_devices_changed_callback`](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/h/rs_context.h#L42) - missing `const` specifier and `void** user` parameter were added.

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
