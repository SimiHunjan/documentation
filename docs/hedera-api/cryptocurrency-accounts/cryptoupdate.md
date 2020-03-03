# CryptoUpdate

## CryptoUpdateTransactionBody

Change properties for the given account. Any null field is ignored \(left unchanged\). This transaction must be signed by the existing key for this account. If the transaction is changing the key field, then the transaction must be signed by both the old key \(from before the change\) and the new key. The old key must sign for security. The new key must sign as a safeguard to avoid accidentally changing to an invalid key, and then having no way to recover. When extending the expiration date, the cost is affected by the size of the list of attached claims, and of the keys associated with the claims and the account.

| Field | Type | Description |
| :--- | :--- | :--- |
| accountIDToUpdate | [AccountID](../basic-types/accountid.md) | The account ID which is being updated in this transaction |
| key | [Key](../basic-types/key.md) | The new key |
| proxyAccountID | [AccountID](../basic-types/accountid.md) | ID of the account to which this account is proxy staked. If proxyAccountID is null, or is an invalid account, or is an account that isn't a node, then this account is automatically proxy staked to a node chosen by the network, but without earning payments. If the proxyAccountID account refuses to accept proxy staking , or if it is not currently running a node, then it will behave as if proxyAccountID was null. |
| proxyFraction |  | \[Deprecated\]. payments earned from proxy staking are shared between the node and this account, with proxyFraction / 10000 going to this account |
| sendRecordThresholdField | oneof |  |
|  | sendRecordThreshold |  |
|  | sendRecordThresholdWrapper | google.protobuf.UInt64Value |
| receiveRecordThresholdField | oneof |  |
|  | receiveRecordThreshold |  |
|  | receiveRecordThresholdWrapper | google.protobuf.UInt64Value |
| autoRenewPeriod | [Duration](../miscellaneous/duration.md) | The duration in which it will automatically extend the expiration period. If it doesn't have enough balance, it extends as long as possible. If it is empty when it expires, then it is deleted. |
| expirationTime | [Timestamp](../miscellaneous/timestamp.md) | The new expiration time to extend to \(ignored if equal to or before the current one\) |
| receiverSigRequiredField | oneof |  |
|  | receiverSigRequired |  |
|  | receiverSigRequiredWrapper | google.protobuf.BoolValue |

