# CryptoAddClaim

## Claim

A hash \(presumably of some kind of credential or certificate\), along with a list of keys \(each of which is either a primitive or a threshold key\). Each of them must reach its threshold when signing the transaction, to attach this claim to this account. At least one of them must reach its threshold to delete this Claim from this account. This is intended to provide a revocation service: all the authorities agree to attach the hash, to attest to the fact that the credential or certificate is valid. Any one of the authorities can later delete the hash, to indicate that the credential has been revoked. In this way, any client can prove to a third party that any particular account has certain credentials, or to identity facts proved about it, and that none of them have been revoked yet.

| Field | Type | Description |
| :--- | :--- | :--- |
| accountID | [AccountID](../basic-types/accountid.md) | the account to which the claim is attached |
| hash |  | 48 byte SHA-384 hash \(presumably of some kind of credential or certificate\) |
| keys | [KeyList](../basic-types/keylist.md) | list of keys: all must sign the transaction to attach the claim, and any one of them can later delete it. Each "key" can actually be a threshold key containing multiple other keys \(including other threshold keys\). |
| claimDuration | [Duration](../miscellaneous/duration.md) | the duration for which the claim will remain valid |

## CryptoAddClaimTransactionBody

Attach the given hash to the given account. The hash can be deleted by the keys used to transfer money from the account. The hash can also be deleted by any one of the deleteKeys \(where that one may itself be a threshold key made up of multiple keys\). Therefore, this acts as a revocation service for claims about the account. External authorities may issue certificates or credentials of some kind that make a claim about this account. The account owner can then attach a hash of that claim to the account. The transaction that adds the claim will be signed by the owner of the account, and also by all the authorities that are attesting to the truth of that claim. If the claim ever ceases to be true, such as when a certificate is revoked, then any one of the listed authorities has the ability to delete it. The account owner also has the ability to delete it at any time.

| Field | Type | Description |
| :--- | :--- | :--- |
| claim | [Claim](cryptoaddclaim.md#claim) | A hash of some credential/certificate, along with the keys that authorized it and are allowed to delete it |

