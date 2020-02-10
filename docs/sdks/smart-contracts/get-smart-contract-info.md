# Get smart contract info

`ContractInfoQuery()` returns information about a smart contract instance.

* Account ID
* Contract ID
* Receipt
* Expiration time
* Number of bytes of storage bein used
* Memo

| Constructor | Description |
| :--- | :--- |
| `ContractInfoQuery()` | Initializes a ContractCallInfoQuery object |

```java
new ContractInfoQuery()
```

## Basic

| Method | Type | Description |
| :--- | :--- | :--- |
| `setContractId(<contractId>)` | ContractId | The ID of the smart contract to return the information for |

## Example

```java
// create the contract's bytecode file
TransactionId fileTxId = new FileCreateTransaction()
    // Use the same key as the operator to "own" this file
    .addKey(OPERATOR_KEY.publicKey)
    .setContents(byteCode)
    .execute(client);

TransactionReceipt fileReceipt = fileTxId.getReceipt(client);
FileId newFileId = fileReceipt.getFileId();

System.out.println("contract bytecode file: " + newFileId);

TransactionId contractTxId = new ContractCreateTransaction()
    .setBytecodeFileId(newFileId)
    .setGas(100000000)
    .setConstructorParams(
        new ContractFunctionParams()
            .addString("hello from hedera!"))
    .execute(client);

TransactionReceipt contractReceipt = contractTxId.getReceipt(client);
ContractId newContractId = contractReceipt.getContractId();

System.out.println("new contract ID: " + newContractId);

ContractInfo getContractInfo = new ContractInfoQuery()
    .setContractId(newContractId)
    .execute(client);

System.out.println("Contract ID is " +getContractInfo.accountId);
```

