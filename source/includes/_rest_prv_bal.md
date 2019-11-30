## Balance

### Cash Account Balance 

> Cash Account Balance - Sample response 

```json
{
    "code": 0,
    "data": [
        {
            "asset":            "USDT",
            "availableBalance": "1285.366663467",
            "totalABalance":    "1285.366663467"
        },
        {
            "asset":            "BTC",
            "availableBalance": "16.1308675",
            "totalABalance":    "22.1308675"
        },
        {
            "asset":            "ETH",
            "availableBalance": "0.6",
            "totalABalance":    "0.6"
        }
    ]
}
```

**HTTP Request**

`GET <account-group>/api/pro/cash/balance`

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String** 

`<timestamp>+balance`


### Margin Account Balance 

> Margin Account Balance - Sample response 

```json
{
    "code": 0,
    "data": [
        {
            "asset":            "USDT",
            "totalABalance":    "11200",
            "availableBalance": "11200",
            "borrowed":         "0",
            "interest":         "0"
        },
        {
            "asset":            "ETH",
            "totalBalance":     "20",
            "availableBalance": "20",
            "borrowed":         "0",
            "interest":         "0"
        }
    ]
}
```

**HTTP Request** 

`GET <account-group>/api/pro/margin/balance`

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#signing-a-Request) section.

**Prehash String** 

`<timestamp>+balance`



### Margin Risk Profile

> Margin Account Risk Profile - Sample response 

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

**HTTP Request**

`POST <account-group>/api/pro/margin/risk`

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#signing-a-Request) section.

**Prehash String**

`<timestamp>+margin/risk`




