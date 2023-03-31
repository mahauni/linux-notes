


## Connecting to other devices (ssh)

to connect to other devices you have to use in your shell the ssh command

$ ssh [username]@[name_device]

after connecting you will be requested to enter the password to enter the device and after accessing you will have access to the machine.
super users probably will always have different different passwords than the normal users, but it don't cost anything to check if they are the same

## Adding users

you need to have super user access to add a new user

to create a user with restricted commands but with access to the shell you can do:

sudo useradd [username] -s /bin/bash 
or
sudo useradd [username] -s /bin/sh 

the option with available shell is a default value in the /etc/default/useradd, you can change it to have default values to flags, but leave if possible leave as it is.


to create a user without access to the shell do:

sudo useradd [username] -s /bin/false