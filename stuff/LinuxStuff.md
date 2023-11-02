# Linux Stuff

## Shell Stuff

Some tips and tricks for the Shell, mainly for the Bash shell.

### History

The *bash* history is a powerful feature for the work on the console of a Linux system.

#### [Removing and avoiding Duplicates in the History](https://www.baeldung.com/linux/history-remove-avoid-duplicates)

##### Manual Deduplication

```console
$ export HISTCONTROL=ignoreboth:erasedups
$ history -a
$ history -w
$ awk '!a[$0]++' $HOME/.bash_history > $HOME/.bash_history.tmp && mv $HOME/.bash_history.tmp $HOME/.bash_history
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

## Miscellaneous Stuff

Some useful tweaks and configuration settings for the Linux operating system and Linux tools.

### Editors

For most Linux distributions, `nano` is the default editor when working in a shell. But for various reasons, I prefer `joe`; it will be installed like this:
```console
$ sudo apt install joe
```

#### Configure `joe`

The global configuration files for the editor `joe` can be found in `/etc/joe`; the main configuration settings are in `/etc/joe/joerc`. If you want to make the configuration adjustments only for a single user, or if you do not have `root` access, you can copy that file to your home directory:

```console
$ cp /etc/joe/joerc ~/.joerc
```
My personal preferences are:

 - `-indentc 32` – The indentation character (32 for space, 9 for tab).
 - `-istep 4` – The number of indentation columns.
 - `-linums` – Enables line numbers on each line.
 - `-mouse` – Enables xterm mouse support. When enabled, left-click will position the cursor and left-click-drag will select blocks. For normal xterm cut and paste, hold the shift key down.
 - `-rmargin 132` – The right margin for the word wrap.
 - `-spaces` – Let TAB inserting spaces instead of tabs.
 - `-tab 4` – The tabulator width.

To set `-mouse`, search for that string in the configuration file and move it to the fist column, to activate the option:
```
…
-joe_state     Use ~/.joe_state file

-mouse         Enable xterm mouse support.  When enabled, left-click will
                position the cursor and left-click-drag will select blocks
                For normal xterm cut and paste, hold the shift key down.

 -joexterm      If you are using XTerm version 212 or higher, and if it wa
                configured with --enable-paste64, set this flag: it allows
                mouse cut & paste to work properly (text selected with the
                mouse can be pasted into other application, and middle
                button clicks paste into JOE).
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

