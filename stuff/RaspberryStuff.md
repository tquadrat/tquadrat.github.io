# The Raspberry

Common information about the Raspberry Pi, my projects based on that computer, and other useful stuff around the "Pi".

---
## [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)

The official documentation for Raspberry Pi computers and microcontrollers. The Raspi Imager can be found [here](https://www.raspberrypi.com/software/).

---
## [The Raspi Camera](raspi/CameraStuff.md)

Information on how to install the Raspberry Camera, and how to use it.

---
## Miscellaneous

Unsorted notes about various features of the Raspberry Pi and components to use with it.

---
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

### Remote Desktop Protocol

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
