---
author: Mehedi Hasan
title: Things to Do After Installing Ubuntu 22.04
date: 2022-09-18
description: Configure Ubuntu 22.04 (Jammy Jellyfish) on your computer.
categories:
  - Linux
tags:
  - post-installation
  - ubuntu
  - gnome
image: ubuntu-22.04.jpg
---

<!-- cspell:words Mehedi Hasan apport dconf dpkg gufw libdvdcss libdvd-pkg libfuse2 rhythmbox touchpad userspace zram -->

Ubuntu is well configured out of the box.
But there are a few things you can do to enhance your experience.
In this article we will look at what to do after installing the latest version of Ubuntu.

## To-Do

### Update the System

After installing Ubuntu, you should update it as soon as possible.
Linux operates on a local database of available packages, which must be synced before you can install any software.

To upgrade your system, open the terminal by pressing `Ctrl + Alt + T` and execute the following commands:

```shell
sudo apt update
sudo apt upgrade
```

### Install Restricted Formats

Due to patent and copyright restrictions, Ubuntu does not ship non-free formats by default.
Certain media formats would not be supported by Ubuntu if Restricted Formats are not installed.
If you use Microsoft Office files, the absence of Microsoft typefaces may probably present you with problems.

If you are using regular, stock Ubuntu, you can install them by entering the following in a terminal:

```shell
sudo apt install ubuntu-restricted-extras
```

Additionally, in order to play encrypted DVDs, you need to install libdvdcss.

```shell
sudo apt install libdvd-pkg
sudo dpkg-reconfigure libdvd-pkg
```

### Install Drivers

The open-source drivers included with Ubuntu perform as expected.
However, if proprietary drivers provide your system better performance, you might still wish to install them.
It is rather easy to do so.

Open App Grid > Click on **Additional Drivers** > Select Recommended Drivers > **Apply Changes**.

Note that you need to wait while it searches for the drivers.

### Set up Firewall

