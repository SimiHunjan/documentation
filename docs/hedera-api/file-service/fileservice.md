# FileService

| RPC | Request | Response | Comments |
| :--- | :--- | :--- | :--- |
| `createFile` | Transaction | TransactionResponse | Creates a file with the content by submitting the transaction. The grpc server returns the TransactionResponse |
| `updateFile` | Transaction | TransactionResponse | Updates a file by submitting the transaction. The grpc server returns the TransactionResponse |
| `deleteFile` | Transaction | TransactionResponse | Deletes a file by submitting the transaction. The grpc server returns the TransactionResponse |
| `appendContent` | Transaction | TransactionResponse | Appends the file contents\(for a given FileID\) by submitting the transaction. The grpc server returns the TransactionResponse |
| `getFileContent` | Query | Response | Retrieves the file content by submitting the query. The grpc server returns the Response |
| `getFileInfo` | Query | Response | Retrieves the file information by submitting the query. The grpc server returns the Response |
| `systemDelete` | Transaction | TransactionResponse | Deletes a file by submitting the transaction when the account has admin privileges on the file. The grpc server returns the TransactionResponse |
| `systemUndelete` | Transaction | TransactionResponse | UnDeletes a file by submitting the transaction when the account has admin privileges on the file. The grpc server returns the TransactionResponse |

