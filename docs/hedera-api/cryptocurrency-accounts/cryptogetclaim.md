# CryptoGetClaim

## CryptoGetClaimQuery

Get a single claim attached to an account, or return null if it does not exist.

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [QueryHeader](../miscellaneous/queryheader.md) | Standard info sent from client to node, including the signed payment, and what kind of response is requested \(cost, state proof, both, or neither\). |
| accountID | [AccountID](../basic-types/accountid.md) | The account ID to which the claim was attached |
| hash |  | The hash of the claim |

## CryptoGetClaimResponse

Response when the client sends the node CryptoGetClaimQuery. If the claim exists, there can be a state proof for that single claim. If the claim doesn't exist, then the state proof must be obtained for the account as a whole, which lists all the attached claims, which then proves that any claim not on the list must not exist.

| Field | Type | Description |
| :--- | :--- | :--- |
| header | [ResponseHeader](../miscellaneous/responseheader.md) | Standard response from node to client, including the requested fields: cost, or state proof, or both, or neither |
| claim | [Claim](cryptoaddclaim.md#claim) | The claim \(account, hash, keys\), or null if there is no Claim with the given hash attached to the given account |

