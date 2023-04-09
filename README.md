


## Connecting to other devices (ssh)

to connect to other devices you have to use in your shell the ssh command
```bash
$ ssh [username]@[name_device]
```
after connecting you will be requested to enter the password to enter the device and after accessing you will have access to the machine.
super users probably will always have different different passwords than the normal users, but it don't cost anything to check if they are the same

## Adding users

you need to have super user access to add a new user

to create a user with restricted commands but with access to the shell you can do:
```bash
sudo useradd [username] -s /bin/bash 
or
sudo useradd [username] -s /bin/sh 
```
the option with available shell is a default value in the /etc/default/useradd, you can change it to have default values to flags, but leave if possible leave as it is.


to create a user without access to the shell do:
```bash
sudo useradd [username] -s /bin/false
```

### Timezones

to get the current date settings
```bash
$ timedatectl

to set the timezone to another one

$ timedatectl set-timezone [country]/[state]

to see the possibilities of timezones. It will not change the timezone.
It will only give to you information on how to change it.

$ tzselect 
```

### File permissions

Flags:

(r) -> Read
(w) -> Write
(x) -> Execute

(u) -> Users
(g) -> Group
(o) -> Others
(a) -> All

```bash
$ chmod [flags] [file or folder]
```

### RunLevel (Boot Target)

get the current boot target

```bash
$ systemctl get-default
```

List all the systemd targets

```bash
$ systemctl list-units --type target 
```

list all loaded units in any state #

```bash
$ systemctl list-units --type target --all
```

Boot Text

```bash
$ systemctl set-default multi-user.target
```

Boot GUI

```bash
$ systemctl set-default graphical.target
```

### Root Login

To enable ssh login, you should go to

```bash
$ cd /etc/ssh
```

and edit the sshd_config file with any editor you like.

to change the Root Login, you should take oof the '#' (comment) and choose between yes or no.

After changing restart the ssh with the command:

```bash
$ systemctl restart sshd
```