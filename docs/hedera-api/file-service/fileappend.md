# FileAppend

## FileAppendTransactionBody

‌Append the given contents to the end of the file. If a file is too big to create with a single FileCreateTransaction, then it can be created with the first part of its contents, and then appended multiple times to create the entire file.

| Field | Type | Description |
| :--- | :--- | :--- |
| fileID | ​[FileID](/@docs-hedera/s/hedera-api/basic-types-1/untitled-2)​ | The file ID of the file to which the bytes are appended to |
| contents | ​Content | The bytes to append to the contents of the file |

