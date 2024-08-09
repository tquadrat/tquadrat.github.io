# Raspberry&nbsp;Pi as a USB Device

## Raspberry&nbsp;Pi&nbsp;Zero as a USB Keyboard

You can find different descriptions on how to configure a Raspberry&nbsp;Pi&nbsp;Zero as a virtual keyboard:

  - Random Nerd Tutorials: [Turn Your Raspberry Pi Zero into a USB Keyboard (HID)](https://randomnerdtutorials.com/raspberry-pi-zero-usb-keyboard-hid/)

### These are the steps that I followed:

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
         
  3. Configuring the Gadget
     
     Now, the Raspberry&ndsb;Pi&ndsb;Zero needs to be defined as a USB keyboard. The configuration is done via `ConfigFS`, a virtual file system located in `/sys/`.

     1. Creating the config script

        The configuration is volatile, so it must run on each startup. Create a new file called `virtual_usb` in `/usr/bin/` and make it executable:
        ```console
        sudo touch /usr/bin/virtual_usb
        sudo chmod +x /usr/bin/virtual_usb
        ```

     2. Run the script on each startup
    
        That this script is executed automatically at startup will be achieved by adding the line below to `/etc/rc.local` before the last line (that one reading `exit 0`):

        ```
        /usr/bin/virtual_usb # libcomposite configuration
        ```

     3. Creating the gadget
    
        For this project, the Raspberry&ndsb;Pi&ndsb;Zero is turned into a USB keyboard (but it could be made to work as a Serial adapter, an Ethernet adapter or Mass Storage).

        Open the scirpt file with:
        ```console
        joe /usr/bin/virtual_usb
        ```
        You can leave the default values as they are, but you could even change the serial number, manufacturer and product name to fit your specific needs.

        ```bash
        #!/bin/bash
        cd /sys/kernel/config/usb_gadget/
        mkdir -p virtual_usb
        cd virtual_usb
        echo 0x1d6b > idVendor # Linux Foundation
        echo 0x0104 > idProduct # Multifunction Composite Gadget
        echo 0x0100 > bcdDevice # v1.0.0
        echo 0x0200 > bcdUSB # USB2
        mkdir -p strings/0x409
        echo "fedcba9876543210" > strings/0x409/serialnumber
        echo "tquadrat.org" > strings/0x409/manufacturer
        echo "Virtual USB Device" > strings/0x409/product
        mkdir -p configs/c.1/strings/0x409
        echo "Config 1: ECM network" > configs/c.1/strings/0x409/configuration
        echo 250 > configs/c.1/MaxPower

        # Add functions here
        mkdir -p functions/hid.usb0
        echo 1 > functions/hid.usb0/protocol
        echo 1 > functions/hid.usb0/subclass
        echo 8 > functions/hid.usb0/report_length
        echo -ne \\x05\\x01\\x09\\x06\\xa1\\x01\\x05\\x07\\x19\\xe0\\x29\\xe7\\x15\\x00\\x25\\x01\\x75\\x01\\x95\\x08\\x81\\x02\\x95\\x01\\x75\\x08\\x81\\x03\\x95\\x05\\x75\\x01\\x05\\x08\\x19\\x01\\x29\\x05\\x91\\x02\\x95\\x01\\x75\\x03\\x91\\x03\\x95\\x06\\x75\\x08\\x15\\x00\\x25\\x65\\x05\\x07\\x19\\x00\\x29\\x65\\x81\\x00\\xc0 > functions/hid.usb0/report_desc
        ln -s functions/hid.usb0 configs/c.1/
        # End functions

        ls /sys/class/udc > UDC
        chmod 666 /dev/hidg0
        ```

  4. Connect the Raspberry&ndsb;Pi&ndsb;Zero to the target computer
    
     After the Raspberry&ndsb;Pi&ndsb;Zero is now prepared, shut it down and connect it to the target computer through the micro USB port that is used for data and peripherals. That micro USB will both power the Pi&nbsp;Zero and act as a keyboard to the connected computer.

   5. Test the new virtual keyboard
    
      Create this Python script `RPi_Keyboard_Example.py` somewhere:

      ```python
      #!/usr/bin/env python3
      NULL_CHAR = chr( 0 )

      def write_report( report ):
          with open( '/dev/hidg0', 'rb+' ) as fd:
              fd.write( report.encode() )

      # Press a
      write_report( NULL_CHAR * 2 + chr( 4 ) + NULL _ CHAR * 5 )
        
      # Release keys
      write_report( NULL_CHAR * 8 )

      # Press SHIFT + a = A
      write_report( chr( 32 ) + NULL_CHAR + chr( 4 ) + NULL_CHAR * 5 )

      # Press b
      write_report( NULL_CHAR * 2 + chr( 5 ) + NULL_CHAR * 5 )

      # Release keys
      write_report( NULL_CHAR * 8 )

      # Press SHIFT + b = B
      write_report( chr( 32 ) + NULL_CHAR + chr( 5 ) + NULL_CHAR * 5 )

      # Press SPACE key
      write_report( NULL_CHAR * 2 + chr( 44 ) + NULL_CHAR * 5 )

      # Press c key
      write_report( NULL_CHAR * 2 + chr( 6 ) + NULL_CHAR * 5 )

      # Press d key
      write_report( NULL_CHAR * 2 + chr( 7 ) + NULL_CHAR * 5 )

      # Press RETURN/ENTER key
      write_report( NULL_CHAR * 2 + chr( 40 ) + NULL_CHAR * 5 )

      # Press e key
      write_report( NULL_CHAR * 2 + chr( 8 ) + NULL_CHAR * 5 )

      # Press f key
      write_report( NULL_CHAR * 2 + chr( 9 ) + NULL_CHAR * 5 )

      # Release all keys
      write_report( NULL_CHAR * 8 )
      ```

      To start that script, type `python3 RPi_Keyboard_Example.py`. When you have opened a text editor on the target computer and placed the cursor in there, the sequence
      ```
      aAbB cd
      ef
      ```
      will by "typed" into it.
        
