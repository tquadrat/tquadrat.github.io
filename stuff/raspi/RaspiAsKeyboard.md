# Raspberry Pi as USB Device

## Raspberry&nbsp;Pi&nbsp;Zero as USB Keyboard

You can find different descriptions on how to configure a Raspberry&nbsp;Pi&nbsp;Zero as a virtual keyboard:

  - Random Nerd Tutorials: [Turn Your Raspberry Pi Zero into a USB Keyboard (HID)](https://randomnerdtutorials.com/raspberry-pi-zero-usb-keyboard-hid/)

These are the steps that I followed:

  1. Install the latest version of the Raspberry&nbsp;Pi&nbsp;OS; this is written for the Bookworm releasae.
  2. Enable the Drivers and modules
     1. Add the line
        ```
        dtoverlay=dwc2
        ```
        to the end of `/boot/firmware/config.txt`.
      2. Add the lines
         ```
         dwc2
         libcomposite
         ```
         to the end of `/etc/modules`.
         
