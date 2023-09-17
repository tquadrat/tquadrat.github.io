# The Raspberry

Common information about the Raspberry Pi, my projects based on that computer, and other useful stuff around the "Pi".

---
## [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)

The official documentation for Raspberry Pi computers and microcontrollers

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
$ sudo systemctl status pijuice.service
$ sudo systemctl enable pijuice.service
$ sudo systemctl restart pijuice.service
```
