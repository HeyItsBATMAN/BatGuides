# How to install Warframe and DXVK manually on Linux

1. Get out of Wine Dependency hell
https://www.gloriouseggroll.tv/how-to-get-out-of-wine-dependency-hell/

2. Get a copy of GlriousEggrolls Warframe Linux installer repository
Option A: Cloning the repository
```
# replace /path/to/GitRepos with the actual path to where you want to clone the repository
cd /path/to/GitRepos
# clone the repository
git clone https://gitlab.com/GloriousEggroll/warframe-linux.git
# change directory into the cloned repository
cd warframe-linux
```

Option B: Download the latest version of the installer without git
```
# replace /path/to/installer with the path where you want to download and extract the installer
cd /path/to/installer
# download the installer
wget https://gitlab.com/GloriousEggroll/warframe-linux/-/archive/master/warframe-linux-master.tar.gz
# extract the installer
tar xfz warframe-linux-master.tar.gz
# change directory into the extracted installer
cd warframe-linux-master
```

3. Make the installer executable
```
chmod a+x ./install.sh
```

4. Run the installer
This will configure a Warframe WinePrefix install the updater script to that directory

Option A (default): Install the game to $HOME/Games/Warframe
```
./install.sh
```

Option B (configuration): 
```
# Set any wine variables you want to set

# usually doesn't need to be changed
export WINE="/path/to/wine"
# usually doesn't need to be changed
export WINEARCH="win32"
# only if you don't want wine to output any messages at all (can help performance)
export WINEDEBUG=-all

# Run the installer with a specific game installation directory
./install.sh '/path/to/game/directory/Warframe'
```

During installation the installer will ask you if you want to add warframe to your PATH
If you answer yes during this step, you can launch warframe from any location in shell by just typing 'warframe'

It will also ask you if you want to add a menu and desktop shortcut.
Press yes if you want them

After installation you can remove the cloned repository folder or the extracted installer, depending on which one you chose

5. Install DXVK
Before you install DXVK make sure that you got the latest drivers you need.
Depending on your linux distribution, you might not have access to them via your repositories.
See the DXVK wiki for information on what latest drivers are needed:
https://github.com/doitsujin/dxvk/wiki/Driver-support
If you do not have the latest driver, either see if your system can upgrade to the latest driver or download an earlier version of DXVK that is compatible with your driver version.

Option A: Installing the latest DXVK release version (easy)
Go to https://github.com/doitsujin/dxvk/releases and download the .tar.gz of the latest release
```
cd /path/do/download/dir
# Replace this link with the link to the latest version
wget https://github.com/doitsujin/dxvk/releases/download/v0.70/dxvk-0.70.tar.gz
tar xfz dxvk-0.70.tar.gz
# Change directory into the extracted dxvk dir
cd dxvk-0.70
# DXVK 0.70 and later will install using a winetricks script
# run the DXVK setup with winetricks
# make sure you're running in the correct WinePrefix (same as the directory you put as argument for install.sh)
export WINEPREFIX=/path/to/Warframe/WinePrefix
winetricks setup_dxvk.verb

# !!! IMPORTANT !!!
# if you've got a version of DXVK earlier than 0.70 you will instead have to
# change directory into the x32 or x64 subfolder (usually x64)
cd x64
chmod a+x ./setup_dxvk.sh
export WINEPREFIX=/path/to/Warframe/WinePrefix
./setup_dxvk.sh
```

Option B: Compile DXVK from source (medium)
Maybe coming soon


6. Run the updater
Depending on your internet connection bandwidth and harddrive speed this step could be really quick or take all day
Take necessary steps to make sure the game and all it's dependencies can download without interruption

Option A (if you pressed yes when it asked if Warframe should be put into PATH):
Open a Terminal and type
```
warframe
```
The game should update and start after the update
You can do this anytime you want to start the game

Option B (if you didn't add to path):
```
cd /path/of/Warframe/Prefix/drive_c/Program\ Files/Warframe/
./warframe.sh
```
Start this file if you want to run warframe

7. (Optional) additional optimizations:
Coming Soon, but basically edit other Environment variables in the warframe.sh and/or the updater.sh

8. (Optional) add the manually installed Warframe to Lutris
Coming Soon