# EdgeTPU Platforms

This directory holds precompiled shared libraries and patches for
using the USB EdgeTPU accelerator on additional platforms to the
main supported ones.

Currently we offer additional support for:

  *  Raspberry Pi Zero and Zero W

DISCLAIMER: Please note that this is not an officially supported Google product.
These additional precompiled libraries are provided *as is* at best
effort. We will do our best to keep these unofficial builds in sync with the
officially suppported ones.

# Installation instructions

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
