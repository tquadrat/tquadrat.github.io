# Installing IntelliJ IDEA

IntelliJ IDEA is currently my preferred IDE for Java programming.

  1. Download the tarball for the respective architecture from here: [https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/) to `~/Downloads`.
  2. Create the folder for the software:
     ```shell
     cd /opt
     sudo mkdir intelliJ
     ```
  3. For IntelliJ IDEA Community, run:
     ```shell
     sudo tar -xzf ~/Downloads/ideaIC-*.tar.gz -C /opt/intelliJ
     ```
     **Warning**: Do not extract the tarball over an existing installation to avoid conflicts. Always extract it to a clean directory.
  4. Execute the `idea.sh` script from the extracted directory to run IntelliJ IDEA.
  5. Create a desktop entry﻿
     1. In the main menu, go to `Tools | Create Desktop Entry`. This requires that there is an open project.
     2. To pin the app to the dash, right-click the IntelliJ IDEA icon and select `Add to Favorites` or `An Dash anheften`, depending on language and version of the operating system.
     