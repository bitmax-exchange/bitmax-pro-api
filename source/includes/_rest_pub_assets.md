### List all Assets

> List all Assets

```
curl -X GET https://bitmax.io/api/pro/assets
```

> Sample Response 

```json
{
    "code": 0,
    "data": [
        {
            "assetCode":        "BTMX",
            "assetName":        "BitMax.io Native Token",
            "precisionScale":    9,
            "nativeScale":       2,
            "withdrawalFee":     11,
            "minWithdrawalAmt":  22,
            "status":           "Normal"
        }
    ]
}
```

**HTTP Request** 

`GET /api/pro/assets`

You can obtain a list of all assets listed on the exchange through this API.
