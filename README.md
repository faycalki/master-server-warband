![Logo](https://i.imgur.com/ibTMkw3.png)

# Master Server (Warband mods)

First of a kind master server for the Mount & Blade: Warband game created with the goal of providing players with on-the-fly notifications regarding any announcements related to cooperative events, multplayer or the overhaul itself, even as they adventure during their campaign.

This requires a dedicated port-forwarded machine to function 24/7 in order to handle logic data of 0 to 1 (which counts how many players are currently playing every few minutes), the master server host also needs to be able to edit files within the machine in order to input data that will output into the user/player machine as a text message for this to work as a proper announcement system instant access to the machine is recommended.

In addition, unlimited reach to players with no need to re-compile any form of code between messages, and an automated approach for gathering data from dedicated servers to output them to players.

# Download

| Source | Link | Status |
|---|---|---|
| Download from github | [Master Server releases](https://github.com/faycalki/master-server-warband/releases) | [![Github All Releases](https://img.shields.io/github/downloads/faycalki/master-server-warband/total.svg)](https://github.com/faycalki/master-server-warband/releases) |


### The formulae (Input/output structure)
* Logic output value of 1 from player to master server --> countplayers.php --> data.txt (add 1 to player count in data.txt, feeds the player counter by sending request to servertld. countplayers.php)

* Compiled code in player game requests data from server every 5 minutes (adjustable) by sending request --> mrv.txt

* mrv.txt (if new announcement message exists, send output data to player) -->  play message at player machine.

* (OPTIONAL for automatic faction/map data) mrv.txt of the master server is fed data through dedicated game servers by requesting data from the following destination: http://domain.tld/filename.php?var1=|450|11|strings

* data2.txt & filename.php assist data.txt by bypassing edit errors/ensuring that a backup is available.

## Pre-requisites
Port forwarded dedicated machine with SSH/Remote access.
Python 2.75 to 2.0, any higher or lower will not compile the code correctly.
Note: HTTP access needs to be granted at port 80 at the very minimum.

## Developing
Unfortunately Python 3 is not supported by the warband module system, so you'll have to install Python 2.7 in order to further develop this project, here are some steps to install Python 2.7 easily, but any other method would work as long as the version between 2 to 2.8 of Python.
First, git clone the repository for the latest source code, then run the commands below to install Python 2.7.16.

```shell
sudo apt-get update
sudo apt-get install build-essential checkinstall
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev
cd /usr/src
sudo tar xzf Python-2.7.16.tgz
sudo wget https://www.python.org/ftp/python/2.7.16/Python-2.7.16.tgz
cd Python-2.7.16
sudo ./configure --enable-optimizations
sudo make altinstall
```

### Setting up everything

1. After installing Python, obtain the latest build files from the Release section in the github repository, the mcnotify folder needs to be created within your website.com/ directory, so it'd look like website.com/mcnotify/ with the files being right at that directory.
2. Adjust the export directory within module_info.py to the game's full module folder (the one you wish to implement the master server in)
3. Insert the code found in the src folder to each corresponding file of the module you wish to implement the announcement system in, so module_scripts code goes to your module_scripts file, and so on for the rest of the files, remember you will need to insert your website (in IP form since warband does not support DNS lookups) for the announcement service to work, the code should be self explanatory on these steps, once the website IP is inputted correctly, continue to the next step.
4. Run build_module.bat and wait for the compilation to finish.
5. Once the compilation finishes successfully, attempt to launch the project within the game Mount & Blade: Warband's by switching the Module from "Native" to the project's name.
6. Play and enjoy your new changes.

### Deploying / Publishing
mrv.txt requires chmod 755
The rest of the files in the directory require chmod 777.

Due to limitations with the warband engine such permissions need to be granted for an outside machine to input the amount of players currently playing the game, I suggest running an .htaccess that completely blocks any outside user from seeing any of the files or scrapping them.

## Features

Currently, the announcement service can provide the following functionalities.
* Provide any custom message at will to every player without them needing to update the game or for you to re-compile any code, simply edit the mrv.txt with your message and it'll output the message once to every player currently online within a few minutes.
* The mrv.txt is also capable of providing coloured messages, gathering data from dedicated game servers to provide the player with information such as the current map ongoing for the event, the current players in the server as well as the factions without any further input from the host.
* Gathers minimal data from players (only a logic check of 0,1 every few minutes to check if player is active and +1 the count for the master server of amount of players active) and the players are completely secure from any form of exploit or security vulnerability due to the code for the user only being able to accept output in message string, thus no code outside a simply announcement message can be executed in the users machine, and their privacy remains secure, too.

## Links

Even though this information can be found inside the project on machine-readable
format like in a .json file, it's good to include a summary of most useful
links to humans using your project. You can include links like:

- Project homepage & Repository: https://github.com/faycalki/master-server-warband
- Issue tracker: https://github.com/faycalki/master-server-warband/issues
  - In case of sensitive bugs like security vulnerabilities, please contact me as soon as possible.
  - My other projects: https://github.com/faycalki/



## Licensing

This announcement service is licensed under MIT, feel free to use it.
