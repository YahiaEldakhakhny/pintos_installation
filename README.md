# Contents
  1. [Pintos Installation Script](#pintos-installation-script)
  1. [Track Script](#track-script)
  1. [Get Shared Script](#get-shared-script)
  
# Pintos Installation Script
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


# Track Script
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
* Make a global link to the script to make the script usable from any directory (use your local full path of the track script instead of `/home/yahia/pintos_installation/track`)
```
sudo ln -s /home/yahia/pintos_installation/track /bin/track
```

## How to use the script
Say you want to add the file `threads.c` to the list of files tracked by the shared repo and the path of the shared repo on your machine is `/home/username/shared_repo` then you can track the file using this command:
```
track threads.c /home/username/shared_repo
```

# Get Shared Script
Say you pulled the latest changes of the shared repo and someone added a ***new*** file to the shared repo, but now you have two versions of the same file on your machine:
* Version 1: This is the old version and it is located in the original pintos directory
* Version 2: This is the updated one and it is located in the shared repo 

The target now is to remove the old version and replace it with a link that points to the updated version that is located in the shared repo.
This is where you use the `get_shared script`.

## Make the script ready to use
* Just like any other script you can get it by either cloning this whole repo or you can just copy it into a file on your local machine
* Once you have the script in some directory on your machine, cd into that directory and make the script executable
```
chmod +x get_shared
```
* Now make a global link to the script so you can run it from any other directory (use your local full path of the get_shared script instead of `/home/yahia/pintos_installation/get_shared`)
```
sudo ln -s /home/yahia/pintos_installation/get_shared /bin/get_shared
```

## How to use the script
Say someone made changes to the file `threads.c` and added it to the shared repo, now when you pulled the latest changes you found that `threads.c` is now in the shared repo and you want to remove your local old version and make a link to the new version.

Assuming that the old version of  `threads.c` is in `/home/username/pintos_dir`, you need to cd into that directory first
```
cd /home/username/pintos_dir
```
Assuming that the path of the shared repo on your machine is `/home/username/shared_repo`, you can use the script from within `/home/username/pintos_dir`:
```
get_shared threads.c /home/username/shared_repo
```
After running the script, the old version of the file should be replaced with a link to the updated version

### Notice that:
* You provide the file first then the path to the shared repo.
* It does not matter whether you provide only the name of the file or the full path
* You need to provide the full path of the shared repo


