# Minecraft Server Template

This template shows how to setup a Minecraft server as a `systemd` service, with RCON, tty support and optional log display to screen.

## Setup
### Server
create the directory `/srv/minecraft` and put your server files there, renaming the executable to `server.jar`
### User, Group
Following best practices, create a user, and group to run the server
```bash
groupadd minecraft
useradd -g minecraft minecraft
```
After you've placed all the files the sevrer needs in the `/srv/minecraft/` directory, change their owner to the created user
```bash
chown -R minecraft:minecraft /srv/minecraft/
```
### Services
Copy all the files located in `/etc/systemd/system` from the repository to the exact same path in the filesystem.
This will only work on systems with `systemd` enabled, namely Ubuntu 18.10 and newer. (my machines run Ubutnu 20.04)
The directory `/etc/systemd/system/getty@tty1.service` is optional, in case you plan on attaching a screen to the server, but not on using it for input, as this will bind a readonly stream to the output of the display.

Finally, To run the server and the execute the following commands
```bash
sudo systemctl daemon-reload
sudo systemctl enable minecraft
sudo systemctl start minecraft
sudo systemctl restart getty@tty1.service # optional
```
