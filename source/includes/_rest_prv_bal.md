## Balance

### Cash Account Balance 

> Sample response 

```json
{
    "code": 0,
    "data": [
        {
            "asset":           "USDT",
            "availableAmount": "1285.366663467",
            "totalAmount":     "1285.366663467"
        },
        {
            "asset":           "BTC",
            "availableAmount": "16.1308675",
            "totalAmount":     "22.1308675"
        },
        {
            "asset":           "ETH",
            "availableAmount": "0.6",
            "totalAmount":     "0.6"
        }
    ]
}
```

**URL** `https://bitmax.io/api/pro/cash/balance`


### Margin Account Balance 

> Sample response 

```json
{
    "code": 0,
    "data": [
        {
            "asset":            "USDT",
            "availableBalance": "11200",
            "borrowedBalance":  "0",
            "interest":         "0",
            "totalAmount":      "11200"
        },
        {
            "asset":            "ETH",
            "availableBalance": "20",
            "borrowedBalance":  "0",
            "interest":         "0",
            "totalAmount":      "20"
        }
    ]
}
```

**URL** `https://bitmax.io/api/pro/margin/balance`


### Margin Account Risk Profile

> Sample response 

```json
{
    "code": 0,
    "data": {
        "accountMaxLeverage":     "10",
        "availableBalanceInUSDT": "17715.8175",
        "currentLeverage":        "1",
        "cushion":                "-1",
        "netBalanceInUSDT":       "17715.8175",
        "pointsBalance":          "0",
        "totalBalanceInUSDT":     "17715.8175",
        "totalBorrowedInUSDT":    "0",
        "totalInterestInUSDT":    "0"
    }
}
```

**URL** `https://bitmax.io/api/pro/margin/risk`


