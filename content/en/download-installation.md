---
title: Download & Installation
codeType: analysis
lang: en
ref: installation
menuitem: Installation guide
category: help
layout: page
permalink: /installation/
priority: 1
---

There are several methods to install Slimcoin. Slimcoin works with Windows, Linux and Mac OS X.

## Download
### Executables (Windows and Mac OS)

You can download the current release on [the Releases page](https://github.com/slimcoin-project/Slimcoin/releases).

Unpack it and place it into a folder of your choice where you can start it. Then continue reading in the *Basic Setup* section below.

### Source code (releases)

Download the current release on [the Releases page](https://github.com/slimcoin-project/Slimcoin/releases).

Unpack the source code into a folder (name it *Slimcoin* for convenience), open a terminal and *cd* into it.

#### Compiling

Compiling is usually straightforward if you have the dependencies installed. Check the current dependencies in the README file. Note that you must also install the development packages.

For the graphical client, type:

```
qmake
make
```

If you only want to compile the daemon: In the *src* subfolder there are several makefiles especially set up for your system (e.g. *makefile.unix*). Check the makefile you need and then type:

```
cd src
make -f YOUR_MAKEFILE
```

After successful compilation, the executable (*slimcoin-qt*) of the graphical client will be available in the base folder, while the daemon executable will live in the *src* subfolder. You can move them anywhere where you want.


### Source code (git, experimental)

You will need the *git* version management system for this method to work.

Simply clone the Slimcoin repository into a folder of your choice:

```
git clone https://github.com/slimcoin-project/Slimcoin.git
```

This will create a subfolder called *Slimcoin*. Change to it:

```
cd Slimcoin
```

By default, the code will be on the *slimcoin* branch, which is stable but not bleeding-edge. If you want the latest, bleeding-edge code you must change to the *master* branch:

```
git checkout master
```

Then compile Slimcoin like indicated above.

## Basic setup

For a basic setup, you first need to know that Slimcoin stores all data (blockchain, wallet, logs and configuration file) in a folder called the **datadir**.

The default location is:

* **Windows:** `C:\Users\YOUR_USERNAME\Appdata\Roaming\Slimcoin` (Windows Vista/7 and later)
* **Linux/Unix:** `/home/YOUR_USERNAME/.slimcoin` or simply `~/.slimcoin`
* **Mac OS:** `~/Library/Application Support/Slimcoin/`

**Note:** Under Windows, to access your datadir fast, simply open the *Run* item at the start menu and type in the following: `%APPDATA%/Slimcoin`

In this datadir it is advisable to create a configuration file named **slimcoin.conf**. You can set there most of the command line options the Slimcoin client offers (see below). Simply create the file with your preferred text editor.

If you want to use the daemon/CLI program *slimcoind*, the configuration file is **mandatory** because here your username and password will be set. Create the file

```
rpcuser=USERNAME
rpcpassword=PASSWORD
```

Put the following line into it if you want to use it as a daemon (running in the background) by default:

```
daemon=1
```

## Starting Slimcoin

Well, you are now ready to start Slimcoin:

* For the graphical client, simply go to the folder where you put it, double click on the executable or start it with **slimcoin-qt** in a terminal.
* For the daemon, type in **slimcoind**.

You will find command line options typing in **slimcoind --help** or **slimcoin-qt --help**. They are mostly similar to the options Bitcoin offers. A reference is here: [Bitcoin command line options guide](https://en.bitcoin.it/wiki/Running_Bitcoin). Note that not all Bitcoin commands are available on Slimcoin, but the ones that are available will mostly work in the expected way.
