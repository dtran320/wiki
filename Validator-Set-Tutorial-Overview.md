---
title: Validator Set Tutorial Overview
---

This tutorial will walk you though the set up of a Private blockchain using [Aura](Aura) consensus and a dynamic validator set contract.

No previous knowledge of Parity Ethereum or Aura is required.

Aura (for Authority Round) is a Proof of Authority consensus mechanism that lets a defined set of authorities seal blocks in a round robbin fashion. This kind of consensus makes sense for Private consortium blockchains or networks based on a currency without value such as a test network where there would be no incentive for miners to spend money in mining. Kovan testnet is running on Aura.  
There are different ways to define the set of authorities in the [chain specification file](Pluggable-Consensus#aura). For a simple network, a fixed list of authorities can be sufficient. Using a contract however help


The overall setup looks as follow:

- 2 authorities accounts (Node0 and Node1) 
- 1 standard account (Alice)


## Table of contents:




|[ Part 1 - Configuring each node → ](Validator-Set-Tutorial-1.md)|


