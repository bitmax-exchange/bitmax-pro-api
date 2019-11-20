## Order Book (Depth)

> Request 

```shell
curl -X GET https://bitmax.io/api/pro/depth?symbol=BTMX/USDT
```

> Sample response 

```json
{
    "m": "depth-snapshot",
    "symbol": "BTMX/USDT",
    "data": {
        "seqnum": 5068757,
        "ts": 1573165838976,
        "asks": [
            [
                "0.06848",
                "4084.2"
            ],
            [
                "0.0696",
                "15890.6"
            ]
        ],
        "bids": [
            [
                "0.06703",
                "13500"
            ],
            [
                "0.06615",
                "24036.9"
            ]
        ]
    }
}
```

#### URL

`GET /api/pro/depth`

#### Request Parameters