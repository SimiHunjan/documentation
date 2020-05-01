# FileUpdate

## FileUpdateTransactionBody

Modify some of the metadata for a file. Any null field is ignored \(left unchanged\). Any field that is null is left unchanged. If contents is non-null, then the file's contents will be replaced with the given bytes. This transaction must be signed by all the keys for that file. If the transaction is modifying the keys field, then it must be signed by all the keys in both the old list and the new list.

| Field | Type | Description |
| :--- | :--- | :--- |
| fileID | [FileID](../basic-types/fileid.md) | The ID of the file to update |
| expirationTime | [Timestamp](../miscellaneous/timestamp.md#timestamp) | The new expiry time \(ignored if not later than the current expiry\) |
| keys | [KeyList](../basic-types/keylist.md) | The new list of keys that can modify or delete the file |
| contents |  | The new contents that should overwrite the file's current contents |

