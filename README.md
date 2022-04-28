# BItcoin Cash UTXO Commitments

Collection of the existing proposals to implement UTXO commitments and FastSync in the Bitcoin Cash network.

## What are UTXO commitments?

UTXO commitments allow nodes to retrieve the current state of the network without needing to download the entire transaction history. Instead, they get a snapshot of the state of the blockchain (UTXO set) and perform a cryptographic verification to make sure they have the correct state, which then allows them to function normally.

## Existing proposals

- [UtxoCommitment version 0](https://github.com/tomasvdw/bips/blob/master/ecmh-utxo-commitment-0.mediawiki) by Tomas van der Wansem.
- [Bucketed Utxo Commitment](https://github.com/tomasvdw/bips/blob/master/BIP-UtxoCommitBucket.mediawiki) by Tomas van der Wansem.
- [UTXO Fastsync](https://bitcoincashresearch.org/t/chip-2021-07-utxo-fastsync/502) by Josh Green. Also available in [this link](https://github.com/SoftwareVerde/bitcoin-verde/blob/master/specification/utxo-fastsync-chip-20210625.md).

## Relevant documents

- [Bitcoin whitepaper](https://www.bitcoin.com/bitcoin.pdf)
- [Bitcoin On-Chain Pruning](https://www.scribd.com/document/317130737/Bitcoin-On-Chain-Pruning) by Peter Gregory Jr.
