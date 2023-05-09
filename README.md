# Linux

When doing a command is always good look the manual, so than always is good to do:

```bash
$ man [command]
```

it is also good to check if the service is running without problems with:
```bash
$ systemctl status [program]
```
and this will show the status of the program typed, good for checking for easy fails.

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

to create a user with a expire date:
```bash
sudo useradd -e [YYYY-MM-DD] [username]
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

### SSH connection without password

If you want to connection ssh without password, because you have to connect everyday or something and you dont want to pass password everytime conecting

You will need to have a ssh key. If you dont have, do this command

```bash
$ ssh-keygen
```

After typing this, it will appear some configurations, but you can use the default configurations. So it will create a pair ssh key in the ~/.ssh, a private (.pub) and a private. But you dont need to care about it.

So to make the connection without password, you will need to:

```bash
$ ssh-copy-id [name]@[ip]
```

After typing you will have to make the same steps when connecting, and then after all the configuration.
You should be able to make a ssh without need the password

### Find

the command find is a powerfull tool to find files with some characterists and than do some commands like mv, rm or cp. 

This powerfull command is a bit tricky to use, so use it mostly with cp and not with other because it can cause some big trouble if done wrong.

the command is like this

```bash
$ find [dir] [flags] -type f -exec [other command (cp)] [flags] [to dir] {} +
```

the command is find all files in the dir that correspond to the flags, like -user to find the user, -name to find some file with specif name and a lot of more of flags.
the -type f is to get only the files with the path.

the exec command need the command, flags like --parent to cp all the parents folders too to a certain dir

ex. 

```bash
$ find /home/usr -user some_other_user -type f -exec cp --parents /home/usr2 {} +
```

### String manipulation (sed)

we can replace or delete some ocurrence of said string in some file:

- replace:
```bash
$ sed 's/\b[string]\b/[string_to_be_replaced]/g' [file] > [to_file]
```

- delete
```bash
$ sed '/\<[string]\>/d' [file] > [to_file]
```

### Cron

This is a tool to automate programs when certain periods of time has been elapsed. So 5 in 5 minutes for example.
To set up this you will need to have installed cronie.
```bash
$ yum install cronie -y
```
After installed you will have to start the crond in your machine, and to do that you will have to
```bash
$ service crond start

$ service crond status
```
After seeing the status of crond and seeing it is active

you can edit the cron file with
```bash
$ crontab -e

$ contab -l
```
After you edit you can see all your cron with the list. And after seeing the command is there its all good now

Ex. of some cron code:
*/5 * * * * echo hello > /tmp/cron_text

### DNS

To add more nameservers to the server, we can do this changing the file in /etc/resolv.conf and add the line nameserver [DNS] and we can add multiple lines to the DNS.