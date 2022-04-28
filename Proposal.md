# Scalable UTXO Commitments

### Abstract

[Abstract]

## Introduction

A Bitcoin-type blockchain is a distributed ledger where transactional data is stored. Nodes use computing power to secure the network and add new transactions to the history. New nodes join the network by querying other nodes until they are in sync, i.e., they have a copy of the longest proof-of-work chain.

In essence, newly joined nodes, or nodes rejoining the network after a period of inactivity, want to obtain the current state of the network, which is, generally speaking, the set of coins or UTXOs that can be spent and the conditions under which they can be used as transaction inputs.

### Data stored by nodes

The information usually stored by nodes is:

- The UTXO set (the state of the network)
- The transaction history (the blockchain), containing:
  - The block headers
  - Newly minted coins (coinbase transactions)
  - Transaction outputs (TXOs):
    - Locking scripts
  - Transaction inputs (TXIs) or Spent Transaction Outputs (STXO):
    - each inputs' sigscript


### Blockchain growth problem

As the time passes and the transactions grow, the amount of information to be stored by each node increases.

At the current maximum capacity of Bitcoin Cash,

If we allow an arbitrarily unlimited number of transactions to enable market-driven on-chain scaling, the maximum amount of information each node can store decreases if the prices of storing and processing such information increase a lot.

### Information required to maintain the network

Nodes only need to keep the state of the network.

### Existing mitigations to blockchain growth

Satoshi proposed a system to minimize the information required to derive the state of the network in section 7 of the whitepaper (**Reclaiming Disk Space**), commonly known as **pruning**.

[Storage price]

[Unlimited bandwidth]

[“Healthy” fee market]


## UTXO commitments

### What are UTXO commitments

### Proposed solutions

#### FastSync

**Advantages**

- Uses an EC multiset to derive the public key of the set of elements inside the UTXO set, regardless of order.
- The cryptographic algorithm used is the same for the generation of key pairs, so it can be considered secure, fast and reliable.

**Disadvantages**

- What is published is not a commitment, but a snapshot of the UTXO set at a given time.
- It does not allow partial verification. A new node must first download the entire UTXO set to know if it corresponds with the valid UTXO set.
- It is only updated every _n_ blocks, instead of every block.
- It does not provide any advantage for users, only node operators.

#### RSA accumulator

https://findora.org/faq/ads/rsa-accumulators/

##### Non-membership witness

If the value `val` is not in the accumulator with current state head `A = 3^y mod N`, then `x = HashPrime(val)` is co-prime with `y`.

The Euclidean algorithm is used to find a large integer `a` (proportional to `y`) and a smaller integer `b` (proportional to `x`) such that `ax + by = 1`. The non-membership witness for val is `(D, b)` where `D = 3^a`. The non-membership witness is verified by checking that `D^xA^b = 3`.



#### Minichain

MiniChain is a proposed stateless blockchain. Nodes do not need to maintain the UTXO set; instead, participants creating transactions send a proof showing that the coins they are trying to spend **are not** in the STXO (spent transaction output) and **are** in the TXO (transaction output) set. That way, they show the coin is valid by proving both that it was actually created at some point and that it has not been spent.

The STXO accumulator is a data structure based on an RSA accumulator. The TXO accumulator is based in MMR (merkle mountain ranges).


---

## Proposal

1. Generate EC multiset of the UTXO set.
2. Generate RSA accumulator of the STXO set.
3. Generate RSA accumulator of the TXO set.
4. Publish the UTXO set.

If a node wants to download the UTXO set:

1. Asks for the UTXO set and its EC multiset.
2. For each UTXO, checks whether it is in the TXO set.
3. For each UTXO, checks wether it is not in the STXO set.
