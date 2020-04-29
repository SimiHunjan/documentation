# Release Notes

| Network | Version |
| :--- | :--- |
| **Mainnet** | Mirror Node v0.8.1 |
| **Testnet** | Mirror Node v0.9.1 |

## Upcoming Release \[May 5, 2020\]

**Hedera Services Code \(v0.5.0\)**   
  
In Hedera Services v0.5.0, we’ve added TLS for trusted communication with nodes on the Hedera network. For better security, only TLS v1.2 and v1.3 with TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384 and TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 cipher suites are allowed.   
  
We’ve added new metadata in the Hedera NodeAddressBook, accessible in system file 0.0.101. The versions of the node software and gRPC Hedera API \(HAPI\) are now queryable via GetVersionInfo under the new NetworkService for node- and network-scoped operations.   
  
For Hedera Consensus Service, we’ve updated the topic running hash calculation to use the SHA-384 hash of the submitted message, rather than the message itself. This reduces the storage requirements needed to validate the hash of a topic. The record of a ConsensusSubmitMessage transaction that uses the new hashing scheme will have a new topicRunningHashVersion field in its receipt. The value of the field will be 2.   
  
Hedera File Service also has several fixes of note. First, we enabled immutable files. Second, we relaxed the signing requirements for a FileDelete transaction to match the semantics of a revocation service. Third, we fixed a fee calculation bug that overcharged certain FileUpdate transactions.   
  
For Hedera Smart Contract Service, we’ve improved visibility into transactions that create child contracts using the new keyword by putting created ids in the record of the transaction; and we now propagate parent contract metadata to created children.   
  
Finally, if you use the throttle properties in system file 0.0.121 to estimate network performance limits, you will also be interested in a new standardized format of those properties. The lists below contain these and other minor updates, bug fixes, and documentation changes. 

**Mirror Node \(v0.9.0\)**

