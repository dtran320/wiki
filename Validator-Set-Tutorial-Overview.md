---
title: Validator Set Tutorial Overview
---

This tutorial will walk you though the set up of a Private blockchain using [Aura](Aura) consensus mechanism and a dynamic validator set contract.

No previous knowledge of Parity Ethereum or Aura is required.

Aura (for Authority Round) is a Proof of Authority (PoA) consensus mechanism that lets a defined set of authorities seal blocks in a round robbin fashion. The term validator is also used in lieu of authority node. Unlike proof of work (PoW) based consensus mechanism, PoA based consensus makes sense for private consortium blockchains or networks using on a currency without value such as test networks where there is no incentive for miners to spend money in mining. Kovan testnet is running on Aura.  
There are different ways to define the set of authorities in the [chain specification file](Pluggable-Consensus#aura). The easiest way is to use a fixed list of authorities. Any change in this list requires a hardfork, and thus an off-chain synchronisation between the parties running authority nodes. Kovan network historically ran with a fixed list of authorities.

If a fixed list might be sufficient for simple networks, there is no easy way to add or remove validators or strong incentive for authorities to maintain their node. Using a contract however allows to dynamically add or remove authorities as well as monitor bad behaving authorites. This Tutorial will show the setup of a network using a fixed list of validators at its start and then move to an on-chain smart contract to manage the validator set. Finally, we will monitor authorities to spot the misbehaving validators.

The overall setup looks as follow:

- 2 authority accounts (`Node0` and `Node1`) 
- 1 standard account receiving RPC requests (`Alice`)

## Table of contents:




|[ Part 1 - Configuring each node → ](Validator-Set-Tutorial-1.md)|


