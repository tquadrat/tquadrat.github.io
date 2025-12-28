# Installing an Operating System on a Raspberry&nbsp;Pi Compute Module

Installing an operating system on a Compute Module (CM4 or CM5) differs fundamentally depending on whether you have the Lite version (without internal storage) or the eMMC version (with built-in storage). Let's start the first scenario using an SD card for storage. Although we are talking here mainly about CM5, the steps are generally the same for a CM4.

## Case A: Installation on CM5 Lite (via microSD card)

This is the simplest method and works exactly the same as with the regular Raspberry&nbsp;Pi&nbsp;5.

  - Preparation: Insert your microSD card into your PC/laptop.
  - Start the Imager: Download and open the Raspberry Pi Imager.
  - Settings:
    - Device: Select "Raspberry Pi 5" (the CM5 is based on the Pi 5 architecture).
    - OS: Select the desired system (usually Raspberry Pi OS 64-bit).
    - Storage: Select your microSD card.
  - Configuration (gear icon): Here you can directly enable the hostname, Wi-Fi password, and SSH.
  - Write: Click "Next/Write." Once the process is complete, insert the card into the slot of your carrier board and start the module.

## Case B: Installation on CM5 with eMMC Internal Storage

If you want to use the storage directly on the module, you must first put the CM5 into a special mode so that your PC recognizes it as a "USB drive".

1. Hardware Preparation
   You need an I/O board (carrier board). There look for a jumper or switch on the board labeled "nRPiboot" or "USB Boot." This must be closed or set to "ON."

   Connect the USB slave port (usually USB-C or Micro-USB) of the I/O board to your PC.

   Connect the power supply to the I/O board if required; sometimes the power comes already through the slave port.

2. Using the "rpiboot" software

   Your PC won't automatically recognize the CM5. You need the `rpiboot` tool.

   ### Windows

     - Installation: Download the installer from GitHub (raspberrypi/usbboot) and run it.
     - Run: Start the `rpiboot` program. A black window will open, waiting for the module.

   Once rpiboot has found the CM5, it will upload drivers, and shortly afterward, the eMMC module will appear in your Windows Explorer as a regular drive.

   ### Linux

   Under Linux, the process is often even smoother, as the necessary tools are usually available directly in the repositories; if not, they can be quickly built yourself.

     #### Installation of `rpiboot`

     - Installation from repository:
       ```bash
       sudo apt update
       sudo apt install rpiboot
       ```
       This works for Ubuntu and Raspberry&nbsp;Pi&nbsp;OS

     - Build `rpiboot` from the sources
       Here is the step-by-step guide for installing eMMC on a CM5 under Linux (e.g., Ubuntu, Debian, Fedora):

       **1. Install dependencies**

         First, you need the `libusb` library to communicate directly with the Broadcom chip's bootloader via USB. On Debian/Ubuntu/Raspberry&nbsp;Pi&nbspOS:
         ```bash
         sudo apt update
         sudo apt install git libusb-1.0-0-dev pkg-config build-essential
         ```

       **2. Build the `rpiboot` tool**

         The official Raspberry Pi tool is called `usbboot`. You need to clone and compile it:
         ```bash
         git clone --depth=1 https://github.com/raspberrypi/usbboot
         cd usbboot
         make
         ```
         Now you have an executable file named `./rpiboot` in the current directory.

    #### Put the CM5 into programming mode

    This is the same hardware step as described previously:

      1. Set the jumper on your I/O board to **"nRPiboot"** (or close the switch).

      2. Connect the USB slave port of the I/O board to your Linux computer.

      3. Connect the power supply to the I/O board.

    #### Mounting the Module as a Drive

    Now start the program you just built with root privileges:
    ```bash
    sudo ./rpiboot
    ```
    
      **What happens now?**

      * The program waits for the CM5.

      * As soon as it is detected, `rpiboot` sends the boot code to the module.

      * The CM5 restarts and registers with your Linux system as a **new mass storage device** (USB drive).

      * In the terminal, you will see a message like: *“Second stage boot server done”*. The program then usually terminates automatically.


3. Flashing with the Imager

   Now you can open the Raspberry Pi Imager (as described in Case A).

   Under Storage, select the newly appearing drive (the CM5's eMMC).

   Write the operating system.

4. Completion
   Disconnect the power supply.

   Very important: Remove the jumper (`nRPiboot` or reset the switch, otherwise the module will attempt to enter programming mode instead of booting the OS on the next startup.

   Power it back on – done!

---

**A quick tip for Linux users:**
If your system doesn't automatically mount the device after the `rpiboot` process, use `dmesg | tail` or `lsblk` to check the name (e.g., `/dev/sdc`) under which it was registered.