It is advisable to enable a firewall that protects against network intrusions.
I recommend you install [Gufw](https://gufw.org/) as it is one of the easiest firewalls for Linux.

```shell
sudo apt install gufw
```

After the installation, open Gufw from the App Grid, authenticate, and then enable the firewall.

### Enable ZRAM

ZRAM is a kernel module that provides a compressed block device in RAM and thus holding much more information in the RAM.
ZRAM could improve responsiveness in case a system often falls back to swap.

The easiest way to enable ZRAM on Ubuntu is to install the [systemd-zram-generator](https://github.com/systemd/zram-generator) package.

```shell
sudo apt install systemd-zram-generator
```

You may need to reboot your system for the ZRAM devices to show up.

### Change Swappiness

The swappiness sysctl parameter represents the kernel's preference for swap space.
Lower values ​​mean the kernel will try to avoid swapping, while higher values ​​will cause the kernel to aggressively try to use swap space.

Check the current swappiness value by running the command `sysctl vm.swappiness` in a terminal.

To set the swappiness value permanently,
create a sysctl.d configuration file. For example:

```shell
sudo touch /etc/sysctl.d/local.conf
printf '%s\n' 'vm.swappiness=10' | sudo tee /etc/sysctl.d/local.conf
```

Reboot and check the swappiness value again.
It should be set to 10 now.

### Add Support for Password Protected Archives

The default archive manager uses `unzip` as a backend to extract zip archives, which does not support password-protection.
There is a different backend named `p7zip-full` that offers extra functionality, including support for password-protected archives.
After installation, the Archive Manager will switch to using this backend.

You can install it from the terminal by the following command:

```shell
sudo apt install p7zip-full
```

### Enhance AppImage Support

AppImage applications do not run in Ubuntu 22.04 despite having the correct file permissions.
The reason for that most AppImages are still using version 2 of the FUSE file system, whereas Ubuntu 22.04 includes version 3.
It would not be a problem once AppImages upgrades to the latest version of the FUSE file system.

In the meantime, you can install FUSE 2 alongside FUSE 3 to deal with this inconvenience.

```shell
sudo apt install libfuse2
```

### Install dconf Editor

dconf Editor is a graphical viewer and editor of applications’ internal settings.
In other words, the dconf Editor can view and edit settings that are not generally exposed through the GUI.

You can install it by using this command:

```shell
sudo apt install dconf-editor
```

### Enable Minimize on Dock Click

It is unpleasant that an open app window in Ubuntu 22.04 cannot be minimized by clicking the app's icon on the Dock.
This behavior can be changed easily with the help of dconf Editor.

Open App Grid > Click on **dconf Editor** > Navigate to `/org/gnome/shell/extensions/dash-to-doc/click-action` > Disable **Use default value** > Select `'minimize'` from the **Custom value**.

### Change Appearance

Ubuntu 22.04 features two styles: Light and Dark.

Choose the one you like from **Settings** > **Appearance** and pick a **Color** to give your system a personal touch.

You may also choose the size of the app icons on the dock and where on the screen the dock appears, as well as enable Panel mode.

### Tweak Privacy Options

#### File History & Trash

"File History" feature makes it easier for you to find files that you might want to use.
If you do not like the feature, go to **Settings** > **Privacy** > **File History & Trash** and turn it off from the "File History" section.

Trash and temporary files can sometimes include personal or sensitive information.
Automatically deleting them can help to protect your privacy.
I highly recommend you enable this feature.

Go to **Settings** > **Privacy** > **File History & Trash** > Enable **Automatically Delete Trash Content** and **Automatically Delete Temporary Files** from the "Trash & Temporary Files" section.

#### Diagnostics

Newer Ubuntu installations come with Problem Reporting enabled by default.
This feature automatically reports the technical problems to Canonical Ltd. anonymously, in an attempt to make Ubuntu better for everyone.
You can change the behavior of this feature to show a dialog for each error before sending its report to Canonical.
You may also choose to disable this feature altogether.

Go to **Settings** > **Privacy** > **Diagnostics** and then select `Manual` or `Never` from the **Send error reports to Canonical** dropdown menu in the "Problem Reporting" section.

### Tweak Power Settings

Out of the box, Ubuntu automatically suspends the system after 20 minutes of inactivity when running on battery power.
I like being able to suspend the system whenever I choose.
You can also turn off this behavior if you wish.

Go to **Settings** > **Power** > Click on **Automatic Suspend** in the "Power Saving Options" section > Disable Automatic Suspend for both **On Battery Power** and **Plugged In**.

### Displays

You can now customize the scaling of your screen if you have a Hi-DPI one.
Thanks to the feature "Fractional Scaling" introduced in Ubuntu 20.04.
If you see a blank screen, your screen is not capable of supporting the scaling you have chosen, and it will revert to the previous scaling after 15 seconds.

Go to **Settings** > **Displays** > Switch to the **Displays** tab > Enable **Fractional Scaling** and then choose among 100%, 125%, 150%, 175%, and 200%.

Ubuntu has a function called Night Light that lessens the amount of blue light that the display emits.
When activated, this helps in reducing eye strain.

Go to **Settings** > **Displays** > Switch to the **Night Light** tab > Enable **Night Light**.

### Mouse & Touchpad

By default, the left or right mouse button action requires you to press the left or right touchpad button, which is annoying.
Enable the tap to click option and just tap the touchpad anywhere to get the same functionality.

Go to **Settings** > **Mouse & Touchpad** > Enable **Tap to Click** from the "Touchpad" section.

### Configure Keyboard

You can make your keyboard behave like a keyboard with a different layout, regardless of the letters and symbols printed on the keys.
This is useful if you often switch between multiple languages.

Go to **Settings** > **Keyboard** > Click the `+` button in the "Input Sources" section > Select the language which is associated with the layout > Select a layout and press **Add**.

### Set Region & Language

#### Date and Measurement Formats

To conform to regional customs, you can modify the formats used for dates, times, numbers, currencies, and measurement.

Go to **Settings** > **Region & Language** > Click on **Formats** > Select the desired Region & Language > Click **Done**.

Restart the session for the modifications to take effect.

### Choose Default Applications

Ubuntu comes with Rhythmbox preinstalled but for some reason sets "Video" as the default app to open Music files.
Change it to "Rhythmbox" for a better experience listening to music.

Go to **Settings** > **Default Applications** > Choose `Rhythmbox` from the Drop-down list for **Music**.

### Install Extension Manager

Ubuntu employs GNOME as its desktop environment, as you may know.
Thanks to its extensions, GNOME can be completely customized.
While certain extensions are pre-installed, more can be installed with "Extension Manager" app.

Open the terminal and install Extension Manager with the following command:

```shell
sudo apt install gnome-shell-extension-manager
```

### Install Tweaks

Along with the GNOME extensions, GNOME Tweaks is a useful software that aids in personalizing your GNOME desktop.
GNOME Tweaks offers options to install additional themes, adjust fonts, change the location of Windows buttons and a few more.

```shell
sudo apt install gnome-tweaks
```

## Conclusion

You could invest a significant effort in customizing and configuring your system.
It is personal preference that ultimately matters.
Let me know if you find this list helpful.
