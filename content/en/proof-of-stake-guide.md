---
title: Proof of Stake Minting Guidec
codeType: guide
lang: en
menuitem: Staking guide
ref: posguide
category: help
layout: page
permalink: /proof-of-stake-guide/
priority: 4
---

**Proof of Stake** (PoS) is a method to generate blocks Slimcoin inherited from Peercoin. In short: The more coins you have, the higher chance you get to find a block.

Block rewards are significantly lower in PoS than in PoW and PoB and they depend on the amount of Slimcoins you use to stake, although they are higher than in Peercoin. But on the other hand, PoS is basically risk-less income if your computer is secured and not compromised. And you contribute to the security of the system.

### Requirements

To mint coins via Proof of Stake, you need a relatively high amount of Slimcoins. 200-300 Slimcoins may be enough, but it's more secure if you try with about 1000 to 2000.

The coins must have not been moved for at least 7 days to qualify for Proof of Stake minting. If you move the coins, you will have to wait 7 days again. The weight of the staked coins rises until day 90, and then stays on the same level (a security measure to avoid certain attacks). 

**Important**: If you wallet is encrypted, you must unlock it to be able to mint (like in Proof of Burn minting). In the graphical client you find the *Unlock wallet* item in the *File* menu. In the graphical client, you should use the following command in the console (*Help* -> *Debug window* -> *Console* tab):

```walletpassphrase PASSPHRASE TIME true```

PASSPHRASE being your passphrase and TIME the time it should be unlocked (in seconds). The "1" means that the unlocking won't enable you to make transactions without entering the passphrase. If you want to unlock it indeterminately simply choose a large number, e.g. 999999999.

In the daemon, it is the same command, only you must add *slimcoind* before it.

### What must I do to mint?

**You have to do nothing!** Simply stay online with the client and the wallet unlocked, and you will eventually find a Proof of Stake block if you have enough mature coins in your wallet.

Your coins work for you automatically, like in some parts of the financial world :)

### The reserve balance (important!)

When you find a block, your staking coins will be frozen for some blocks to prevent certain kinds of attacks. During that time, you cannot do transactions with these staking coins.

To avoid this lock, you can set the so-called **reserve balance**. This is an amount of coins that won't be frozen if you find a block. But on the other hand it won't participate in "staking".

The reserve balance can be set in the graphical client in the **Options** window in the **Settings** menu.

To permanently set a reserve balance, also if using the Slimcoin daemon (slimcoind), edit the **slimcoin.conf** configuration file and add:

```reservebalance=NUMBER_OF_COINS```

If reservebalance is set to 0, then you will stake with all coins.

### CPU and memory usage

Proof of Stake, in Slimcoin, requires a relative high amount of memory and CPU resources. The amount of resources depends on the number of inputs that are used to stake. The more inputs you have in your wallet, the more resources are needed ([Source](https://bitcointalk.org/index.php?topic=1141676.msg19085405#msg19085405)).

**Note**: The number of inputs is related to the number of transactions you received. In short: normally, for every transaction you received, your wallet will contain one input. The more transactions you receive, the more inputs your wallet will have to manage.

Because of this issue, if the computer or server you use to mint is older or low on resources, it's a good idea to *not* use the same wallet for Proof of Burn minting or Proof of Work mining and for Proof of Stake minting. Mining and PoB minting produce a continuous stream of new inputs that then will consume increasingly more resources when you mint by Proof of Stake.

It is advisable that you *clean* your wallet before you start to mint if you have a large amount of inputs. For this purpose, simply make a single transaction to one of your wallet addresses including all coins in the wallet. So you will have all your balance concentrated in one single input.
