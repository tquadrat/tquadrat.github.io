# Installing Go on Linux
Go (or `golang`) is a multi-purpose programming language that was originally developed by Google. See [go.dev](https://go.dev) for details.

  1. Download the latest version of the Go development environment from [https://go.dev/dl/](https://go.dev/dl/) to `~/Downloads`. Alternatively, call `wget` in that folder:
     ```shell
     # Verify the version!
     wget https://go.dev/dl/go1.25.7.linux-arm64.tar.gz
     ``
  3. Delete the symbolic link `/opt/go` (if it exists), then extract the archive you just downloaded into `/opt`, creating a fresh Go tree in `/opt/go`:
     ```shell
     sudo rm /opt/go && sudo tar -C /opt -xzvf ~/Downloads/go*.tar.gz
     ```
     Do not untar the archive into an existing `/opt/go` tree! This is known to produce broken Go installations.
  4. Rename `/opt/go` to `/opt/go1.25.7` or whatever the current version of the software is.
     ```shell
     sudo mv /opt/go /opt/go1.25.7
     ```
  5. Create a symbolic link for the new folder:
     ```shell
     sudo ln -s /opt/go1.25.7 /opt/go
     ```   
  6. Add the environment variables for Go to `$HOME/.bashrc`:
     ```shell 
     # Go Environment Settings
     export GOROOT=/opt/go
     export GOPATH=$HOME/go
     export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
     ```
     **Note**: Changes made to a profile file may not apply until the next time you log into your computer. To apply the changes immediately, just run the shell commands directly or execute them from the profile using a command such as `source $HOME/.bashrc`.

	 Alternatively, the environment can be placed into `/etc/profile`, to make them system-wide available.

   8. Verify that you've installed Go by opening a command prompt and typing the following command:
      ```shell
      go version
      ```
      Confirm that the command prints the installed version of Go.
