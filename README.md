# EdgeTPU Platforms

This repository holds auxiliary platform-related material related to
[Google Coral Edge TPU](https://coral.withgoogle.com).
Here you can find precompiled images,
shared libraries and patches for using the USB Edge TPU accelerator on
additional platforms to the main supported ones.

DISCLAIMER: Please note that this is not an officially supported Google product.
These additional precompiled images and libraries are provided *as is* at best
effort. We will do our best to keep these unofficial builds in sync with the
officially supported ones.

## Prebuilt images for Raspberry Pis

For convenience we have uploaded prebuilt images for Raspberry Pi Zero,
Pi 3 and Pi 4. Simply write the image to an sd card and boot up your Pi.
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

The Coral USB Accelerator is not supported under MacOS, but you can use it from
a Linux VM under VirtualBox, if you forward the USB port through. This repo
contains a Vagrantfile that does the port forwarding for you.

```bash
# virtualbox will prompt you to enable it in security settings.
# Re-run the install if this causes it to error out the first time.
brew cask install virtualbox
brew cask install vagrant
brew cask install virtualbox-extension-pack
vagrant plugin install vagrant-vbguest
```

Once you have installed the requirements, you can start the machine.
This will take a while.
```bash
vagrant up
# Reboot it with the correct version of guest additions installed.
vagrant reload
```

Once everything is built, you can get a shell by typing:
```bash
vagrant ssh
```

Now that you're in, you should check that the coral device is visible:
```
$ lsusb
Bus 002 Device 003: ID 1a6e:089a Global Unichip Corp.
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

Follow the rest of the instructions on [the Coral Website](https://coral.withgoogle.com/tutorials/accelerator/) just like on any other platform.

If you get the error `RuntimeError: Error in device opening (/sys/bus/usb/devices/2-1)!`
then use `vagrant reload` to restart the VM and it should start working again.

Once you have run an example, the device's id will change:
```
$ lsusb
Bus 002 Device 002: ID 18d1:9302 Google Inc.
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```


## Unsupported platforms install wheels

We recommend using the above images but if you want to install edgetpu
libraries from scratch onto a Pi Zero image you can also download a modified
installation script for Raspberry Pi Zero and Zero W

Go to the [release page of this repo](https://github.com/google-coral/edgetpu-platforms/releases)
Download edgetpu_api_&lt;platform&gt;_&lt;version&gt;.tar.gz with platform
matching the desired device platform and copy the file to your device.
Untar it and run the install.sh script inside.

For example for Raspberry Pi Zero download edgetpu_api_rpi0_1.9.2.tar.gz
```
tar xzf edgetpu_api_rpi0_1.9.2.tar.gz
cd edgetpu_api
bash ./install.sh
```

Follow the rest of the instructions on [the Coral Website](https://coral.withgoogle.com/tutorials/accelerator/) just like on any other platform.
