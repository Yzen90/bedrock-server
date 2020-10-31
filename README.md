# Minecraft™ Bedrock Server convenience scripts

### Tested with Ubuntu Server 18.04

## Contents
1. [Get the scripts](#get-the-scripts)
2. [Update the scripts](#update-the-scripts)
3. [New bedrock server instance](#new-bedrock-server-instance)
4. [Import existing bedrock server files to new instance](#import-existing-bedrock-server-files-to-new-instance)
   1. [Import example](#import-example)
5. [Update bedrock server instance](#update-bedrock-server-instance)
   1. [Instance update example](#instance-update-example)

## Get the scripts

Install required packages:

    sudo apt install curl grep wget unzip

Clone the repository:

    git clone https://github.com/xrnoz/bedrock-server.git
    cd bedrock-server

Or download and extract:

    wget https://github.com/xrnoz/bedrock-server/archive/master.zip
    unzip master.zip
    cd bedrock-server-master

[Back to top](#minecraft-bedrock-server-convenience-scripts)

## Update the scripts

With git:

    cd bedrock-server
    git pull

Or download and extract in directory that conains existing bedrock-server-master directory:

    wget https://github.com/xrnoz/bedrock-server/archive/master.zip -O master.zip
    unzip -o master.zip
    cd bedrock-server-master

[Back to top](#minecraft-bedrock-server-convenience-scripts)

## New bedrock server instance

`./new <instance name>`

- `<instance name>` Name that will be used as the systemd service name in the form of `mcbs-<instance name>` and in the `./instances` and `./run` directories for the new bedrock server instance. This argument will be converted to lowercase and it's whitespace trimmed.


[Back to top](#minecraft-bedrock-server-convenience-scripts)

## Import existing bedrock server files to new instance

`./import <source directory> <instance name>`

- `<source directory>` Path of directory that contains existing worlds directory and permissions.json, server.properties, whitelist.json files.

- `<instance name>` Name that will be used as the systemd service name in the form of `mcbs-<instance name>` and in the `./instances` and `./run` directories for the new bedrock server instance. This argument will be converted to lowercase and it's whitespace trimmed.

After the import is completed the bedrock server instance can be run with `./run/<instance name>/bedrock_server.sh` or to create, enable and start the systemd service for the instance, run `sudo ./install-service <instance name>`. After service install, run `systemctl status mcbs-<instance name>` to verify that the bedrock server instance is running properly.


### Import example

Source directory:

    /
    └─ path/
       └─ to/
          └─ bedrock/
             ├─ permissions.json
             ├─ server.properties
             ├─ whitelist.json
             └─ worlds/
                └─ ...

Import:

    :~/bedrock-server$ ./import /path/to/bedrock/ awesome-world

Run:

    :~/bedrock-server$ ./run/awesome-world/bedrock_server.sh

Install service and verify:

    :~/bedrock-server$ sudo ./install-service awesome-world
    :~/bedrock-server$ systemctl status mcbs-awesome-world

[Back to top](#minecraft-bedrock-server-convenience-scripts)

## Update bedrock server instance

`./update <instance name>`

- `<instance name>` Name of the instance that will be updated. This argument will be converted to lowercase and it's whitespace trimmed.

If the service for the instance is installed and is active, it must be stopped first with `sudo systemctl stop mcbs-<instance name>` to be able to update. After the update is completed, the service can be started again with `sudo systemctl start mcbs-<instance name>`.

To force the update if the instance is up to date, run `rm ./instances/<instance_name>/running-version` before `./update <instance name>`.

### Instance update example

    :~/bedrock-server$ sudo systemctl stop mcbs-awesome-world
    :~/bedrock-server$ ./update awesome-world
    :~/bedrock-server$ sudo systemctl start mcbs-awesome-world

[Back to top](#minecraft-bedrock-server-convenience-scripts)
