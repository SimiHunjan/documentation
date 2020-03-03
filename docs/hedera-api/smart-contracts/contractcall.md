# ContractCall

## **ContractCallTransactionBody**

Call a function of the given smart contract instance, giving it functionParameters as its inputs. it can use the given amount of gas, and any unspent gas will be refunded to the paying account.

| Field | Type | Description |
| :--- | :--- | :--- |
| contractID | [ContractID](../basic-types/contractid.md) | the contract instance to call, in the format used in transactions |
| gas |  | the maximum amount of gas to use for the call |
| amount |  | number of tinybars sent \(the function must be payable if this is nonzero\) |
| functionParameters |  | which function to call, and the parameters to pass to the function |

