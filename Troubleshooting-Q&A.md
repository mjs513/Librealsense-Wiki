> [Wiki](Home) ▸ **Troubleshooting Q&A**

We've grouped together related questions for your convenience 

**[Git](#git)**
- [Git returns `access timeout` when I try to clone the repository](#q-git-returns-access-timeout-when-i-try-to-clone-the-repository)

**[Camera not working\detected](#camera-not-working-detected)**
- [How do I see which Intel RealSense cameras are connects?](#q-how-do-i-see-which-intel-realsense-cameras-are-connects)
- [I connected the camera to the USB port but it is not recognized](#q-i-connected-the-camera-to-the-usb-port-but-it-is-not-recognized)
- [I'm using a virtual machine and the camera is not working](#q-im-using-a-virtual-machine-and-the-camera-is-not-working)
- [Streaming gets stuck on windows](#q-streaming-gets-stuck-on-windows)

**[Installation](#installation)**
- [How do I enable librealsense logs?](#q-how-do-i-enable-librealsense-logs)
- [GCC Internal Error](#q-gcc-internal-error)
- [I ran the udev rules script but Linux still get `Permission denied`](#q-i-ran-the-udev-rules-script-but-linux-still-get-permission-denied)
- [`dmesg` shows: `uvcvideo: module verification failed: signature and/or required key missing - tainting kernel`](#q-dmesg-shows-uvcvideo-module-verification-failed-signature-andor-required-key-missing---tainting-kernel)
- [`sudo modprobe uvcvideo` produces `dmesg: uvc kernel module is not loaded`](#q)

**[Python](#python)**
  - [CMake shows an error when I try to build with Python bindings](#q-cmake-shows-an-error-when-i-try-to-build-with-python-bindings)


-----------------


Git
====================
## Q: Git returns `access timeout` when I try to clone the repository

    git.launchpad... access timeout

This usually happens when your computer is behind a firewall, try to configure git to use the appropriate proxy server



-----------------

Camera not working\detected
====================

## Q: How do I see which Intel RealSense cameras are connects?
#### **Linux:**
Open shell:
```bash
$ lsusb | grep 8086
```

#### **Windows:**
1. Click the `Win-Key`+`X` keys
2. Choose `Device Manager`
3. Look under `Imaging devices` for "Intel RealSense" cameras



## Q: I connected the camera to the USB port but it is not recognized

> ❗️ Make sure your camera is connected using USB 3.0 ❗️ 

If your camera is connected via USB 3.0, check to make sure your OS detects the camera ([how?](#q-how-do-i-see-which-intel-realsense-cameras-are-connects)).


## Q: I'm using a virtual machine and the camera is not working

Due to the USB 3.0 translation layer between native hardware and virtual machine, the librealsense team does not support installation in a VM. If you do choose to try it, we recommend using VMware Workstation Player, and not Oracle VirtualBox for proper emulation of the USB3 controller.

## Q: Streaming gets stuck on windows

When working on Windows 8.1, make sure you have [KB3075872](https://support.microsoft.com/en-us/kb/3075872) and [KB2919355](https://support.microsoft.com/en-us/kb/2919355) installed. These patches are addressing issues with 8.1 video drivers, resolved in Windows 10.


-----------------

Installation
====================

## Q: How do I enable librealsense logs?
To change the log level of LibRealSense logger, you need to set a local variable named **LRS_LOG_LEVEL**
and initialize it with the desirable log level:

#### **Linux:**
```bash
$ export LRS_LOG_LEVEL="<Log Level>"
```

#### **Windows:**
```bash
$ set LRS_LOG_LEVEL="<Log Level>"
```
- A LibRealSense log will be created even when an application does not activate the LibRealSense logger.


## Q: GCC Internal Error

The gcc compiler issues the following error while compiling:

> gcc: internal compiler error

This might indicate that you do not have enough memory or swap space on your machine. Try closing memory consuming applications, and if you are running inside a VM increase available RAM to at least 2 GB.

## Q: I ran the udev rules script but Linux still get `Permission denied`

First, try re-installing udev rules located in librealsense source directory:
    sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/
    sudo udevadm control --reload-rules && udevadm trigger

If the issue persists, the cause might be due to the fact that your user is not part of the `plugdev` group.


## Q: `dmesg` shows: `uvcvideo: module verification failed: signature and/or required key missing - tainting kernel`

This is a standard warning issued since Kernel 4.4-30+, it is only a notification and does not affect module's functionality.

## Q: `sudo modprobe uvcvideo` produces `dmesg: uvc kernel module is not loaded`

This issue is caused since the patched module kernel version is incompatible with the resident kernel.
Verify the actual kernel version with `uname -r`.
Revert and proceed from [Make Ubuntu Up-to-date](../doc/installation.md#make-ubuntu-up-to-date) step from the Linux installation guide.

-----------------

Python
====================

## Q: CMake shows an error when I try to build with Python bindings
The following message appears:

>  Could NOT find PythonInterp (missing: PYTHON_EXECUTABLE)

Please check the following:
- Make sure Python is installed
- **On Windows**: If you've just installed python, reboot (or log off) and try again
  - Try the answers suggested here: [building-opencv-libraries-from-source-files](https://stackoverflow.com/questions/9119253/building-opencv-libraries-from-source-files)


>   Python config failure: Python is 32-bit, chosen compiler is 64-bit

If this message appears you should install python 64 bit
