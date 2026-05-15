# PiJuice

The PiJuice hat provides a UPS to the Raspberry Pi. It provides also an RTC.

  - [Installation of PiJuice](https://learn.pi-supply.com/make/pijuice-quick-start-guide-faq/#software-installation)

If the PiJuice GUI does not start, refer [to this article](https://github.com/PiSupply/PiJuice/issues/1000).

To enable the PiJuice Service that is required to configure the software, try this:
```bash
sudo systemctl status pijuice.service
sudo systemctl enable pijuice.service
sudo systemctl restart pijuice.service
```
