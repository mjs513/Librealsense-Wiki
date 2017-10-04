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
is now available as [rs2_config_disable_all_streams](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L275)

### Added
* [rs2_pipeline_start_with_config](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L115)
* [rs2_pipeline_get_active_profile](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L127)
* [rs2_delete_pipeline_profile](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L158)
* [rs2_create_config](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L171)
* [rs2_delete_config](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L178)
* [rs2_config_enable_all_stream](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L219)
* [rs2_config_enable_device_from_file](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L243)
* [rs2_config_enable_record_to_file](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L253)
* [rs2_config_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L295)
* [rs2_config_can_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L306)

### Removed
* [rs2_get_stream_profile_size](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_sensor.h#L357) - This function was intended to offer an estimate of USB bandwidth, however USB3 performance is affect by factors other then bytes/second, rendering this method useless
* [rs2_open_pipeline](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L42) - This function was offered to force pipeline configuration prior to streaming. This can be more effectively achieved by [rs2_config_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L295) and [rs2_config_can_resolve](https://github.com/IntelRealSense/librealsense/tree/v2.8.0/include/librealsense2/h/rs_pipeline.h#L306) 
* [rs2_start_pipeline_with_callback](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L49) -
 and [rs2_start_pipeline_with_callback_cpp](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L57) - Pipeline is always performing synchronization at the moment. If you wish to get minimum latency you can use callback API of the individual sensors 
* [rs2_pipeline_get_selection_count](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L120), [rs2_pipeline_get_stream_selection](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L129),  [rs2_pipeline_get_stream_type_selection](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L139),  [rs2_pipeline_delete_selection](https://github.com/IntelRealSense/librealsense/tree/v2.7.9/include/librealsense2/h/rs_pipeline.h#L145) - These methods were redundant