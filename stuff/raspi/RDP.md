# The Remote Desktop Protocol

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

## Configuration Files

  - `/etc/xrdp/xrdp.ini` – The main configuration file; usually no changes required.
  - `/etc/xrdp/xrdp_keyboard.ini` – The keyboard configuration. 

## Black Screen after Login via `xRDP`

Usually this happens when the same user as for the RDP session is already logged in locally, and both are using the same window manager. In newer versions of the Raspberry&nbsp;Pi&nbsp;OS, Wayland is used instead of X11 – the latter is still used by `xRDP` – and as both are using different window manager implementations. Therefore it should work in most cases.
