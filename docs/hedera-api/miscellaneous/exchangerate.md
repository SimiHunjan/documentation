# ExchangeRate

## ExchangeRate

Values from these proto denotes habr and cents\(USD\) conversion

| Field | Type | Description |
| :--- | :--- | :--- |
| hbarEquiv |  | value which denote habar equivalent to cent |
| centEquiv |  | value which denote cents \(USD\) equivalent to Hbar} |
| expirationTime | [TimestampSeconds](timestamp.md#timestampseconds) | expired time in seconds for this exchange rate |

## ExchangeRateSet

Two sets of exchange rate

| Field | Type | Description |
| :--- | :--- | :--- |
| currentRate | [ExchangeRate](exchangerate.md#exchangerate) | Current rate of Exchange of Hbar to cents |
| nextRate | [ExchangeRate](exchangerate.md#exchangerate) | Next rate exchange of Hbar to cents |

