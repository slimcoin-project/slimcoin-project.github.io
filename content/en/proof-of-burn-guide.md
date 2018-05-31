---
title: Proof of Burn Minting Guide
codeType: guide
lang: en
menuitem: Burning guide
category: help
ref: pobguide
layout: page
permalink: /proof-of-burn-guide/
priority: 3
---

**Burning** is the distinctive feature of Slimcoin. Here you find a guide how to earn Slimcoins by burning.

### How it works

You destroy a part of your coins sending them to an unspendable address, the **burn address**, using a special command. When the system detects that you burnt coins, your address gets a **score** called **Effective Burnt Coins** that determines your chance to find blocks. This score is higher if you burnt more coins.

Don't be afraid to burn too few coins - you can always rise your score burning more coins from the same address.

While burning, you not only can get rewards but also help regulating the money supply. [Learn more about Proof of Burn](/proof-of-burn-eli5/) in our simple explanation.

**Note**: The *Effective Burnt Coins* score decreases ("decays") a little bit every block to avoid attacks by early adopters and to mimic the aging of mining equipment, but the score is positive for over one year for every coin you burnt. So you have plenty of time to benefit from your burnt coins.

### Requirements

You need a Slimcoin client (graphical client or daemon) and some Slimcoins. That's all! No mining equipment or other hardware is required.

To have chances to find blocks regularly, you should burn at least 100, or better 1000 Slimcoins.

**Important**: If you wallet is encrypted, you must unlock it to be able to mint. In the graphical client, you should use the following command in the console (*Help* -> *Debug window* -> *Console* tab):

```walletpassphrase PASSPHRASE TIME```

In the daemon, you unlock it with the following RPC command:

```slimcoind walletpassphrase PASSPHRASE TIME```

PASSPHRASE being your passphrase and TIME the time it should be unlocked (in seconds). If you want to unlock it indeterminately simply choose a large number, e.g. 999999999.

### Burning with the graphical client

In the graphical client, a graphical item called **Burn Coins** is provided which makes it very easy to burn coins. It is accessible from the main window or via the **Tools** menu.

Simply **enter the amount** you want to burn in the window that appears and click OK. Wait until the burnt coint have matured and then you will receive rewards every time you find a block.

**Note**. Burning normally costs a transaction fee of 0.01 Slimcoins per kilobyte, like all transactions. Sometimes, if the transaction is very large because you use many inputs, the client will tell you that he will add a higher fee for this transaction.

### Burning with the daemon

With the daemon it's also very easy to burn.

Simply type the following command in the terminal:

```slimcoind burncoins AMOUNT```

being AMOUNT the amount in entire Slimcoins. (You also can use this command in the Debug console in the graphical client).


### Get information about burning

With the following command you get some basic information about the state of the Proof of Burn system:

```slimcoind getburndata```

You get the following indicators:

* **Net Burnt Coins** is the total amount of coins you have burnt.
* **Effective Burnt Coins** is your score: it is the number of coins you burnt minus the decayed burnt coins.
* **Inmature Burnt Coins** are coins you burnt but still haven't matured. The maturing period is XX blocks.
* **Decayed Burnt Coins** is the amount of coins being deducted from your score (see above) to avoid early adopter attacks and make burning fairer.

* **Formatted nEffectiveBurnCoins** is the sum of the "Effective Burnt Coins" score of all acounts together. It is a rough measure to calculate the amount of coins you have to burn if you want to find blocks regularly: the higher this value, the higher the amount of coins you should burn.
* **nEffectiveBurnCoins** is another way to display the Effective Burnt coins score.
* **nBurnBits** is a technical term referring to the *burn hash target* stored in the current block (for details, see the Whitepaper).
* **General info** is probably not being used actually.

### How many coins have been burnt until today?

You could think the *Formatted nEffectiveBurnCoins* number is what you need, but it is not - because this number does not contain the *Decayed Burnt Coins* and is probably much smaller.

To see the real number you must check the **burn address**. In the built-in block explorer of the client or any other block explorer 
eg. [Bchain.info](https://bchain.info/SLM/), enter the following address:

**SfSLMCoinMainNetworkBurnAddr1DeTK5**

In May 2018, the address had roughly a balance of 2,75 million Slimcoins; at that time that were about 14,66% of the total supply of 18,75 million.
