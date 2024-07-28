# Linux Stuff

  1. [Basix Software](#basic-software)
  2. [Shell Stuff](#shell-stuff)
  3. [Installing Java](#installing-java)
  4. [Miscellaneous Stuff](#updating-the-gradle-wrapper)

## Basic Software

This is a list of software that I will install on each Linux machine that I work with. Some are less useful on Raspberry&nbsp;Pi machines, others I do not need on desktops and/or laptops.

| Ubuntu Desktop | Ubuntu Laptop | Raspberry Pi OS |
| :---: | :---: | :---: |
| `joe` | `joe` | `joe` |
| Java | Java | Java |
| Subversion | Subversion | Subversion |
| `git` | `git` | `git` |
| SDKMAN! | SDKMAN! | SDKMAN! |
| Gradle | Gradle | Gradle |
| Remmina | Remmina | |
| | | xRDP |
| GParted | GParted | |


### `git`
`git` is an SCM that excels for distributed source code management, but it is also used a lot for the distribution of software. It will be installed through `apt`.

For my personal use, I prefer [Subversion](#subversion).

### GParted
GParted is a partition manager that allows to resize, copy, and move partitions without data loss. Can be useful also on a Raspberry&nbsp;Pi.

Will be installed through `apt`.

### Gradle
The [Gradle Build Tool](https://gradle.org/) is useful to build software and manage all its dependencies. It should be installed on any machine that is used for software development.

Gradle can be installed via `apt` as well as through `snap`, but both sources are usually not providing the latest versions. Therefore the recommended source is [SDKMAN!](https://sdkman.io/). See [here](#sdkman) on how to install "The Software Development Kit Manager" if not yet done.

How to update the Gradle Wrapper is described [here](#configure-joe).

### Java

The latest LTS version of the JDK needs to be available on all machines. Although it could be installed through [SDKMAN!](#sdkman), I prefer to install it manually, the process is described [here](#installing-java).

### `joe`

`joe` (*Joe's Own Editor*) is a simple text editor for the console window that works basically like the old Turbo Pascal editor. It is very similar to the `nano` editor, but I prefer `joe` over `nano`.

`joe` will be installed through `apt`. For the configuration of the editor, see [here](#configure-joe).

### Remmina

[Remmina](https://remmina.org/) is a tool to access remote systems through `ssh`, `sftp` and `rdp`. I usually install it through `apt` but if this is not working, see [here](https://remmina.org/how-to-install-remmina/).

### SDKMAN!

[SDKMAN!](https://sdkman.io/) is a *packet manager* for software development tools. It will be installed through a shell command. Obviously it makes sense only on machines that are somehow used for software development.

For more information on the usage of SDKMAN!, see [here](https://sdkman.io/usage).

### Subversion

[Apache Subversion](https://subversion.apache.org/) is another version control system, like [`git`](#git). When installed through `apt`, it brings both, the server and the client to the machine.

Mainly the client command `svn` is needed, as I use a Subversion repository for the various configuration files I need (aside that I use it for my own software projects, too).

### xRDP

The server for the Remote Desktop protocol, mainly used on the Raspberry&nbsp;Pi systems. For details, see [here](https://github.com/tquadrat/tquadrat.github.io/blob/main/stuff/RaspberryStuff.md#remote-desktop-protocol).

### Installation Commands

The installation of Java is described [here](#installing-java).

  - Through `apt` for `git`, GParted, `joe`, Remmina, Subversion and xRDP:
    - Desktop, Laptop:
      ```console
      sudo apt install git gparted joe reminna subversion
      ```
    - Raspberry&nbsp;Pi:
      ```console
      sudo apt install git joe xrdp subversion
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
    $ sdk install gradle 8.7
    ```
    (here for version 8.7).

## Shell Stuff

Some tips and tricks for the Shell, mainly for the Bash shell.

### History

The *bash* history is a powerful feature for the work on the console of a Linux system.

#### [Removing and avoiding Duplicates in the History](https://www.baeldung.com/linux/history-remove-avoid-duplicates)

##### Manual Deduplication

```console
export HISTCONTROL=ignoreboth:erasedups
history -a
history -w
awk '!a[$0]++' $HOME/.bash_history > $HOME/.bash_history.tmp && mv $HOME/.bash_history.tmp $HOME/.bash_history
```

This of course does not remove the duplicates that are already/still hold in memory. Here a reboot or at least a re-login would help.

##### Make it permanent

Add
```shell
export HISTCONTROL=ignoreboth:erasedups
```
to `/etc/rc.local` or to `$HOME/.bashrc` and reboot.

Some distributions may already set `$HISTCONTROL` in `$HOME/.bashrc`.

An enhancement is described [here](https://unix.stackexchange.com/a/556267/280398). This leads to a `$HOME/.bashrc` like this:

```shell
# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth:erasedups

# don't put simple commands to the history
HISTIGNORE=cd:ls:"ls -la":exit

# append to the history file, don't overwrite it
shopt -s histappend

# merge the history for all sessions on close
function historymerge {
    history -n; history -w; history -c; history -r;
}
trap historymerge EXIT

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=5000
HISTFILESIZE=15000
```

## Installing Java

Although [SDKMAN!](https://sdkman.io/) also allows to install a JDK, I prefer to do it manually.

  1. Download the install package from the [Eclipse Temurin Download page](https://adoptium.net/de/temurin/releases/).
   
     Select the latest LTS version of the JDK that fits for the target operation system.

     | Target | Architecture |
     | --- | --- |
     | Ubuntu on Desktop/Laptop | x64 |
     | MacOS on Intel | x64 |
     | MacOS on A# | aarch64 |
     | Windows | x64 |
     | Raspberry Pi OS 64bit | aarch64 |
     | Raspberry Pi OS 32bit | arm |

     Perhaps some versions are not available for all targets.
     
  2. Create the target folder:
     ```console
     cd /opt
     sudo mkdir java
     ```

  3. Install the JDK in the target folder; if the downloaded file from the first step was stored in the `Downloads` folder, the command would be like this:
     ```console
     cd /opt/java
     sudo tar -xvf ~/Downloads/OpenJDK….tar.gz
     ```

     Of course the correct name for the file must be provided.

  4. Create the shell script `SetupJava.sh` somewhere on the local `PATH` (usually `~/bin` or `~/.local/bin`).

     The contents of the file looks like this:
     ```shell
     #! /bin/sh
     JAVA_PATH="/opt/java/<install_path>/bin"

     sudo update-alternatives --install "/usr/bin/jar" "jar" $JAVA_PATH/jar 1 
     sudo update-alternatives --set "jar" $JAVA_PATH/jar 

     sudo update-alternatives --install "/usr/bin/jarsigner" "jarsigner" $JAVA_PATH/jarsigner 1 
     sudo update-alternatives --set "jarsigner" $JAVA_PATH/jarsigner 

     sudo update-alternatives --install "/usr/bin/java" "java" $JAVA_PATH/java 1
     sudo update-alternatives --set "java" $JAVA_PATH/java

     sudo update-alternatives --install "/usr/bin/javac" "javac" $JAVA_PATH/javac 1
     sudo update-alternatives --set "javac" $JAVA_PATH/javac

     sudo update-alternatives --install "/usr/bin/javadoc" "javadoc" $JAVA_PATH/javadoc 1
     sudo update-alternatives --set "javadoc" $JAVA_PATH/javadoc

     sudo update-alternatives --install "/usr/bin/javap" "javap" $JAVA_PATH/javap 1
     sudo update-alternatives --set "javap" $JAVA_PATH/javap

     sudo update-alternatives --install "/usr/bin/jcmd" "jcmd" $JAVA_PATH/jcmd 1 
     sudo update-alternatives --set "jcmd" $JAVA_PATH/jcmd
     
     sudo update-alternatives --install "/usr/bin/jconsole" "jconsole" $JAVA_PATH/jconsole 1 
     sudo update-alternatives --set "jconsole" $JAVA_PATH/jconsole

     sudo update-alternatives --install "/usr/bin/jdb" "jdb" $JAVA_PATH/jdb 1 
     sudo update-alternatives --set "jdb" $JAVA_PATH/jdb

     sudo update-alternatives --install "/usr/bin/jdeprscan" "jdeprscan" $JAVA_PATH/jdeprscan 1 
     sudo update-alternatives --set "jdeprscan" $JAVA_PATH/jdeprscan

     sudo update-alternatives --install "/usr/bin/jdeps" "jdeps" $JAVA_PATH/jdeps 1 
     sudo update-alternatives --set "jdeps" $JAVA_PATH/jdeps

     sudo update-alternatives --install "/usr/bin/jfr" "jfr" $JAVA_PATH/jfr 1 
     sudo update-alternatives --set "jfr" $JAVA_PATH/jfr

     sudo update-alternatives --install "/usr/bin/jhsdb" "jhsdb" $JAVA_PATH/jhsdb 1 
     sudo update-alternatives --set "jhsdb" $JAVA_PATH/jhsdb

     sudo update-alternatives --install "/usr/bin/jinfo" "jinfo" $JAVA_PATH/jinfo 1 
     sudo update-alternatives --set "jinfo" $JAVA_PATH/jinfo

     sudo update-alternatives --install "/usr/bin/jlink" "jlink" $JAVA_PATH/jlink 1 
     sudo update-alternatives --set "jlink" $JAVA_PATH/jlink

     sudo update-alternatives --install "/usr/bin/jmap" "jmap" $JAVA_PATH/jmap 1 
     sudo update-alternatives --set "jmap" $JAVA_PATH/jmap

     sudo update-alternatives --install "/usr/bin/jmod" "jmod" $JAVA_PATH/jmod 1 
     sudo update-alternatives --set "jmod" $JAVA_PATH/jmod

     sudo update-alternatives --install "/usr/bin/jpackage" "jpackage" $JAVA_PATH/jpackage 1 
     sudo update-alternatives --set "jpackage" $JAVA_PATH/jpackage

     sudo update-alternatives --install "/usr/bin/jrunscript" "jrunscript" $JAVA_PATH/jrunscript 1 
     sudo update-alternatives --set "jrunscript" $JAVA_PATH/jrunscript

     sudo update-alternatives --install "/usr/bin/jshell" "jshell" $JAVA_PATH/jshell 1 
     sudo update-alternatives --set "jshell" $JAVA_PATH/jshell

     sudo update-alternatives --install "/usr/bin/jstack" "jstack" $JAVA_PATH/jstack 1 
     sudo update-alternatives --set "jstack" $JAVA_PATH/jstack
     
     sudo update-alternatives --install "/usr/bin/jstat" "jstat" $JAVA_PATH/jstat 1 
     sudo update-alternatives --set "jstat" $JAVA_PATH/jstat

     sudo update-alternatives --install "/usr/bin/jstatd" "jstatd" $JAVA_PATH/jstatd 1 
     sudo update-alternatives --set "jstatd" $JAVA_PATH/jstatd

     sudo update-alternatives --install "/usr/bin/jwebserver" "jwebserver" $JAVA_PATH/jwebserver 1 
     sudo update-alternatives --set "jwebserver" $JAVA_PATH/jwebserver

     sudo update-alternatives --install "/usr/bin/keytool" "keytool" $JAVA_PATH/keytool 1 
     sudo update-alternatives --set "keytool" $JAVA_PATH/keytool

     sudo update-alternatives --install "/usr/bin/rmiregistry" "rmiregistry" $JAVA_PATH/rmiregistry 1 
     sudo update-alternatives --set "rmiregistry" $JAVA_PATH/rmiregistry

     sudo update-alternatives --install "/usr/bin/serialver" "serialver" $JAVA_PATH/serialver 1 
     sudo update-alternatives --set "serialver" $JAVA_PATH/serialver
     ```
     
     Set the respective installation path and save the script. For future versions of the JDK, additional tools could be added and would require additional entries to the script. Of course, other tools may get dropped from the JDK, and the respective lines need to be removed.

  5. Make the script executable and run it:
     ```console
     chmod u+x SetupJava.sh
     SetupJava.sh
     ```   
     
[This page](https://github.com/tquadrat/tquadrat.github.io/blob/main/stuff/jshellConfig.md#jshell-startup-configuration) describes how `jshell` can be configured to run integrated into the Ubuntu terminal.

## Miscellaneous Stuff

Some useful tweaks and configuration settings for the Linux operating system and Linux tools.

### Updating the Gradle Wrapper

In most cases, a project is built using the [Gradle Wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html). And of course, at some point the version of the wrapper needs to be updated when the Gradle version is updated.

Use the `wrapper` Gradle task to upgrade Gradle Wrapper. It not only updates the Gradle version in the `gradle-wrapper.properties` file, but it also updates the Wrapper shell script (`gradlew`) and the Gradle Wrapper jar (`gradle-wrapper.jar`).

You can run the wrapper task from the terminal, specifying the latest version
```console
./gradlew wrapper --gradle-version latest
```
or the specific version you want:
```console
./gradlew wrapper --gradle-version 8.1.1
```

### Configure `joe`

The global configuration files for the editor `joe` can be found in `/etc/joe`; the main configuration settings are in `/etc/joe/joerc`. If you want to make the configuration adjustments only for a single user, or if you do not have `root` access, you can copy that file to your home directory:

```console
$ cp /etc/joe/joerc ~/.joerc
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