Mainnet mirror nodes will be upgraded to [v0.9.0](release-notes.md#mirror-node-v-0-9-0).  

**Enhancements** 

* Add support for TLS
* Expand address book metadata
* Return all created contract ids 
* Propagate creator contract metadata
* Introduce GetVersionInfo query 
* Standardize throttle configuration 
* Enforce file.encoding=utf-8 on startup 
* Make duration properties inclusive for readability

**Bug fixes** 

* Use message SHA-384 hash in running hash 
* Enable immutable files Relax 
* FileDelete signing requirements 
* Fix sbh calculation in 
* FileUpdate Return metadata for deleted files
* Enforce receiver signing requirements during contract execution 
* Reject invalid CryptoGetInfo
* Reject CryptoCreate with empty key
* Return NOT\_SUPPORTED for state proof queries 
* Waive fees for 0.0.57 updating 0.0.111
* Waive signing requirements for 0.0.55 updating 0.0.121/0.0.122
* Waive all fees for 0.0.2
* Do not throttle system accounts 

**Documentation changes** 

* Replace “claim” with “livehash” as appropriate
* Standardize and clarify HAPI doc

## [Mirror Node \(v0.9.1\)](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.9.1)

Small bug fix release to address not being able to handle address book updates that span multiple transactions.

## [Mirror Node \(v0.9.0\)](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.9.0)

This release contains another new REST API for our [consensus service](https://www.hedera.com/consensus-service/). You can now retrieve all topic messages in a particular topic, with additional filtering by sequence number and consensus timestamp. Here's an example:

`GET /api/v1/topic/7?sequencenumber=gt:2&timestamp=lte:1234567890.000000006&limit=2`

```text
{
  "messages": [
    {
      "consensus_timestamp": "1234567890.000000003",
      "topic_id": "0.0.7",
      "message": "bWVzc2FnZQ==",
      "running_hash": "cnVubmluZ19oYXNo",
      "sequence_number": 3
    },
    {
      "consensus_timestamp": "1234567890.000000004",
      "topic_id": "0.0.7",
      "message": "bWVzc2FnZQ==",
      "running_hash": "cnVubmluZ19oYXNo",
      "sequence_number": 4
    }
  ],
  "links": {
     "next": "/api/v1/topic/7?sequencenumber=gt:2&timestamp=lte:1234567890.000000006&timestamp=gt:1234567890.000000004&limit=2"
  }
}
```

The other big feature of this release is [Kubernetes](https://kubernetes.io/) support. We've create a [Helm](https://helm.sh/) chart that can be used to deploy a highly available Mirror Node with a single command. This feature is still under heavy development as we work towards converting our current deployments to this new approach.

## [Mirror Node \(v0.8.1\)](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.8.1)

Small bug fix release to fix a packaging issue.

## [Mirror Node \(v0.8.0\)](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.8.0)

Mirror node v0.8.0 is here! We're made great strides in making the mirror node easier to run and manage. In particular, we added support for [requester pays](https://docs.aws.amazon.com/AmazonS3/latest/dev/RequesterPaysBuckets.html) buckets. This will allow anyone to run a mirror node as long as they are willing to pay for the cost to retrieve the data. Currently only Hedera and a few partners have access to the bucket, so enabling this will open up that data to our community. We are still working on a migration of the buckets to this model, so stay tuned.

We also added two new experimental REST APIs to retrieve HCS data. Firstly, we added `/api/v1/topic/message/${consensusTimestamp}` to retrieve a topic message by its consensus timestamp. Secondly, we added `/api/v1/topic/${topic}/message/${seqNum}` to retrieve a particular topic message by its sequence number from a topic. These APIs are considered alpha and may changed or be removed in the future. We also dramatically increased test coverage for the REST APIs and squashed some bugs in the process.

For our GRPC API, we had to switch from R2DBC to Hibernate to reach the scale and stability that we needed. In doing so, we can now support a lot more concurrent subscribers at a higher throughput. It should also finally put to rest any stability concerns with the GRPC component.

There are a few breaking changes that we had to make. We now no longer write and store record or balance files to the filesystem after they are inserted into the database. If you still need these files, you can set `hedera.mirror.parser.balance.keepFiles` and `hedera.mirror.parser.record.keepFiles` to true.

Also, we moved the persist properties to be grouped under a new path. That is we moved options like `hedera.mirror.parser.record.persistTransactionBytes` to `hedera.mirror.parser.record.persist.transactionBytes`. Please update your local configuration accordingly.

## [Mirror Node \(v0.7.0\) ](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.7.0)

0.7.0 focuses on refactoring the record file parsing to decouple the parsing from the persisting of data. This refactoring is laying the groundwork for additional performance improvements and allowing additional downstream components to register for notification of the transactions.

## 0.4.1 Updates

#### Hedera Services Code \(v0.4.1\) 

* Software update includes the ability for Hedera to dynamically set throttles on network transaction types. 
* The following throttles would be updated to: 1000 submit messages per second and 5 topic creates per second. 
* Reassigning of new Council Member nodes 

#### [Mirror Node \(v0.6.0\) ](https://github.com/hashgraph/hedera-mirror-node/releases/tag/v0.6.0)

* Release focused on stability and performance improvements. 
* End to end test coverage. 

This release was mainly focused on enhancing the stability and performance of the mirror node. We improved the transaction ingestion speed from 600 to about 4000 transactions per second. At the same time, we greatly improved the resiliency and performance of the GRPC module. We also added acceptance tests to test out HCS end to end.

**Breaking Change**

Please note that one potentially breaking change in this release is to reject subscriptions to topics that don't exist. This avoids the server having to poll repeatedly until it is created and taking up resources for a topic that may never exist. It is expected that clients or the [SDK](https://github.com/hashgraph/hedera-sdk-java/issues/367) will poll periodically after creating a topic until that topic makes its way to the mirror node. This functionality is hidden behind a feature flag but will slowly be rolled out over the next month.

## **0.4.0 Updates**

{% hint style="info" %}
**Note:** Mainnet update is scheduled to occur on February 10, 2020.
{% endhint %}

#### Hedera Services Code \(v0.4.0\)

* Say hello to the Hedera Consensus Service! This release is the first to include HCS, allowing verifiable timestamping and ordering of application messages.  
* Network pricing has been updated to include HCS transactions and queries 
* Network throttle for HCS set to 1000 tps for submitting messages, and 100 tps for each of the other HCS operations. 
* Improved end to end testing.
* General code clean up and refactoring.
* ContractCall - TransactionReceipt response to ContractCall no longer includes the contractID called
* CryptoUpdate - TransactionReceipt response to CryptoUpdate no longer includes the accountID updated
* CryptoTransfer – CryptoTransfer transactions resulting in INSUFFICIENT\_ACCOUNT\_BALANCE error no longer list Transfers in the TransactionRecord transferList that were not applied

#### Mirror Node \(v0.5.3\) 

* Now supports all HCS functionality including a streaming gRPC API for message topic subscription. 
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



