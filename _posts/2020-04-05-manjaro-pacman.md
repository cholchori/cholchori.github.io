---
title: manjaro linux pacman
layout: post
date: 2020-04-05
description: 
image: smile.gif
categories: ["IT"]
---

# Overview

Manjaro's package manager, [[Pamac]] ships with most Manjaro editions.  All Manjaro editions include [https://www.archlinux.org/pacman/ pacman], the package manager from upstream Arch Linux.  Pacman includes some advanced features not found in Pamac.

Key points to know:

* Pacman is already installed in Manjaro Linux by default
* Pacman is mainly developed/maintained by Arch Linux developers
* Pacman can only be used from the command line, if you would prefer a graphical package manager please see [[Pamac]] or [[Octopi]]
* Pacman can only use the official Manjaro [[Repositories_and_Servers|repository]]. There are seperate articles available for accessing the [[Arch_User_Repository|Arch User Repository(AUR)]], using [[Flatpak|flatpaks]] and using [[Snaps|snaps]]


# Installing Updates

To update the package database and update all packages on the system
```
 sudo pacman -Syu
```

To force a full refresh of the package database and update all packages on the system. You must do this when [[Switching_Branches|switching branches]] or [[Pacman-mirrors|switching mirrors]].
```
 sudo pacman -Syyu
 ```


To force a full refresh of the package database, update all packages on the system and allow packages to be downgraded.  Downgrading should be only be needed when switching to an older branch.  For example, switching from Testing to Stable.
 sudo pacman -Syyuu


# Searching for Packages

To search the Manjaro repositories for available packages you can use the command {{ic|pacman -Ss keyword}}. It will search both the package name and the description for the keyword.  For example, to search for packages containing the keyword smplayer you could use:
 pacman -Ss smplayer


You can search your installed packages in the same manner using {{ic|-Qs}} instead of {{ic|-Ss}}.  To search your installed packages for smplayer:
 pacman -Qs smplayer


Once you have found a package you can use {{ic|pacman -Qi}} to get more information about an installed packages or {{ic|pacman -Si}} for packages in the repos.  Following the example above you could use
 pacman -Si smplayer


Finally, for a list of all installed packages on your system, enter the following command:
 pacman -Ql


# Installing Packages

{{warning|Never install a package without updating the system first.  On a rolling release this can lead to an unbootable system}}


To install a software package, the basic syntax is {{ic|pacman -S packagename}}.  However, installing a package without updating the system will lead to a partial upgrade situation so all the examples here will use {{ic|pacman -Syu packagename which will install the package and ensure the system is up to date}}.  For example, to sinatll smplayer the command is:
 sudo pacman -Syu smplayer


You will then be presented a list of software to install.  You may notice this list has more packages than you requested. This is because many packages also have dependencies which are packages that must be installed in order for the software you selected to function properly. 


Pacman can also directly install packages from the local system or a location on the internet.  The format of that command is {{ic|pacman -U packagelocation}}.  For example, to install a copy of your package cache you could do something like:
 sudo pacman -U /var/cache/pacman/pkg/smplayer-19.5.0-1-x86_64.pkg.tar.xz

Alternatively, you could get it directly from one of Manjaro's mirrors:
 sudo pacman -U https://mirror.alpix.eu/manjaro/stable/community/x86_64/smplayer-19.5.0-1-x86_64.pkg.tar.xz


{{warning|When using pacman -U it is up to you to ensure that the package you are installing is fully compatible with your system.}}


# Removing Packages

{{warning|Always review the package list before confirming when removing packages.  If you are not careful you can easily remove your entire desktop due to dependencies.}}


To remove a software package, the basic syntax is {{ic|sudo pacman -R packagename}}.  We could remove the smplayer package we installed above with:
 sudo pacman -R smplayer


This will remove the package, but will leave all the dependencies behind.  If you also want to remove the unneeded dependencies you could use {{ic|pacman -Rsu packagename}} as seen in this example:
 sudo pacman -Rsu smplayer


Sometimes when you try to remove a package you will not be able to because there are other packages which depend on it.  You can use {{ic|pacman -Rc packagename}} to remove a package and everything that depends on it.  Be careful to heed the above warning when using this option.
 sudo pacman -Rc smplayer


The most nuclear option is {{ic|pacman -Rcs packagename}}.  This will remove everything that depends on packagename and continue to do so on its dependencies.  This should really only be used in exceptional circumstances such as when removing an entire desktop environment and trying not to leave anything behind.


Pacman usually also creates backup configuration files when deleting packages. To remove those, you can add {{ic|n}} to any of the examples above.  For example:
 sudo pacman -Rn smplayer
 sudo pacman -Rsun smplayer
 sudo pacman -Rcn smplayer


# Viewing and Removing Orphans

To list all ''orphans'', installed packages that are not used by anything else and should no longer be needed:
 pacman -Qdt


To remove all the orphans:
 sudo pacman -Rs $(pacman -Qdtq)


=Downloading Packages without Installing=

In some cases it may be useful to download a package without installing.  For example, to install on a different system that is not connected to the internet.  This can be done with {{ic|pacman -Sw packagename}}.  For example:
 sudo pacman -Sw smplayer


The package and any rerquired dependencies will be downloaded to your pacman cache at {{ic|/var/cache/pacman/pkg}}


# Determining which Package Owns a File

It is often useful to understand which package installed a file on your system.  This is easy to do with pacman using {{ic|pacman -Qo /path/to/filename}}.  For example:
 pacman -Qo /usr/bin/smplayer


# Cleaning the Cache

When pacman installs packages, it keeps a copy of all the old packages you have downloaded. This cache can be very useful if you have to install older packages in an emergency. However, left unchecked, this cache will grow very large over time. Systems running [[Pamac]] will already have access to its automated pacman cache cleaning functions.  It is also possible to clean them manually using pacman.

To clear the cache of packages that are no longer installed, enter the following command:
 sudo pacman -Sc


Otherwise, to clear the cache completely, enter the following command (and use with care):
 sudo pacman -Scc


A safer way to remove old package cache files is to remove all packages except for the latest three package versions using {{ic|paccache}}:
 paccache -rvk3

# The Configuration File, pacman.conf

Pacman's settings are located in {{ic|/etc/pacman.conf}}.  This file is owned by root, please see [[Viewing_and_editing_configuration_files|this guide]] if you need more information on how to edit this file.  A full reference to these options can be found in the Arch Wiki linked below.  This sections features some settings that may be of particular interest to Manjaro users.


{{note|pacman.conf settings are case sensitive}}


## Enabling Color Output

By default, pacman's output is monochrome but enabling colored output can make the output easier to read if your terminal supports colors.  This can be enabled by uncommenting or adding the following line to the file
 Color


## Showing PacMan Eating Power Pills

If you are bored of simply watching lines of hashes while downloading software packages in the terminal, why not change the progress bar to Pacman eating power pills instead?  To enable this, simply add the line:
 ILoveCandy


# Troubleshooting

A separate page for pacman troubleshooting is available '''[[pacman troubleshooting|here]]'''.


# See Also

* [[System Maintenance]]
* [[Pacman-mirrors]]
* [[Pacman troubleshooting]]
* [[Downgrading packages]]
* [https://wiki.archlinux.org/index.php/Pacman ArchWiki: pacman]
* [https://wiki.archlinux.org/index.php/Pacman_tips ArchWiki: pacman tips]
* [https://wiki.archlinux.org/index.php/Improve_pacman_performance ArchWiki: pacman performance]
