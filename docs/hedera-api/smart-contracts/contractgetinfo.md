# ContractGetInfo

## ContractGetInfoQuery

Get information about a smart contract instance. This includes the account that it uses, the file containing its bytecode, and the time when it will expire.

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [QueryHeader](../miscellaneous/queryheader.md) | standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\). |
| contractID | [ContractID](../basic-types/contractid.md) | the contract for which information is requested |

## ContractGetInfoResponse

Response when the client sends the node ContractGetInfoQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [ResponseHeader](../miscellaneous/responseheader.md) | standard response from node to client, including the requested fields: cost, or state proof, or both, or neither |
| contractInfo | [ContractGetInfoResponse.ContractInfo](contractgetinfo.md#contractgetinforesponse-contractinfo) | the information about this contract instance \(a state proof can be generated for this\) |

## ContractGetInfoResponse.ContractInfo

Response when the client sends the node ContractGetInfoQuery

| Field | Type | Description |
| :--- | :--- | :--- |
| contractID | [ContractID](../basic-types/contractid.md) | ID of the contract instance, in the format used in transactions |
| accountID | [AccountID](../basic-types/accountid.md) | ID of the cryptocurrency account owned by the contract instance, in the format used in transactions |
| contractAccountID |  | ID of both the contract instance and the cryptocurrency account owned by the contract instance, in the format used by Solidity |
| adminKey | [Key](../basic-types/key.md) | the state of the instance and its fields can be modified arbitrarily if this key signs a transaction to modify it. If this is null, then such modifications are not possible, and there is no administrator that can override the normal operation of this smart contract instance. Note that if it is created with no admin keys, then there is no administrator to authorize changing the admin keys, so there can never be any admin keys for that instance. |
| expirationTime | [Timestamp](../miscellaneous/timestamp.md#timestamp) | the current time at which this contract instance \(and its account\) is set to expire |
| autoRenewPeriod | [Duration](../miscellaneous/duration.md) | the expiration time will extend every this many seconds. If there are insufficient funds, then it extends as long as possible. If the account is empty when it expires, then it is deleted. |
| storage |  | number of bytes of storage being used by this instance \(which affects the cost to extend the expiration time\) |
| memo |  | the memo associated with the contract \(max 100 bytes\) |

