---
title: What is Proof of Burn (ELI5)?
lang: en
menuitem: Proof of Burn ELI5
category: technology
ref: eli5
layout: page
permalink: /proof-of-burn-eli5/
priority: 4
---

In this article, we will explain the revolutionary consensus mechanism behind Slimcoin: **Proof of burn**.

*If you need a super-short explanation, you can go to the **[tl;dr](#tldr)** section at the end. Readers that are familiar with Bitcoin's Proof of Work and **why** it works can skip the first two sections.*

### Why a consensus method is necessary?

To understand what is Proof of Burn, first we must understand why cryptocurrencies use a "consensus method".

First, the basics: The blockchain is the **main database** of a cryptocurrency. It contains all valid transactions.

All nodes - all participants that run a full-featured client software - save the blockchain on their hard disks. It's called a "blockchain" because the transactions are grouped in **blocks**. A block is written when the nodes agree to a set of transactions that the nodes regard as valid.

But **how do the nodes agree** which transactions should be saved into a block? There is no central authority that validates the transactions, so this work must be done by the nodes in a collaborative way.

The blockchain technology already prevents that some node could create money out of thin air, because blocks are chained together with cryptographic hashes and only coins that have been legitimately created (e.g. by mining) can be spent. But there could be dishonest nodes that tried to use a coin twice - this is called a **double spend**. For example, they could buy an item in an online shop and inmediately try to send the same coins to an exchange. This way they could fool the shop owner and the exchange owner and get both things - the bought item and the money.

To *prevent double spends*, the nodes must **come to an agreement** which transactions are valid and which are not.

On a first glance, we could let the nodes **vote** for which transactions are included into a block, with each node having one vote. But there is a problem: **A malicious participant could create thousands of nodes** and manipulate the vote.


### Proof of work: Bitcoin's consensus mechanism

So we need a vote mechanism that is not manipulable by creating more nodes.

In Bitcoin and many other cryptocurrencies, a mechanism called **Proof of work** is used. 

We could describe the process the following way: The nodes (*miners*) compete to write a block into the blockchain. To include a block, their computers must first do some *work*: they must **solve a difficult cryptographic puzzle**. The node that first solves it gets the right to write the block, and gets a reward for it to incentive this work. This process is colloquially called **mining**.

If you want to **double spend**, you must have the computing power to **write several blocks in a row**. First you send the transaction to the person you're scamming, pretending to buy something with it. Then you wait until the item is sent to you. But as you can't include both conflicting transactions in the same chain, you would have to mine a private chain with the second transaction (the one that sends the money back to yourself) until you got the item. Then you publish your private chain and hope that other nodes mine on top of it.

For this to happen, the nodes must recognize your chain as the "best" (or "longest") and thus you must have a **lot of computing power**. You can only be sure to write several blocks in a row if you have more than half of the computing power of all nodes of the network (this is the infamous **51% attack**).

That is the way how double-spending attacks are prevented in Bitcoin: because it is prohibitively costly to buy the "mining" power to achieve this.

### Proof of burn: Proof of work without energy waste

The important thing to understand is that the raw computing power is not important to prevent manipulation by double spending. What is important is the **cost** of the computing power. **It must be costly** for an attacker to achieve the power to *mine* several blocks in a row.

So in Proof of work, the right to mine blocks is tied to a monetary cost for the miner. **The more a miner pays** for computing equipment that is able to solve the cryptographic puzzle (*mining rigs*), **the more chances he has** to get the right to mine blocks. 

But what if we can have the same effect in a more direct way?

We can mimic this cost letting the nodes "destroy" or "burn" coins, if they want to get the right to write blocks. **That is the principle behind Proof of Burn**. We call it also **minting**, because no real work is done. Remember: all what's important is the cost of the mechanism.

That sounds crazy. But the brilliant mind that has invented Proof of Burn, Iain Stewart, has provided us an analogy: **Burnt coins are mining rigs!**

That means: The act of *burning coins* can be compared to the act to *buy a mining rig*. In Proof of Burn, every time you burn coins, you **buy a virtual mining rig** that gives you the power to mine blocks. **The more coins you burn, the bigger that virtual mining rig**.

That's exactly how Slimcoin's Proof of Burn mechanism works:

If you burn coins, you **not only** get the right to compete for the next block. A mining rig is something more durable, **and so are Slimcoin's virtual mining rigs**. You burn coins and this rises your chance to get blocks for a long time - **at least for a year**.

Now, **to prevent early adopters from benefitting too much** or attacking the system , the power of burnt coins **decays** every time a block is mined. It doesn't decay much, so don't be afraid - you will have a lot of time. But this also mimics mining: Mining rigs eventually **become obsolete** because there is better technology available. So miners, to stay competitive, will have to renew their equipment sometimes. The same is true for Proof of Burn: if you want to maintain your minting power, you must burn coins periodically.

Like in Proof of Work, the **block rewards are high enough** to allow the participants to make a financial gain (profit) from minting. You won't get back your investment in one hour or one day, but with some patience, in most situations you'll eventually **get significantly more coins that the ones you burnt**.

Proof of burn has the advantage over Proof of Work that it does consume much less energy. So Slimcoin is your coin of choice if you ever have worried about Bitcoin's environmental cost. But Proof of Burn has also advantages over Proof of Stake, another consensus method that minimizes energy use. We will cover this point in a later post.

In Slimcoin, we combine Proof of Burn with Proof of Stake and Proof of Work. The reason is mainly security: Proof of Burn and Proof of Stake alone have some weaknesses, but the mandatory presence of some Proof of Work blocks helps to prevent the exploitation of them.

### tldr

**Proof of burn works like virtual mining: You buy a virtual mining rig if you burn coins. The more coins you burn, the more powerful the mining rig. Every virtual mining rig gives you the right to mine for a long time, just like real mining rigs. But they eventually lose their power - just like mining rigs that get obsolete because of Moore's law.**
