---
title: "How to restore a snapshot"
lang: en
ref: restsnapshots
menuitem: Snapshot's restoring guide
category: help
layout: page
permalink: /restore-snapshots/
priority: 11
---

***Disclamer: This guide offers no guaranty whatesoever that you won't lose your data or damage your equipement by following it. Use these instructions on your own risk and only if you are more than 100% sure you know what you are doing. The responsibility for whatever possible issue or damage in any case is intirely yours. Proceed only if you agree with this disclamer.***

<br/><br/>
These are general instructions for Linux users. If you are using Windows or Mac feel free to modify these instructions according to your needs if you know how to, and don't hesitate to create a pull request or share your improvements by publishing an issue on Github
(<a href="https://github.com/slimcoin-project/slimcoin-project.github.io/issues" target="_blank">here</a>) to help the others.
If you find an error please submit your correction as well.

## Backup your data
This step is needed only if you have already used slimcoin so far, i.e. you have a ~/.slimcoin folder on your machine.

Move your slimcoin folder elsewhere to protect your existing data and above all your wallet's keys (i.e. your coins) from any accidental loss:

    mv ~/.slimcoin ~/.slimcoin_backup

## Create a new slimcoin folder
Make a new .slimcoin folder where you'll put your snapshot data later on:

    mkdir ~/.slimcoin

## Unzip your snapshot file
Assuming your snapshot file is in your home directory unzip its content into ~/.slimcoin folder using the following command:

    unzip -d ~/.slimcoin/ ~/slimcoin_snapshot.zip

## Copy your wallet into the new folder
In case you've already used slimcoin before and got some coins on your wallet you should copy your wallet.dat file from the previosly created backup into the new slimcoin folder:

    cp ~/.slimcoin_backup/wallet.dat ~/.slimcoin


## Copy or create your slimcoin configuration file:
If it's not the first time you are using slimcoin client on your machine copy your configuration file slimcoin.conf from backup:

    cp ~/.slimcoin_backup/slimcoin.conf ~/.slimcoin

Otherwise create your configuration:

    echo "reservebalance=0" >> ~/.slimcoin/slimcoin.conf
    echo "rpcuser=YOUR_USERNAME" >> ~/.slimcoin/slimcoin.conf
    echo "rpcpassword=YOUR_PASSWORD" >> ~/.slimcoin/slimcoin.conf
    echo "rpcallowip=127.0.0.1" >> ~/.slimcoin/slimcoin.conf
    echo "addnode=109.245.199.123" >> ~/.slimcoin/slimcoin.conf
    echo "addnode=109.93.201.218" >> ~/.slimcoin/slimcoin.conf
    echo "addnode=185.150.190.19" >> ~/.slimcoin/slimcoin.conf
    echo "port=41682" >> ~/.slimcoin/slimcoin.conf
    
(you should change YOUR_USERNAME and YOUR_PASSWORD values in your ~/.slimcoin/slimcoin.conf file)

## Launch your client
To use your new blockchain data and to additionally syncronise it you may want to launch your local client:

    /LOCATION/OF/YOUR/CLIENT/./slimcoind

or

    /LOCATION/OF/YOUR/CLIENT/./slimcoin-qt

(the value of /LOCATION/OF/YOUR/CLIENT/ above depends on where your client is located)

## Note
You may want to keep your ~/.slimcoin_backup folder in case you discover later on that it contains something you still need.
