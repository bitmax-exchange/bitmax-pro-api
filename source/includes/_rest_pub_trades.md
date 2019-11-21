## Market Trades

> Request 

```
curl -X GET https://bitmax.io/api/pro/trades?symbol=BTMX/USDT
```

> Sample response 

```json
{
    "code": 0,
    "data": {
        "trades": [
            {
                "bm": false,               // is buyer maker?
                "id": 144115191800016553,
                "p": "0.06762",            
                "q": "400",
                "ts": 1573165890854
            },
            {
                "bm": true,
                "id": 144115191800070421,
                "p": "0.06797",
                "q": "341",
                "ts": 1573166037845
            }
        ],
        "m": "trades",
        "symbol": "BTMX/USDT"
    }
}
```

**HTTP Request**

`GET /api/pro/trades`

