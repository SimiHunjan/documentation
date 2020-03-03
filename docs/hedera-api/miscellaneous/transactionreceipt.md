# TransactionReceipt

## TransactionReceipt

The consensus result for a transaction, which might not be currently known, or may succeed or fail.

| Field | Type | Description |  |
| :--- | :--- | :--- | :--- |
| status | [ResponseCodeEnum](responsecode.md#responsecodeenum) | whether the transaction succeeded or failed \(or is unknown\) |  |
| accountID | [AccountID](../basic-types/accountid.md) | The account ID, if a new account was created |  |
| fileID | [FileID](../basic-types/fileid.md) | The file ID, if a new file was created |  |
| contractID | [ContractID](../basic-types/contractid.md) | The contract ID, if a new smart contract instance was created |  |
| exchangeRate | [ExchangeRateSet](exchangerate.md#exchangerateset) | exchange rate set of Hbar to cents \(USD\) |  |



