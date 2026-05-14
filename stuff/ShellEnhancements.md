# Shell Enhancements

Some tips and tricks for the Linux shell, mainly for the `bash` shell.

## `history`

The `bash` history is a powerful feature for the work on the console of a Linux system.

### [Removing and avoiding Duplicates in the History](https://www.baeldung.com/linux/history-remove-avoid-duplicates)

#### Manual Deduplication

```console
export HISTCONTROL=ignoreboth:erasedups
history -a
history -w
awk '!a[$0]++' $HOME/.bash_history > $HOME/.bash_history.tmp && mv $HOME/.bash_history.tmp $HOME/.bash_history
```

This of course does not remove the duplicates that are already/still hold in memory. Here a reboot or at least a re-login would help.

#### Make it permanent

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

## Command Aliases

The `bash` can be enhanced through aliases that will be defined in `.bash_aliases` like this:

```bash
alias <name>="<command sequence>"
```

Here are the aliases that I use regularly:
```bash
alias histfind="history | grep $*"
alias md="mkdir -p"
alias mdcd="source mdcd.sh"
```

 - `histfind` searches a recently used command in the command history.
 
 - `md` creates a new directory and all missing parent directories in one go.

 - `mdcd` creates a new directory and changes to it afterwards. This alias requires a shell script named `mdcd.sh` somwhere on the path.
 
   The script looks like this:
   ```bash
    #!/bin/bash

    mkdir -p "$1"
    eval cd "$1"
   ```
 
