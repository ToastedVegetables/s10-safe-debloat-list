# A beginner's guide to debloating your Galaxy S10 *safely* using ADB commands
[![License](https://img.shields.io/badge/license-MIT-green)](./LICENSE)
##### Contributions, issues, and feature requests are welcome!
##### Give a star if you like this project!

This repository is meant for beginners and contains the steps and scripts necessary to remove bloat apps from your Galaxy S10.
The goal of this repository is to be beginner-friendly, by providing a list of apps that are **safe** to remove from your device, and by telling you what each app does. Many other guides don't tell you any of this information, leaving you to research it yourself, or, even worse-- just removing the app without knowing what it does.
If you have experience with ADB and know what you're doing, you can skip right to the [Usage](#usage). Otherwise, I recommend that you read the entirety of this guide, to avoid bricking your phone or doing the process incorrectly.  
Please note, this repository is designed for the Samsung Galaxy S10, and has not been tested with the S10+.  
Disclaimer: I am not responsible for any possible damages or errors that may occur from incorrect usage of the commands listed in this guide. Proceed at your own risk.



## Table of contents:
- [File Locations](#file-locations)
- [Prerequisites](#prerequisites)
- [Installing ADB](#installing-adb)
- [Enabling Developer Options](#enabling-developer-options)
- [Enabling USB Debugging](#enabling-usb-debugging)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)


## File Locations
- AT&T-specific debloat commands can be found in [AT&T-specific commands](https://github.com/ToastedVegetables/s10-safe-debloat-list/blob/8d76ee8be4cb17c0cf92a5dcc92f6a3cf939d017/AT&T-specific%20commands.txt)
- Package names with an explanation of what each of them are can be found in [Package Explanations](https://github.com/ToastedVegetables/s10-safe-debloat-list/blob/8d76ee8be4cb17c0cf92a5dcc92f6a3cf939d017/Package%20Explanations.txt)
- Raw commands (without AT&T-specific apps) can be found in [S10 Debloat Commands](https://github.com/ToastedVegetables/s10-safe-debloat-list/blob/8d76ee8be4cb17c0cf92a5dcc92f6a3cf939d017/S10%20Debloat%20Commands.txt)


## Prerequisites
- ADB installed on your computer
- Developer Options enabled on your S10
- USB debugging enabled on your S10

## Installing ADB
1. [Download](https://developer.android.com/studio/releases/platform-tools) the Android SDK Platform Tools ZIP file for Windows
   - Note: the download is a .zip file, ~12MB compressed, ~35MB uncompressed
2. Extract the contents of the .zip file to an easily accessible directory (I used `C:\`, but feel free to use any directory)
3. Open the `platform-tools` folder that should've been automatically created when you unzipped the .zip file
   - Note: if you created a folder with a different name and extracted the contents of the .zip file to it, you should open that folder
4. While holding Shift, right-click any blank space in the folder
5. Press "Open CMD/PowerShell window here"
6. Test that you have ADB installed properly by using the command `adb --version` (you might need to use a `.\` in front of the command to let it run in PowerShell, to bypass this please add adb.exe to your PATH- see [removing PowerShell requirement that scripts and executables be preceded by \.\\](https://stackoverflow.com/questions/9792897/how-do-you-remove-the-powershell-requirement-that-scripts-and-executables-be-pre))
7. If you get an output similar to this, you're good to go:
```
Android Debug Bridge version 1.0.41
Version 31.0.2-7242960
Installed as C:\platform-tools\adb.exe
```

## Enabling Developer Options
1. On your phone, open Settings
2. Scroll down and click on "About Phone"
3. Click on "Software information"
4. Click on "Build number" 7 times in rapid succession, until a popup appears telling you that you've successfully enabled developer options
5. Exit "About phone" and verify that you have a new section of settings after "About phone" titled "Developer options"

## Enabling USB debugging
1. Click on the "Developer options" section in Settings
2. Scroll down until you see a mini-section titled "Debugging"
3. Toggle "USB debugging" on
4. Read the warning and click "OK"

## Usage
1. Make sure that your S10 has USB debugging turned on
2. Make sure your phone is turned on and unlocked, and connect your phone to your computer via USB
3. Open the "platform-tools" folder on your computer, or cd into the directory
4. Run the command `adb devices`
5. If this is your first time, press "OK" on the prompt on your phone to allow USB debugging from your computer
5. You should see the device name listed as a "device", with a serial number prefacing it (if your device is listed as `unauthorized`, make sure you've accepted the prompt on your phone, and re-run the command)
6. Enter the shell using the command `adb shell`
7. Verify that you are in the shell with the command `whoami`, this command should return `shell`
8. Run the appropriate commands in [File Locations](#file-locations) (if you have any carrier other than AT&T, run the commands found in [S10 Debloat Commands](s10-safe-debloat-list/S10%20Debloat%20Commands.txt), otherwise feel free to remove all of the AT&T bloatware from your phone, too! If you want to choose which apps to remove, see [I want to learn more or uninstall specific apps](#i-want-to-learn-more-or-uninstall-specific-apps)

## Troubleshooting

#### ADB is not detecting my phone:
1. Most bad ADB connections are actually caused by bad cables. Make sure that you have a high quality USB-C *data* cable, and not a charging cable. Some charging cables deliver power and transfer data, and these may work, but it's better to use a dedicated USB-C data cable.
2. Try [downloading](https://adb.clockworkmod.com/) and installing the Universal ADB Drivers.
3. The problem may also be caused by a damaged cable or charging port on your phone.
4. There are tons of resources online that cover this issue, try Googling and see what you find!

#### I uninstalled an app on accident, and now I want it back:
1. Don't worry, it's super easy to install previously removed apps. Just run the command `adb shell cmd package install-existing <packagename>`, with `<packagename>` being the name of the package (app) that you want to reinstall.

#### I want to learn more or uninstall specific apps:
1. It's super simple to search for and uninstall specific apps, instead of using my list. To do so, simply run the commands `adb shell pm list packages | findstr ""` with the app/package name in the quotation marks, followed by `pm uninstall -k --user 0 <packagename>`, with `<packagename>` being the aforementioned app's package name.
2. To find an app's package name, you can use an app such as [Package Viewer](https://play.google.com/store/apps/details?id=cz.seeq.prog.android.packageviewer), or reference this *extremely* useful list of all the preinstalled packages on your phone for the [S10](https://docs.samsungknox.com/CCMode/G973U_Q.pdf) or [S10+](https://docs.samsungknox.com/CCMode/G975U1_Q.pdf)
3. There are a ton of interesting projects that use ADB, such as:
  - [ADB AppControl](https://appcontrol.neocities.org/index_en.html)
  - [Apps that require ADB permissions](https://www.makeuseof.com/tag/android-adb-apps/)
  - And tons more online!

Thanks for reading!
