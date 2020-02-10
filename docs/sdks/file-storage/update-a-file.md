# Update a file

`FileUpdateTransaction()` updates the metadata for a file. This transaction must be signed by all the keys assigned to the file.

| Constructor | Description |
| :--- | :--- |
| `FileUpdateTransaction()` | Intializes the FileUpdateTransaction object |

```java
new FileUpdateTransaction()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setFileId(<fileId>)` | FileId | The FileID of the file to update |
| `addKey(<key>)` | [Ed25519PublicKey](https://github.com/hashgraph/hedera-sdk-java/blob/master/src/main/java/com/hedera/hashgraph/sdk/crypto/ed25519/Ed25519PublicKey.java) | The public key\(s\) to add to update the file with |
| `setContents(<contents>)` | byte\[ \] | The contents to update the file with |
| `setExpirationTime(<expiration>)` | Instant | The new expiration time  |

## Example

```java
// `Client.forMainnet()` is provided for connecting to Hedera mainnet
Client client = Client.forTestnet();

// Defaults the operator account ID and key such that all generated transactions will be paid for
// by this account and be signed by this key
client.setOperator(OPERATOR_ID, OPERATOR_KEY);

// Content to be stored in the file
byte[] fileContents = ("Hedera is great!").getBytes();

// Create the new file and set its properties
TransactionId newFileTxId = new FileCreateTransaction()
    .addKey(OPERATOR_KEY.publicKey) // The public key of the owner of the file
    .setContents(fileContents) // Contents of the file
    .setMaxTransactionFee(new Hbar(2))
    .execute(client);

FileId newFileId = newFileTxId.getReceipt(client).getFileId();

//Print the file ID to console
System.out.println("The new file ID is " + newFileId.toString());

// Get file contents
byte[] contents = new FileContentsQuery()
    .setFileId(newFileId)
    .execute(client);

// Prints query results to console
System.out.println("File content query results: " + new String(contents));

TransactionId updateFileTx = new FileUpdateTransaction()
    .setFileId(newFileId)
    .setContents(("This is the updated content to the file ").getBytes())
    .execute(client);

byte[] updateContents = new FileContentsQuery()
    .setFileId(newFileId)
    .execute(client);
    
System.out.println("File content query results: " + new String(updateContents));
```

