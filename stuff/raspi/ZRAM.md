# Getting rid of `/dev/zram0`

When you install the Raspberry&nbsp;Pi&nbsp;OS that is based on Debian GNU/Linux&nbsp;13 (codenamed "trixie"), it uses a device `/dev/zram0` for swapping to memory. That eats up valuable resources there (but is very fast). When your system has an SSD installed, you should consider to used a SWAP partition instead. How to setup this is explained quite well at various locations in the web.

What's missing is how to to get rid of the `/dev/zram0`. There are a lot of different descriptions, especially when you ask your favourite AI, but none worked for me (at 2026-01-13). But finally I found the solution: remove the package `rpi-swap` (and, when you are at this point, also `zram-tools`), and the device is gone!

```bash
sudo apt purge rpi-swap zram-tools
sudo apt autoremove
``` 
