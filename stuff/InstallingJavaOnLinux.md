# Installing Java

Although [SDKMAN!](https://sdkman.io/) and even `apt` allow to install a JDK, I prefer to do it manually.

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
     
     The following steps are for Linux operating systems; for Windows, you usually just starts the installer (`*.msi`) for the JDK.
     
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
     
[This page](jshellConfig.md#ubuntu-setup) describes how `jshell` can be configured to run integrated into the Ubuntu terminal.
