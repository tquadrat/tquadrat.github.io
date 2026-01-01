# The Raspberry

Common information about the Raspberry Pi, my projects based on that computer, and other useful stuff around the "Pi". Refer also to the [page with the Linux Stuff](https://github.com/tquadrat/tquadrat.github.io/blob/main/stuff/LinuxStuff.md#linux-stuff) for information related to the Linux operating system in general.

   1. [General Documentation](#raspberry-pi-documentation)
   2. [The Raspi Camera](#the-raspi-camera)
   3. [The Raspi as a USB Device](#the-raspi-as-a-usb-device)
   4. [Installing a Compute Module](#installing-a-compute-module)
   5. [Miscellaneous](#miscellaneous)

---
## [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)

The official documentation for Raspberry Pi computers and microcontrollers. The Raspi Imager can be found [here](https://www.raspberrypi.com/software/).

---
## [The Raspi Camera](raspi/CameraStuff.md)

Information on how to install the Raspberry Camera, and how to use it.

## [The Raspi as a USB Device](raspi/RaspiAsKeyboard.md)

Information on how to use a Raspberry&nbsp;Pi as a USB device (like a keyboard or a harddrive) for another computer. Mainly Raspberry&nbsp;Pi&nbsp;Zero models are used for this purpose, but also Pi&nbsp;4 and Pi&nbsp;5 can be used this way.

---
## Installing a Compute Module

The Compute Modules are an alternative to a 'real' Raspberry&nbsp;Pi for the use in embedded systems. They lack the connectors of the Raspberry&nbsp;Pi, these needs to be provided by the host board. But they come with built-in eMMC memory (if not the lite version), so there is no need for an external MicroSD card for the operating system.

How to install the operating system on a CM5 is described [here](raspi/InstallCM.md).

---
## Miscellaneous

Unsorted notes about various features of the Raspberry Pi and components to use with it.

1. [Switching off the Undervoltage Warning](#switching-off-the-undervoltage-warning)
2. [Setting up a Music Server](#setting-up-a-music-server)
3. [PiJuice](#pijuice)
4. [The Remote Desktop Protocol](#the-remote-desktop-protocol)

---
### Switching off the Undervoltage Warning

The Raspberry&nbsp;Pi&nbsp;5 is quite particular about power supplies. Many "powerful" mobile phone chargers deliver 25W or more, but often at higher voltages (9V, 12V) and not at the **5V/5A** required by the Raspi, while weaker power supplies really do not provide sufficient power.

The message "This power supply is not capable to deliver 5A …" (or a small yellow lightning bolt icon in the upper right corner of the screen) appears on the Raspberry&nbsp;Pi&nbsp;5 because it communicates with the power supply via the *"USB-C Power Delivery (PD)"* protocol. If the power supply doesn't signal that it can deliver **5A at 5V**, the Raspi reduces the current to the USB ports (from 1.6A to 600mA) as a safety precaution to prevent system crashes.

The command `vcgencmd` can be used to get some more insight into the current power consumption of you Raspi. With
```bash
vcgencmd get_throttled
```
you get information whether the Raspi is currently throttled due to low voltage. An output like
```text
throttled=0x0
```
indicates that currently everything is alright.

```bash
vcgencmd pmic_read_adc
```
provides more detailed information.

If your problem is really only the incomplete communication between the Raspi and the power supply, here are three ways to get rid of the message:  

  #### 1. The Clean Solution: The Official Power Supply
  Use the official **Raspberry&nbsp;Pi 27W USB-C Power Supply**. It's one of the few that supports the exact 5V/5A profile. This will make the message disappear immediately, and all USB devices will receive full power.

  #### 2. The Configuration Solution (Ignore the Warning & Remove the USB Limit)
  If you know your power supply is stable and you don't have any power-hungry USB devices (like external hard drives without their own power supply) connected, you can manually override the check.

   ##### Method A: Via `config.txt`
   1. Open the configuration file in the terminal:
     ```bash
     sudo joe /boot/firmware/config.txt
     ```
     *(For older versions: `/boot/config.txt`)*

   2. Add this line to the end of the file:
     ```text
     usb_max_current_enable=1
     ```

   3. Save and exit with `Ctrl+KX`.
   4. Restart the Raspi.


   #### Method B: Via EEPROM Configuration (Recommended)
   This is the most reliable method to suppress the boot warning directly at the hardware level:
   1. Enter the following command:
      ```bash
      sudo rpi-eeprom-config --edit
      ```
   2. Find or add the line `PSU_MAX_CURRENT`:
      ```text
      PSU_MAX_CURRENT=5000
      ```
   3. Save with `Ctrl+O`, `Enter`, and exit with `Ctrl+X`.
   4. Reboot the Raspi.
   
   The Raspi will now "think" it has a 5A power supply.

   #### 3. What happens if you only suppress the message?

   If you choose the software solution but your power supply is actually weak, the following can happen:

   * **System crashes:** As soon as you plug in a USB device, the voltage drops and the Pi restarts.

   * **Undervoltage Warnings:** The small yellow lightning bolt icon (or a warning in the upper right corner) will continue to appear if the voltage drops below 4.63V.

**Important for CM5 users:** Here the behaviour depends heavily on the **carrier board**. Some boards have their own current regulation, which tricks the module into thinking there's enough power, while others pass the CM5 warning directly through.

### Setting up a Music Server

How to setup a music server based on [OwnTone](https://owntone.github.io/owntone-server/) is described [here](MusicServer.md). This software does not only run on a Raspberry&nbsp;Pi, but also on various other Linux versions.

### PiJuice

The PiJuice hat provides a UPS to the Raspberry Pi. It provides also an RTC.

  - [Installation of PiJuice](https://learn.pi-supply.com/make/pijuice-quick-start-guide-faq/#software-installation)

If the PiJuice GUI does not start, refer [to this article](https://github.com/PiSupply/PiJuice/issues/1000).

To enable the PiJuice Service that is required to configure the software, try this:
```bash
sudo systemctl status pijuice.service
sudo systemctl enable pijuice.service
sudo systemctl restart pijuice.service
```

### The Remote Desktop Protocol

From [Wikipedia](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol): 

> **Remote Desktop Protocol (RDP)** is a proprietary protocol developed by Microsoft Corporation which provides a user with a graphical interface to connect to another computer over a network connection. The user employs RDP client software for this purpose, while the other computer must run RDP server software.
>
> […]
>
> Microsoft currently refers to their official RDP client software as Remote Desktop Connection, formerly "*Terminal Services Client*".
>
> The protocol is an extension of the [ITU-T T.128](https://en.wikipedia.org/wiki/T.120) application sharing protocol. […]

To use the *Remote Desktop Protocol* (RDP) to access the Raspberry&nbsp;Pi computer, the server software `xRDP` must be installed on it:
```bash
sudo apt install xrdp
```

Of course on the client machine (that one that displays the Raspi's desktop), a corresponding client software is required

#### Configuration Files

  - `/etc/xrdp/xrdp.ini` – The main configuration file; usually no changes required.
  - `/etc/xrdp/xrdp_keyboard.ini` – The keyboard configuration. 

#### Black Screen after Login via `xRDP`

Usually this happens when the same user as for the RDP session is already logged in locally, and both are using the same window manager. In newer versions of the Raspberry&nbsp;Pi&nbsp;OS, Wayland is used instead of X11 – the latter is still used by `xRDP` – and as both are using different window manager implementations. Therefore it should work in most cases.
