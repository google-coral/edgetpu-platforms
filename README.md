# Edge TPU unofficial platforms

This repository holds auxiliary platform-related material related to
[Google Coral Edge TPU](https://coral.ai).
Here you can find precompiled images,
shared libraries and patches for using the USB Accelerator on
additional platforms to the main supported ones.

DISCLAIMER: Please note that this repository is not officially supported by Google.
These additional precompiled images and libraries are provided *as is* at best
effort. We will try to keep these unofficial builds in sync with the
officially supported ones, but they will likely be out of date.

## Prebuilt images for Raspberry Pis

For convenience, we have uploaded prebuilt Raspbian images for Raspberry Pi Zero,
Pi 3 and Pi 4. Simply write the image to an SD card, boot up your Pi, and connect the USB Accelerator.
The images contain several examples that should work out of the box.

The download links are:

  * [Raspberry Pi Zero, Stretch Lite, Edgetpu 1.9.2](https://github.com/google-coral/edgetpu-platforms/releases/download/v1.9.2/rpi0-raspbian-stretch-edgetpu-1.9.2.img.gz)
  * [Raspberry Pi 3, Stretch Lite, Edgetpu 2.11.1](https://github.com/google-coral/edgetpu-platforms/releases/download/v2.11.1/rpi3-raspbian-stretch-lite-edgetpu-2.11.1.img.gz)
  * [Raspberry Pi 4, Buster, Edgetpu 2.11.1](https://github.com/google-coral/edgetpu-platforms/releases/download/v2.11.1/rpi4-raspbian-buster-edgetpu-2.11.1.img.gz)

After you boot be sure to do the following two steps:

  * The Pi image is DHCP and SSH enabled by default. Log in with user "pi" and
    password "raspberry". IMPORTANT: Once you're in you should
    immediately change your password away from the default one, otherwise
    you have a security risk.
    ```
    passwd
    ```
  * The filesystem needs to be expanded to the full size of the SD card,
    which is likely larger than the image. To do so:
    ```
    sudo raspi-config
    ```
    And then choose “Expand root partition to fill SD card” option
    under Advanced Options, save and reboot.


## MacOS using Vagrant

The `Vagrantfile` in this repo was originally created to support macOS from a Linux VM under VirtualBox.
This is no longer necessary because the Coral USB Accelerator now officially supports macOS (and Windows 10), [since January 2020](https://coral.ai/news/updates-01-2020).

To use the USB Accelerator on macOS, simply follow the [USB Accelerator get started guide](https://coral.ai/docs/accelerator/get-started).


## Unsupported platforms install wheels

We recommend using the above images but if you want to install edgetpu
libraries from scratch onto a Pi Zero image you can also download a modified
installation script for Raspberry Pi Zero and Zero W.

1. Go to the [release page of this repo](https://github.com/google-coral/edgetpu-platforms/releases).
2. Download edgetpu_api_&lt;platform&gt;_&lt;version&gt;.tar.gz with platform
matching the desired device platform and copy the file to your device.
3. Untar it and run the install.sh script inside.

For example for Raspberry Pi Zero download edgetpu_api_rpi0_1.9.2.tar.gz
```
tar xzf edgetpu_api_rpi0_1.9.2.tar.gz
cd edgetpu_api
bash ./install.sh
```

Follow the rest of the instructions on [the Coral website](https://coral.ai/docs/accelerator/get-started) just like on any other platform.
