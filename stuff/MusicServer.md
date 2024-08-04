# Music Server

My requirements for a Music Server were the following:

  - it must be able to play live streams from internet radio stations
  - it has to be able to output to AirPlay as I use two old Apple TVs as connectors to my speakers
  - it should run on a Raspberry&nbsp;Pi; running on Pi&nbsp;4 would be nice, as I have several of them, but requiring a Pi&nbsp;5 would not cause serious issues

After some research in the Web, I found [OwnTone](https://owntone.github.io/owntone-server/).

## Installation of OwnTone

The starting page for the installation of OwnTone in general can be found [here](https://owntone.github.io/owntone-server/installation/). It provides links to detailed instructions for the different targets.

As I want to install it on a Raspberry&nbsp;Pi, I used the description provided [here](https://forums.raspberrypi.com/viewtopic.php?t=49928).

  1. General Preparations

     I installed the latest Raspberry&nbsp;Pi&nbsp;OS, using the [Imager](https://www.raspberrypi.com/documentation/computers/getting-started.html#raspberry-pi-imager); at the time of writing (2024-08-04) this is the 64-bit Bookworm version, with Desktop and SSH enabled.

     Next I followed the steps from the [*Linux Stuff* page](LinuxStuff.md) to install the [basic software](LinuxStuff.md#basic-software) and [Java](LinuxStuff.md#installing-java), and to configure the software.

     I switched off WiFi and assigned a fixed IP address to the music server.

  3. Create the Folders for the Music

     I decided to store the files in the users `home` folder; there already exists a folder `Music`. So I created the necessary folders there:
     ```console
     cd ~/Music
     mkdir Audiobooks Compilations Podcasts
     ```

  4. Add the repository key for the OwnTone repository:
     ```console
     wget -q -O - http://www.gyfgafguf.dk/raspbian/owntone.gpg | sudo gpg --dearmor --output /usr/share/keyrings/owntone-archive-keyring.gpg
     ```
     
  5. Add the repository for *Bookworm* :
     ```console
     sudo wget -q -O /etc/apt/sources.list.d/owntone.list http://www.gyfgafguf.dk/raspbian/owntone-bookworm.list
     ```
     According to the documentation, there are also versions for *Bullseye' and 'Buster' available.

  6. Install the software
     ```console
     sudo apt update
     sudo apt install owntone -y
     ```

  7. For the next steps, it is useful when OwnTone is currently not running, therefore we make sure that it does not run:
     ```console
     sudo service owntone stop
     ```

  8. Move the data files to the target location in the `home` folder.
     ```console
     mkdir -p ~/.local/share/owntone/cache ~/.local/share/owntone/log
     sudo mv /var/cache/owntone/* ~/.local/share/owntone/cache/
     sudo chmod <user>:<group>  ~/.local/share/owntone/cache/*
     sudo rmdir /var/cache/owntone
     sudo rm /var/log/owntone
     
     ```
     
  8. Edit the configuration file `/etc/owntone.conf` to suit the individual needs. The line numbers may vary.
     ```
     …
      10 general {
      11     # Username
      12     # Make sure the user has read access to the library directories you set
      13     # below, and full access to the databases, log and local audio
      14     uid = "<user>"
      15 
      16     # Database location
      17     db_path = "/home/<user>/.local/share/owntone/cache/songs3.db"
      18 
      19     # Database backup location
      20     # Uncomment and specify a full path to enable abilty to use REST endpoint
      21     # to initiate backup of songs3.db
      22     db_backup_path = "/home/<user>/.local/share/owntone/cache/songs3.bak"
      23 
      24     # Log file and level
      25     # Available levels: fatal, log, warning, info, debug, spam
      26     logfile = "/home/<user>/.local/share/owntone/log/owntone.log"
      27     loglevel = log
      28 
     …
      54 
      55     # Location of cache database
      56     cache_path = "/home/<user>/.local/share/owntone/cache/cache.db"
      57
     …
      70 }
      71 
      72 # Library configuration
      73 library {
      74     # Name of the library as displayed by the clients (%h: hostname). If you
      75     # change the name after pairing with Remote you may have to re-pair.
      76     name = "Music on %h"
      77 
      78     # TCP port to listen on. Default port is 3689 (daap)
      79     port = 3689
     …
      84     # Directories to index
      85     directories = { "/home/<user>/Music" }
     …
     235 
     236     # Allows creating, deleting and modifying m3u playlists in the library directories.
     237     # Only supported by the player web interface and some mpd clients
     238     # Defaults to being disabled.
     239     allow_modifying_stored_playlists = true
     …
     246     # By default OwnTone will - like iTunes - clear the playqueue if
     247     # playback stops. Setting clear_queue_on_stop_disable to true will keep
     248     # the playlist like MPD does. Note that some dacp clients do not show
     249     # the playqueue if playback is stopped.
     250     clear_queue_on_stop_disable = true
     251 }
     252 
     …
     ```
     I do not have a speaker system directly connected to the music server, therefore the local audio output is disabled.
     ```
     …
     252 
     253 # Local audio output
     254 #audio {
     255     # Name - used in the speaker list in Remote
     256 #   nickname = "Computer"
     257
     …
     294 #}
     295 
     …
     ```
     
  9. Start/restart the OwnTone service:
     ```console
     sudo service owntone start
     ```

  10. Wait for the library scan to complete. The progress can be followed with one of the commands below:
      ```console
      tail -f /home/<user>/.local/share/owntone/log/owntone.log
      sudo service owntone status
      journalctl -xeu owntone.service
      systemctl status owntone.service
      ```

  11. Connect to the music server with a browser through the URL `http://<server>:3689/` and finish the configuration there.

Finally I had to move the music files to the `~/Music` folder to make it available.

For internet radio stations, I have created a `Radio.m3u` in `~/Music` that contains the links to the respective streams.
