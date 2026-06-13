# Basic Software for Linux

## Software List
This is a list of software that I will install on each Linux machine that I work with. Some are less useful on Raspberry&nbsp;Pi machines, others I do not need on desktops and/or laptops.

Configuration files and scripts can be found in the *ChangeManagement* repository .

| | Ubuntu Desktop | Ubuntu Laptop | Raspberry Pi OS |
| :---: | :---: | :---: | :---: |
| `joe` | x | x | x |
| `curl` | x | x | x |
| `wget` | x | x | x |
| Java | x | x | x |
| Python 3 | x | x | x |
| Subversion | x | x | x |
| `git` | x | x | x |
| Git Credential Manager | x | x | x |
| go | x | x | x |
| SDKMAN! | x | x | x |
| Gradle | x | x | x |
| Remmina | x | x | x<sup>*</sup> |
| xRDP | | | x |
| GParted | x | x | x<sup>*</sup> |
| FileZilla | x | x | x<sup>*</sup> |
| Seahorse | | | x<sup>*</sup> |

<sup>*</sup> Only for systems with a GUI installed

### `curl`
`curl` is a command line tool for file transfer using the URL syntax. It is preinstalled on most Linux systems, but if not, it can be installed through `apt`.

### FileZilla
FileZilla is a graphical FTP client that supports also SFTP. Use `apt` to install it.

### `git`
`git` is an SCM that excels for distributed source code management, but it is also used a lot for the distribution of software. It will be installed through `apt`.

For my personal use, I prefer [Subversion](#subversion).

### Git Credential Manager
The GCM is used to simplify working with Git repositories. The installation is described [here](https://github.com/git-ecosystem/git-credential-manager).

### go
go (or golang) is a multi-purpose programming language. See [go.dev](https://go.dev) for details. The installation is described [here](InstallingGoOnLinux.md).

### GParted
GParted is a partition manager that allows to resize, copy, and move partitions without data loss. Can be useful also on a Raspberry&nbsp;Pi.

Will be installed through `apt`.

### Gradle
The [Gradle Build Tool](https://gradle.org/) is useful to build software and manage all its dependencies. It should be installed on any machine that is used for software development.

Gradle can be installed via `apt` as well as through `snap`, but both sources are usually not providing the latest versions. Therefore the recommended source is [SDKMAN!](https://sdkman.io/). See [here](#sdkman) on how to install "The Software Development Kit Manager" if not yet done.

How to update the Gradle Wrapper is described [here](UpdateGradleWrapper.md).

### Java

The latest LTS version of the JDK needs to be available on all machines. Although it could be installed through [SDKMAN!](#sdkman), I prefer to install it manually, the process is described [here](InstallingJavaOnLinux.md).

### `joe`

`joe` (*Joe's Own Editor*) is a simple text editor for the console window that works basically like the old Turbo Pascal editor. It is very similar to the `nano` editor, but I prefer `joe` over `nano`.

`joe` will be installed through `apt`.

#### Configure `joe`

The global configuration files for the editor `joe` can be found in `/etc/joe`; the main configuration settings are in `/etc/joe/joerc`. If you want to make the configuration adjustments only for a single user, or if you do not have `root` access, you can copy that file to your home directory:

```console
cp /etc/joe/joerc ~/.joerc
```

My personal preferences are:

 - `-indentc 32` – The indentation character (32 for space, 9 for tab).
 - `-istep 4` – The number of indentation columns.
 - `-lightoff`– Turns off highlighting after block copy or move.
 - `-linums` – Enables line numbers on each line.
 - `-rmargin 132` – The right margin for the word wrap.
 - `-spaces` – Let TAB inserting spaces instead of tabs.
 - `-tab 4` – The tabulator width.

To set `-lightoff`, search for that string in the configuration file and move it to the fist column, to activate the option:
```
…
 -break_links
		Delete file before writing, to break hard links
		and symbolic links.

-lightoff	Turn off highlighting after block copy or move

 -exask		^KX always confirms file name
…
```

For the other settings, search for the string "` Default local options`" and add the options below the found line:
```
…
 Default local options
-highlight
-istep 4

-indentc 32
-linums
-rmargin 132
-spaces
-tab 4

…
```

### Python 3

Python is an easy-to-learn multi-purpose programming language. Usually the latest version will be installed together with the operating system, otherwise it can be installed through `apt`.

### Remmina

[Remmina](https://remmina.org/) is a tool to access remote systems through `ssh`, `sftp` and `rdp`. I usually install it through `apt` but if this is not working, see [here](https://remmina.org/how-to-install-remmina/).

### SDKMAN!

[SDKMAN!](https://sdkman.io/) is a *packet manager* for software development tools. It will be installed through a shell command. Obviously it makes sense only on machines that are somehow used for software development.

For more information on the usage of SDKMAN!, see [here](https://sdkman.io/usage).

### Seahorse

Seahorse is a UI tool for the management of secrets, in particular for keyrings. It will be installed through `apt`.

### Subversion

[Apache Subversion](https://subversion.apache.org/) is another version control system, like [`git`](#git). When installed through `apt`, it brings both, the server and the client to the machine.

Mainly the client command `svn` is needed, as I use a Subversion repository for the various configuration files I need (aside that I use it for my own software projects, too).

### `wget`
`wget` is another command line tool to load files from the network. If not already installed, it can be made available through `apt`.

### xRDP

The server for the Remote Desktop protocol, mainly used on the Raspberry&nbsp;Pi systems. For details, see [here](https://github.com/tquadrat/tquadrat.github.io/blob/main/stuff/RaspberryStuff.md#remote-desktop-protocol).

## Installation Commands
  - Through `apt` for FileZilla, `git`, GParted, `joe`, Remmina, Subversion and xRDP:
    - Desktop, Laptop (Ubuntu):
      ```console
      sudo apt update
      sudo apt full-upgrade -y
      sudo apt install curl filezilla git gparted joe remmina subversion wget -y
      ```
    - Raspberry&nbsp;Pi (Raspberry Pi OS):
      ```console
      sudo apt update
      sudo apt full-upgrade -y
      sudo apt install curl filezilla git joe remmina seahorse subversion wget xrdp -y
      ```
  - Through shell command for SDKMAN!:

    To check whether "The Software Development Kit Manager" is installed already, execute
    ```console
    sdk version
    ```
    in a shell window. To install it, just execute
    ```console
    curl -s "https://get.sdkman.io" | bash
    ```
    followed by
    ```console
    source "$HOME/.sdkman/bin/sdkman-init.sh"
    ```
  - Through SDKMAN! for Gradle:   
    ```console 
    sdk install gradle
    ```
    This will install the latest version and set it as the default.

# Additional Software
## Tex/Latex
Tex/Latex is the preferred format for the creation of large documents. On Linux, this requires to install `texlive`, and my preferred editor for Tex/Latex is [`texmaker`](https://www.xm1math.net/texmaker/). The installation command for both is
```console
sudo apt install texlive texlive-fonts-extra biber texmaker
```
See [here](#TexStuff.md) for some hints regarding Tex/Latex.

