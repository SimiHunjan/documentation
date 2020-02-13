# Release Notes

## **0.4.0 Release Notes**

{% hint style="info" %}
**Note:** Mainnet update is scheduled to occur on February 10, 2020.
{% endhint %}

#### Hedera Services Code \(0.4.0\)

*  Improved end to end testing.
* General code clean up and refactoring.
* ContractCall - TransactionReceipt response to ContractCall no longer includes the contractID called
* CryptoUpdate - TransactionReceipt response to CryptoUpdate no longer includes the accountID updated
* CryptoTransfer – CryptoTransfer transactions resulting in INSUFFICIENT\_ACCOUNT\_BALANCE error no longer list Transfers in the TransactionRecord transferList that were not applied

#### Mirror Node \(0.5.3\) 

* Changed how the mirror node verifies mainnet consensus. Mirror node now waits for at least third of node signatures rather than greater than two thirds to verify consensus.
*  Added new mainnet nodes to the mirror node address book.
* Access still restricted to a white listed set of IP addresses. Request access [here](https://learn.hedera.com/l/576593/2020-01-13/7z5jb).
* Please see the Mirror Node releases page for the full list of changes [here](https://github.com/hashgraph/hedera-mirror-node/releases).
* We occasionally may encounter a situation where an additional 15-20 second delay in message round trip time is experienced and subscriber connections are dropped. No messages are lost, and the consensus time is not affected. Clients are encouraged to reconnect. This issue will be fixed in a subsequent release of the Hedera mirror node. Some third-party mirror nodes should not be affected by this issue. We also don't expect it to impact the exchanges using the REST end point for the mirror node. 

#### SDKs 

* Java SDK has been updated to support the Hedera Consensus Service
* JavaScript/Typescript SDK has reached version 1.0.0, supporting all four mainnet services
* JavaScript/Typescript SDK supports both running in the browser \(with Envoy Proxy\) and in Node.
* Go SDK now supports all four mainnet services.

**Fees**

* Transfer list within transaction records now shows only a single net amount in or out for each account, reflecting both transfers and any fees paid.
* Fixed bug in fee schedule that had resulted in fees for ContractCallLocal, ContractGetBytecode, and getVersion queries being undercharged by ~33%
* You may get more information regarding transaction record fees [here](https://docs.hedera.com/guides/mainnet/fees/transaction-records).

#### SDK Extension Components

* The Hedera SDK Extension Components \(SXC\) is an open sourced set of pre-built components that aim to provide additional functionality over and above HCS to make it easier and quicker to develop applications, particularly if they require secure communications between participants.
* Components use the Hedera Java SDK to communicate with the Hedera Consensus Service.
* Learn more about Hedera SXC [here](https://github.com/hashgraph/hedera-hcs-sxc).



