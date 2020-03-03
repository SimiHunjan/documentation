# ConsensusTopicInfo

|  Field | Type | Description |
| :--- | :--- | :--- |
| `memo` | ​Content | Short publicly visible memo about the topic. No guarantee of uniqueness. |
| `runningHash` | ​Content | SHA-384 running hash &lt;previousRunningHash, topicId, consensusTimestamp, sequenceNumber, message&gt; |
| `sequenceNumber` | ​Content | Sequence number \(starting at 1 for the first submitMessage\) of messages on the topic. |
| `expirationTime` | ​[Timestamp](../miscellaneous/timestamp.md#timestamp)​ | Effective consensus timestamp at \(and after\) which submitMessage calls will no longer succeed on the topic and the topic will expire and after AUTORENEW\_GRACE\_PERIOD be automatically deleted. |
| `adminKey` | ​[Key](../basic-types/key.md)​ | Access control for update/delete of the topic. Null if there is no key. |
| `submitKey` | ​[Key](../basic-types/key.md)​ | Access control for ConsensusService.submitMessage. Null if there is no key. |
| `autoRenewPeriod` | ​[Duration](../miscellaneous/duration.md)​ | ​Content |
| `autoRenewAccount` | ​[AccountID](../basic-types/accountid.md)​ | Null if there is no autoRenewAccount. |

