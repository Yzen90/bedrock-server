# Minecraft™ Bedrock Server management scripts
## Tested with Ubuntu Server 18.04

### Install

`sudo apt install curl grep wget unzip`

`git clone https://github.com/xrnoz/bedrock-server.git`

`cd bedrock-server`

### New bedrock server instance

TODO

### Import existing bedrock server files

`./import <source directory> <instance name>`

- `<source directory>` Path of directory that has existing permissions.json, server.properties, whitelist.json files and worlds directory.

- `<instance name>` Name that will be used in the instances directory and as the systemd service name in the form of "`mcbs-<instance name>`".

> `<instance name>` is turned to lowercase and all whitespace removed.
>
> After import, run `sudo ./install-service <instance name>` to create, enable and start the systemd service for the instance.
>
> After service install, run `systemctl status mcbs-<instance name>` to verify that the bedrock server instance is running correctly.


#### Example:

`$ ./import /path/to/bedrock/ awesome-world`

`$ sudo ./install-service awesome-world`

`$ sudo systemctl status mcbs-awesome-world`

Where:

    /
    └─ path/
       └─ to/
          └─ bedrock/
             ├─ permissions.json
             ├─ server.properties
             ├─ whitelist.json
             └─ worlds/
                └─ My World/
                   ├─ db/
                   ├─ level.dat
                   └─ levelname.txt

### Update bedrock server

TODO
