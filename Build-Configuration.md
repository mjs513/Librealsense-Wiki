### Intro
Intel RealSense SDK is using **CMake** eco-system to offer useful customization to customers who wish to build the SDK from source.  
> For example, to generate makefile with `BUILD_EXAMPLES` flag turned-on, use the following command line:
`cmake .. -DBUILD_EXAMPLES=true`
Alternatively, use `cmake-gui` utility to configure and generate your build files.

## Build Customization Flags
| Flag  | Description | Default |
| ------------- | ------------- |----
| BUILD_EXAMPLES  | Build SDK examples and tools |`false`|
| BUILD_GRAPHICAL_EXAMPLES  | Controls the-subset of examples and tools dependent on `OpenGL`. Disabling this option will reduce the set of tools and examples to `rs-save-to-file`, `rs-terminal`, `rs-enumerate-devices` and `rs-fw-logger`. Recommended for headless systems without the graphic subsystem | `true`|
|BUILD_UNIT_TESTS| Build the full suite of unit-tests for the SDK|`true`|
|BUILD_WITH_OPENMP| When enabled, YUY to RGB conversion and Depth-Color spatial alignment will take advantage of multiple-cores using `OpenMP`. This can reduce latency at expense of greater CPU utilization|`true`|
| ENFORCE_METADATA | Having UVC per-frame metadata requires building with Windows SDK installed. When this flag is disabled, the resulting binary might not be capable of properly parsing UVC metadata if Windows SDK was not installed during the build. If this flag is true, not having Windows SDK install will break the build | `false`|
|BUILD_PYTHON_BINDINGS|Build Python bindings for the SDK. Requires Python to be installed. See [wrapper page](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/python) for more information|`false`|
|BUILD_PYTHON_MATLAB|Build Matlab wrapper for the SDK. See [wrapper page](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/matlab) for more information|`false`|
|BUILD_OPENNI2_BINDINGS|Build OpenNi2 wrapper for the SDK. See [wrapper page](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/openni2) for more information|`false`|
|BUILD_NODEJS_BINDINGS|Build Node.js bindings for the SDK. Requires Node.js to be installed. See [wrapper page](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/nodejs) for more information|`false`|
|BUILD_CSHARP_BINDINGS|Build .NET bindings for the SDK. See [wrapper page](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/csharp) for more information|`false`|
|DOTNET_VERSION_EXAMPLES|Select .NET framework version to be used for .NET examples|`4.0`|
|DOTNET_VERSION_LIBRARY|Select .NET framework version to be used for .NET wrapper|`3.5`|
|ENABLE_CCACHE|Enable building the SDK with CCache|`false`|
|BUILD_UNITY_BINDINGS|Build Unity sample scene using the SDK. See [wrapper page](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/unity) for more information|`false`|
|FORCE_LIBUVC|Setting this flag to true will configure the underlying backend to use `libuvc`. This backend is default for Mac OS, but can be configured on other OS-s as well. `libuvc` can serve as a more robust alternative to the native backend, however, it has well known limitations and is not recommended to be used in end-products|`false`|
|USE_SYSTEM_LIBUSB|When enabled, the SDK will assume libusb is installed on the system and use it. When disabled the SDK build process will fetch, build and install libusb from [github.com/libusb/libusb](https://github.com/libusb/libusb) before building librealsense|`true`|
|FORCE_WINUSB_UVC|Setting this will configure librealsense to use Windows backend based on WinUSB rewrite of the UVC protocol, instead of Media Foundation. Requires installation of a special driver provided inside the [Win7 SDK installer](https://github.com/IntelRealSense/librealsense/releases/download/v2.17.1/Intel.RealSense.SDK.win7.exe)|`false`|
|TRACE_API|When this flag is enabled, all API-calls will be written to the log at `INFO` severity. This will include any errors, duration, input and output parameters as well as the return value. Entry and exit from API calls will be documented as well at `DEBUG` severity. Enabling this feature will result in severe performance penalty|`false`|
|HWM_OVER_XU|When this option is enabled, hardware commands will be dispatched through extension-unit (XU) transfer protocol. When disabled (and assuming the hardware supports it) the SDK will talk to the hardware directly using `libusb` / `WinUSB`|`true`|
|BUILD_SHARED_LIBS| When enabled the output of the library will be a dynamic link library (DLL) or a shared object (SO). When disabled the output will be a static library (LIB/A)|`true`|
|**CMAKE_BUILD_TYPE**|Desired build time. To take advantage of compiler optimizations set to "Release" or "RelWithDebInfo"|`Debug`|
|ENABLE_ZERO_COPY| When enabled frames that do not require processing will not be mem-copied on arrival, rather the `rs2::frame` object will track native handle to the underlying OS resource (be it V4L2 video-buff or an `ISample`). This will reduce CPU utilization and save battery life, but can introduce unexpected latency or frame-drops, since the responsibility for buffer lifetime management falls on the application developer **(deprecated)**|`false`|
|BUILD_EASYLOGGINGPP|Perform cross-platform logging using EasyLogging++ 3rd-party library|`true`|
|BUILD_CV_EXAMPLES|Build computer vision examples requiring OpenCV. See [wrappers/opencv](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/opencv)|`false`|
|BUILD_CV_KINFU_EXAMPLES|Build simple 3d-reconstruction example using Kinnect-Fussion implementation. Relies on `OPENCV_ENABLE_NONFREE`. See [wrappers/opencv/kinfu](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/opencv/kinfu#rs-kinfu-sample)|`false`|
|BUILD_PCL_EXAMPLES|Search for PCL 3rd-party library and include example under `wrappers/pcl` in the project|`false`|
|BUILD_WITH_TM2|Assuming you received from Intel an engineering sample of T265(TM2) device, enable support for it in the SDK|`false`|
|BUILD_WITH_CUDA|Build the SDK using CUDA for color conversions and image alignment|`false`|
|BUILD_WITH_STATIC_CRT|When enabled increases binary footprint but prevents the dependency on Visual C++ Redistributables|`true`|
