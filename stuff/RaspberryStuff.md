# The Raspberry

Common information about the Raspberry Pi, my projects based on that computer, and other useful stuff around the "Pi".

---
## [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html)

The official documentation for Raspberry Pi computers and microcontrollers

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

---
### [The Raspi Camera](raspi/CameraStuff.md)

Information on how to install the Raspberry Camera, and how to use it.

Foto mit der Kamera aufnehmen:

$ raspistill -v -o <dateiname>

Hierbei wird ein Foto mit eine (standarmäßig eingestellten) Verzögerung von fünf Sekunden aufgenommen und als JPEG mit dem angegebenen Dateinamen gespeichert. Durch die Option -v werden zusätzlich noch einige Informationen auf der Konsole ausgegeben.

Verzögerung
----------
Der CCD-Chip der Kamera benötigt eine gewisse Zeit zur Auto-Justierung, so dass der default-Wert für die Verzögerung auf 5000 Millisekunden eingestellt ist. Durch Angabe der Option "-t <delay>" kann die Verzögerung auf den angegebenen Wert in Millisekunden verändert werden; sie kann bis auf eine Millisekunde verringert werden, darunter leidet allerdings die Gesamtqualität des Fotos deutlich, insbesondere bei den Farben und beim Kontrast. 700 bis 1000 Millisekunden scheinen ein guter Wert zu sein, um vernünftige Fotos zu machen.

Spiegeln der Aufnahme
---------------------
Je nachdem wie das Kamera-Modul verbaut und aufgestellt wurde, kann es sein, dass man die Aufnahmen spiegeln möchte.

Mit der Option "-hf" spiegelt man das Foto horizontal, während die Option "-vf" es vertikal spiegelt.

---
### [The Sunfounder Pan-Tilt Hat](https://docs.sunfounder.com/projects/pantilt-v3/en/latest/)

  - [Repository with the Software](https://github.com/sunfounder/pan-tilt-hat.git)

