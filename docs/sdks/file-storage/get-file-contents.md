# Get file contents

`FileContentsQuery()` returns the contents of a file. If the file is empty the content field is empty. The response returns the file ID and the file contents in bytes.

| Constructor | Description |
| :--- | :--- |
| `FileContentsQuery()` | Initializes a FileContentQuery object |

```java
new FileContentsQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setAccountId(<account>)` | AccountId | The ID of the file to get contents from |

## Example

{% tabs %}
{% tab title="Java" %}
```java
byte[] fileContents = ("Hedera is great!").getBytes();

// Create the new file and set its properties
TransactionId newFileTxId = new FileCreateTransaction()
    .addKey(OPERATOR_KEY.getPublicKey()) // The public key of the owner of the file
    .setContents(fileContents) // Contents of the file
    .setMaxTransactionFee(200000000) // 2h
    .execute(client);

FileId newFileId = newFileTxId.getReceipt(client).getFileId();

//Print the file ID to console
System.out.println("The new file ID is " + newFileId.toString());

// Get file contents
FileGetContentsResponse contents = new FileContentsQuery()
    .setFileId(newFileId)
    .execute(client);

// Prints query results to console
System.out.println("File content query results: " + contents.getFileContents().getContents().toStringUtf8());
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
const fileContents = await new FileContentsQuery()
    .setFileId(fileId)
    .execute(client);
    
console.log(`file contents: ${fileContents}`)
```
{% endtab %}
{% endtabs %}

