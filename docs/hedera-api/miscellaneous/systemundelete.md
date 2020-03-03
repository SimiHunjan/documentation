# SystemUndelete

## SystemUndeleteTransactionBody

Undelete a file or smart contract that was deleted by AdminDelete - can only be done with a Hedera admin multisig. When it is deleted, it immediately disappears from the system as seen by the user, but is still stored internally until the expiration time, at which time it is truly and permanently deleted. Until that time, it can be undeleted by the Hedera admin multisig. When a smart contract is deleted, the cryptocurrency account within it continues to exist, and is not affected by the expiration time here.

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| id | oneof |  |  |
|  | fileID | [FileID](../basic-types/fileid.md) | The file ID to undelete, in the format used in transactions |
|  | contractID | [ContractID](../basic-types/contractid.md) | The contract ID instance to undelete, in the format used in transactions |

