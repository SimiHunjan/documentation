# Delete a file

`FileDeleteTransaction()` deletes a file stored on the Hedera network. Once the file has been deleted, it will be marked as deleted until it expires and will not retain any of its contents.

| Constructor | Description |
| :--- | :--- |
| `FileDeleteTransaction()` | Initializes the FileDeleteTransaction object |

```java
new FileDeleteTransaction()
```

## Basic

| Methods | Type | Description |
| :--- | :--- | :--- |
| `setFileId(<fileId>)` | FileId | The ID of the file to delete |

## Example

{% tabs %}
{% tab title="Java" %}
```java
TransactionId fileDeleteTxnId = new FileDeleteTransaction()
     .setFileId(newFileId)
     .execute(client);

// if this doesn't throw then the transaction was a success
fileDeleteTxnId.getReceipt(client);

System.out.println("File deleted successfully.");

FileInfo fileInfo = new FileInfoQuery()
     .setFileId(newFileId)
     .execute(client);
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const operatorAccount = process.env.OPERATOR_ID;
const operatorPrivateKey = process.env.OPERATOR_KEY;
const operatorPublicKey = Ed25519PublicKey.fromString(process.env.OPERATOR_PUB_KEY);

 if (operatorPrivateKey == null || operatorAccount == null) {
  throw new Error(
    "environment variables OPERATOR_KEY and OPERATOR_ID must be present"
  );
}

const client = new Client({
   network: { "0.testnet.hedera.com:50211": "0.0.3" },
   operator: {
     account: operatorAccount,
     privateKey: operatorPrivateKey
   }
});

// First, we'll create a file with our operator as an admin
const transactionId = await new FileCreateTransaction()
   .setContents("creating a file to test deletion")
   .setMaxTransactionFee(Hbar.of(100))
   .addKey(operatorPublicKey)
   .execute(client);

// The receipt will contain the FileId, or where it exists on the network
const createFileReceipt = await transactionId.getReceipt(client);
console.log("create file receipt ", JSON.stringify(createFileReceipt) + "\n");

// Then we'll delete this newly created file
const deleteFileTransactionId = await new FileDeleteTransaction()
   .setFileId(createFileReceipt._fileId) // Define which file to delete
   .setMaxTransactionFee(Hbar.of(100))
   .execute(client); // Presumes the client is the file's admin key

// After deletion, the receipt should NOT contain a file ID
const deleteFileReceipt = await deleteFileTransactionId.getReceipt(client);
console.log("deleted file receipt, won't contain a file ID ", JSON.stringify(deleteFileReceipt) + "\n");  
```
{% endtab %}
{% endtabs %}

