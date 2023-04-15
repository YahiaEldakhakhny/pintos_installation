# Pintos Installation script
This script mainly follows the [installation instructions](https://github.com/YahiaEldakhakhny/CSEx61-pintos/blob/main/Installation.md)
but still it differs from the original instructions in a manner that is optimized for our team

## Differences Between This Script and The Official Instructions
* The script is configured to exit immediately if any error occurs.
* When the script starts a section of the installation it prints the name of the step on the terminal in a unique color (probably red if your terminal uses the default colors).
This is done to make debugging easier so if an error occurs in a certain step, you can start where the script stopped, so there is no need to start from scratch.
* Git is the first thing to be installed.
* When cloning the pintos repo, I clone a ***Fork*** that is dedicated for our team
```
git clone https://github.com/YahiaEldakhakhny/CSEx61-pintos.git
```
* When exporting pintos path to bashrc, I added single quotes because if the path variable contains white spaces, they will cause errors when trying to load the bashrc

The command I used:
```
echo "export PATH='$PINTOSHOME/src/utils:$PATH'" >> ~/.bashrc
```
The command used in the official instructions:
```
echo "export PATH=$PINTOSHOME/src/utils:$PATH" >> ~/.bashrc
```

## Script Limitations
The last step in the script is:
```
echo "export PATH=~/pintos/src/utils:$PATH" >> ~/.bashrc
```
After performing this step, the script exits, and you are supposed to reload your bashrc manually and follow the rest of the official instructions
starting from:
```
source ~/.bashrc
```
Just before the script exits, it prints the $PINTOSHOME environment variable so you can copy it and reuse it wherever needed

## Recommendations
* Run the script from your home directory (makes it easier to find the pintos directory if you need to find it manually later on).
* If you are using a ***Virtual Machine*** clone the machine before trying to install pintos (whether manually or using the script).
This creates a backup copy of the machine that you can use in case sothing wrong happens.
To clone a machine make sure that it is powered off and then right click it, you should see the option `clone`.


# Track script
`track` is a script we can use to track a specific file from pintos and add it to the shared git repo

## Make the script ready to use
* Clone this repo if you don't have it already
```
git clone https://github.com/YahiaEldakhakhny/pintos_installation.git
```
* If you already have the repo cloned locally just pull the latest changes
```
git pull origin
```
***Make sure you cd into this repo before executing the following commands***
* Make sure that the track script is executable
```
chmod +x track
```
* Make a global link to the script to make the script usable from any directory
```
ln -s track /bin/track
```

## How to use the script
Say you want to add the file `threads.c` to the list of files tracked by the shared repo and the path of the shared repo on your machine is `/home/username/shared_repo` then you can track the file using this command:
```
track threads.c /home/username/shared_repo
