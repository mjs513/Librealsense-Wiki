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
|BUILD_PYTHON_BINDINGS|Build Python bindings for the SDK. Requires Python to be installed. See wrapper page for more information|`false`|
|BUILD_NODEJS_BINDINGS|Build Node.js bindings for the SDK. Requires Node.js to be installed. See wrapper page for more information|`false`|
|FORCE_LIBUVC|Setting this flag to true will configure the underlying backend to use `libuvc`. This backend is default for Mac OS, but can be configured on other OS-s as well. `libuvc` can serve as a more robust alternative to the native backend, however, it has well known limitations and is not recommended to be used in end-products|`false`|
|TRACE_API|When this flag is enabled, all API-calls will be written to the log at `INFO` severity. This will include any errors, duration, input and output parameters as well as the return value. Entry and exit from API calls will be documented as well at `DEBUG` severity. Enabling this feature will result in severe performance penalty|`false`|
|HWM_OVER_XU|When this option is enabled, hardware commands will be dispatched through extension-unit (XU) transfer protocol. When disabled (and assuming the hardware supports it) the SDK will talk to the hardware directly using `libusb` / `WinUSB`|`true`|
|BUILD_SHARED_LIBS| When enabled the output of the library will be a dynamic link library (DLL) or a shared object (SO). When disabled the output will be a static library (LIB/A)|`true`|
