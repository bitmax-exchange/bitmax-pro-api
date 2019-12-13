## Balance

### Cash Account Balance 

> Cash Account Balance - Sample response 

```json
{
    "code": 0,
    "data": [
        {
            "asset":            "USDT",
            "totalBalance":    "1285.366663467",
            "availableBalance": "1285.366663467"
        },
        {
            "asset":            "BTC",
            "totalBalance":    "22.1308675",
            "availableBalance": "16.1308675"
        },
        {
            "asset":            "ETH",
            "totalBalance":     "0.6",
            "availableBalance": "0.6"
        }
    ]
}
```

**HTTP Request**

`GET <account-group>/api/pro/v1/cash/balance`

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String** 

`<timestamp>+balance`

**Code Sample**

Please refer to python code to[query private balance]{https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_balance.py}

### Margin Account Balance 

> Margin Account Balance - Sample response 

```json
{
    "code": 0,
    "data": [
        {
            "asset":            "USDT",
            "totalBalance":     "11200",
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

`GET <account-group>/api/pro/v1/margin/balance`

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
        "totalBalanceInUSDT":     "17715.8175",
        "totalBorrowedInUSDT":    "0",
        "totalInterestInUSDT":    "0",
        "netBalanceInUSDT":       "17715.8175",
        "pointsBalance":          "0",
        "currentLeverage":        "1",
        "cushion":                "-1"
    }
}
```

**HTTP Request**

`POST <account-group>/api/pro/v1/margin/risk`

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#signing-a-Request) section.

**Prehash String**

`<timestamp>+margin/risk`

**Code Sample**

Please refer to python code to[query private margin risk]{https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_margin_risk.py}


