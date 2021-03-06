---
description: Hedera accounts
---

# Accounts

## Accounts

Accounts are the central starting point for Hedera. Accounts are stored on the public ledger and are required to pay transaction fees. Accounts hold hbars which are used to pay for the transction fees. 

Accounts are comprised of:

* Keys
* Account ID
* Balance
* Livehash\(es\)

## Keys

Each account has a public and private key pair. The private key of the account is used authorize and sign transactions. The private key is not to be shared with other members on the network as they can authorize transactions from your account on your behalf. The public key is what is visable to others on the account. Key pairs are used to identify the user and authorize transactions that are submitted to the network for consensus.

The public key can be shared and is visible to other users in the network. The private key should be kept secret to the owner. Private keys _cannot_ be recovered once they are lost.

Public and private keys are generated by an algorithm and are unique to one another. Hedera currently supports the following key generation systems:

* [Ed25519](https://ed25519.cr.yp.to/index.html)
* Smart contract ID

```java
// Ed25519 keys example
private key   = 302e020100300506032...

public key   = 302...
```

## Account ID

Hedera account IDs have the format x.y.z \(eg 0.0.3\) where:

* x represents the shard number \(`shardId`\). It will default to 0 today, as Hedera only performs in one shard.
* y represents the realm number \(`realmId`\). It will default to 0 today, as realms are not yet supported.
* z represents the account number, the equivalent of a human-friendly public key.

## Balance

The amount of HBAR \(ℏ\) held by the account.

## Expiration

Accounts, like files and smart contracts, take up storage on the network. Accounts must have a sufficient amount of hbar to fund a renewal of its storage on the network. The amount for renewal will be charged every pre-determined number of seconds. This amount of time is known as the autoRenewPeriod.

The maximum autoRenewPeriod for an account, file, or smart contract will be limited to 3 months \(7890000 seconds\).

## LiveHash

A hash \(presumably of some kind of credential or certificate\), along with a list of keys \(each of which is either a primitive or a threshold key\). Each of them must reach its threshold when signing the transaction, to attach this livehash to this account. At least one of them must reach its threshold to delete this livehash from this account.

