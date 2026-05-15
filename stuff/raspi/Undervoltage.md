# Switching off the Undervoltage Warning

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

  ## 1. The Clean Solution: The Official Power Supply
  Use the official **Raspberry&nbsp;Pi 27W USB-C Power Supply**. It's one of the few that supports the exact 5V/5A profile. This will make the message disappear immediately, and all USB devices will receive full power.

  ## 2. The Configuration Solution (Ignore the Warning & Remove the USB Limit)
  If you know your power supply is stable and you don't have any power-hungry USB devices (like external hard drives without their own power supply) connected, you can manually override the check.

   ### Method A: Via `config.txt`
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


   ### Method B: Via EEPROM Configuration (Recommended)
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

   ## 3. What happens if you only suppress the message?

   If you choose the software solution but your power supply is actually weak, the following can happen:

   * **System crashes:** As soon as you plug in a USB device, the voltage drops and the Pi restarts.

   * **Undervoltage Warnings:** The small yellow lightning bolt icon (or a warning in the upper right corner) will continue to appear if the voltage drops below 4.63V.

**Important for CM5 users:** Here the behaviour depends heavily on the **carrier board**. Some boards have their own current regulation, which tricks the module into thinking there's enough power, while others pass the CM5 warning directly through.
