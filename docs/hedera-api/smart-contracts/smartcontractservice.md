# SmartContractService

| RPC | Request | Response | Comments |
| :--- | :--- | :--- | :--- |
| `createContract` | Transaction | TransactionResponse | Creates a contract by submitting the transaction. The grpc server returns the TransactionResponse |
| `updateContract` | Transaction | TransactionResponse | Updates a contract with the content by submitting the transaction. The grpc server returns the TransactionResponse |
| `contractCallMethod` | Transaction | TransactionResponse | Calls a contract by submitting the transaction. The grpc server returns the TransactionResponse |
| `getContractInfo` | Query | Response | Retrieves the contract information by submitting the query. The grpc server returns the Response |
| `contractCallLocalMethod` | Query | Response | Calls a smart contract by submitting the query. The grpc server returns the Response |
| `ContractGetBytecode` | Query | Response | Retrieves the byte code of a contract by submitting the query. The grpc server returns the Response |
| `getBySolidityID` | Query | Response | Retrieves a contract\(using Solidity ID\) by submitting the query. The grpc server returns the Response |
| `getTxRecordByContractID` | Query | Response | Retrieves a contract\(using contract ID\) by submitting the query. The grpc server returns the Response |
| `deleteContract` | Transaction | TransactionResponse | Delete a contract instance\(mark as deleted until it expires\), and transfer hbars to the specified account. The grpc server returns the TransactionResponse |
| `systemDelete` | Transaction | TransactionResponse | Deletes a smart contract by submitting the transaction when the account has admin privileges on the file. The grpc server returns the TransactionResponse |
| `systemUndelete` | Transaction | TransactionResponse | UnDeletes a smart contract by submitting the transaction when the account has admin privileges on the file. The grpc server returns the TransactionResponse |

