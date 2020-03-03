# FileCreate

## FileCreateTransactionBody <a id="filecreatetransactionbody"></a>

‌Create a new file, containing the given contents. It is referenced by its FileID, and does not have a filename, so it is important to get the FileID. After the file is created, the FileID for it can be found in the receipt, or retrieved with a GetByKey query, or by asking for a Record of the transaction to be created, and retrieving that.

| Field | Type | Description |
| :--- | :--- | :--- |
| expirationTime | ​[Timestamp](../miscellaneous/timestamp.md#timestamp)​ | The time at which this file should expire \(unless FileUpdateTransaction is used before then to extend its life\) |
| keys | ​[KeyList](../basic-types/keylist.md)​ | All these keys must sign to create or modify the file. Any one of them can sign to delete the file. |
| contents | ​Content | The bytes that are the contents of the file |
| shardID | ​[ShardID](../basic-types/shardid.md)​ | Shard in which this file is created |
| realmID | ​[RealmID](../basic-types/realmid.md)​ | The Realm in which to the file is created \(leave this null to create a new realm\) |
| newRealmAdminKey | ​[Key](../basic-types/key.md)​ | If realmID is null, then this the admin key for the new realm that will be created |

