---
title: Slimcoin's Advantages
lang: en
ref: advantages
menuitem: Advantages
category: technology
layout: page
permalink: /advantages/
priority: 3
---


### Long-term & stability oriented

Slimcoin's Proof of Burn mechanism encourages **long term involvement**. If you burn coins to participate, you automatically become a long term investor: You probably will get back your investment (and possibly make a profit, like in mining), but not in a short period of time, and you must be connected permanently to the network with a full node to get a decent return.

It is like if you are buying a mining rig that only is working for Slimcoin and you cannot re-use it with other cryptocurrencies.

This feature is what helped Slimcoin to survive even in its worst phase in early 2016 when it was delisted from all exchanges and its client wasn't still very stable.

### Energy efficient

Slimcoin significantly **reduces energy use** with respect to Bitcoin and other pure Proof of Work currencies, because mining is only responsible for between one third and one half of the blocks.

Like in Peercoin, the rewards of Proof of Work blocks are gradually reduced when the difficulty increases. That means that the incentive to produce blocks by burning and staking in relation to mining is increasing over time. So it is expected that energy use will decrease gradually.

### Balanced power structure

Slimcoin's three block generation mechanisms (Proof of Work, Proof of Stake and Proof of Burn) produce three power groups: **miners**, **stakers** and **burners**. Each mechanism is benefitting a distinct group with different incentives.

* **Miners** are often short-term involved, as there are no DCrypt ASICs and so they must mine with generic CPUs and GPUs - they can always change to another cryptocurrency. They work as the **clock** of the consensus mechanism: The protocol favours PoW blocks slighltly over other kinds of blocks, so a Proof of Burn block can only be generated after a Proof of Work block, and several Proof of Stake blocks in a row diminish the chain trust value.
* **Stakers** are overlapping with the user group often called **the economy**. They are participants with large holdings and so they are more long term oriented and interested in the development (and favourable price evolution) of the coin. But they in theory could sell their coins in every moment.
* **Burners** are the most long-term oriented group of all, because they have *"bought virtual mining rigs"* that are only working for Slimcoin and don't get back their investment very fast. They are interested in a stable or rising price. In contrast to stakers, they are rewarded for taking a risk.

These three power groups avoid the power imbalance that is obvious in pure Proof of Work currencies, where miners have a large degree of influence on development decisions (see Bitcoin's Segwit drama for it) and also pure Proof of Stake currencies, where large service providers like exchanges, payment processors and online wallet operators have a large share of the power.

### ASIC unfriendly proof-of-work

It is believed that ASICs are the tool that lead to centralization in most Proof-of-work cryptocurrencies. In Bitcoin, mining is only profitable if you own large ASIC farms.

Slimcoin's DCrypt Proof of work algorithm is ASIC unfriendly, so it's mostly mined by CPUs and GPUs. It is difficult to parallelize. See the Whitepaper for more information.

### PoS 50%+1 attack and Nothing at Stake attack protection

Pure Proof of Stake currencies can be attacked by users that hold a large amount of currency and "mint" with it, creating an attack chain which can be used for double spends. The necessary holdings for an attack are even smaller than 50% of the "staking" coins because of the so-called **Nothing at Stake problem**. In naive implementations, there is an incentive for nodes to mint on every fork that is produced. For attackers that means it's easier to attack the chain with relative low holdings, because they can trick other nodes to mint on an attack chain, until it becomes the "longest" one.

Slimcoin's blockchain inherited the concept of **chain trust** from Peercoin: Chains accumulate trust with the amount of coin-days "used" in Proof of Stake blocks. The chain with most trust is the "longest chain" all honest clients will follow.

However, Slimcoin's chain trust algorithm is more complex than Peercoin's. The trust of a chain decreases if there are two or more PoS blocks in a row. If an attacker wants to reorganize the chain in a malicious way buying a large number of coins and minting on an alternative "attack chain", his attack chain is limited to a longitude of a few blocks because with the first two PoS blocks in a row the trust will diminish. The honest chain, which has normally relatively evenly distributed PoW, PoS and PoB blocks, will rapidly become the longest chain (chain with most trust) again.

Proof of Burn, as it does not consume external resources, is - in principle - also vulnerable to Nothing at Stake-style attacks. But in Slimcoin an attack via Proof of Burn is impossible: Proof of Work works as a *clock* for Proof of Burn, and two Proof of Burn blocks can never be generated in a row without a PoW block between them.

For these reasons, an attack is much more complex than in pure PoS currencies: you actually must be at least a very large miner and staker at the same time to have a realistic chance to find various blocks in a row and be able to convince other nodes that your attack chain is the "longest" one.

Additionally, Slimcoin uses the duplicate stake detection mechanism from Peercoin, which punishes minters who are detected to mint on more than one fork.

### 50%+1-attack protection

On the other hand, the presence of Proof of Burn and Proof of Stake blocks makes it much **more difficult** - if not impossible - to attack the chain via an **50%+1 mining attack**. It is possible to produce various PoW blocks in a row to create an attack chain, but after a certain number without PoS blocks the chain trust diminishes. Honest nodes will then regard the attack chain as "shorter" than the honest chain with a more even PoW/PoS/PoB block distribution.

### Users control the available supply

Proof of Burn **allows users to control the available supply** of the currency. In theory, the nodes could burn every coin that is generated and reduce supply nearly to zero, leaving only the block reward mechanism as available supply.

This flexibility has probably consequences that will be investigated in an academic study. If the **supply follows demand** - like some believe - then it's probable that the price will be more stable. There are several mechanisms that could lead to a higher burning rate when the price per unit is low:

1. One unit is **simply cheaper** when price per unit is low - that should incentive more people to burn, even to simply try it out.
2. If you are long term optimist, in low price phases you can get **more potential future rewards with less investment** (more **RoI** measured in "stable" currencies or goods/services) 
3. When you burn coins, you send a **bullish signal** to the other participants because you openly do a long term investment and everyone is seeing it. So a large burn transaction can lead to buys on the exchange market.
4. When you burn, you openly **retire the coins from the "sellable supply"**. In low price phases users are incentived to do that to limit supply and produce supply deflation, which is also a bullish signal.

If there are more coins burnt in low price phases than in high price phases, then the supply auto-regulates. The users are then acting like a **completely decentralized** central bank, but within strict limits. They cannot create coins out of thin air or elevate supply, they can only reduce it temporarily. So the positive, stability-rewarding effects should outweigh the "supply volatility".
