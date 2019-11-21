## Market Trades

> Request 

```
curl -X GET /api/pro/trades?symbol=BTMX/USDT
```

> Sample response 

```json
{
    "code": 0,
    "data": {
        "m": "trades",
        "symbol": "BTMX/USDT",
        "trades": [
            {
                "id": 144115191800016553,
                "p": "0.06762",            
                "q": "400",
                "ts": 1573165890854,
                "bm": false               // is buyer maker?
            },
            {
                "id": 144115191800070421,
                "p": "0.06797",
                "q": "341",
                "ts": 1573166037845,
                "bm": true
            }
        ]
    }
}
```

**HTTP Request**

`GET /api/pro/trades`

#### Request Parameters

   Name    | Type    | Required | Value Range                           | Description
---------- | ------- | -------- | ------------------------------------- |---------------
 `symbol`  | String  | Yes      |  Valid symbol supported by exchange   | 
 `n`       | Int     | No       |  any positive integer, capped at 100  | number of trades to return.


#### Response Content 

   Name    | Type       | Description 
---------- | ---------- | -----------------------------
  `seqnum` | `Long`     | the sequence number of the trade record. `seqnum` is always increasing for each symbol, but may not be consecutive 
  `p`      | `String`   | trade price in string format 
  `q`      | `String`   | trade size in string format
  `ts`     | `Long`     | UTC timestamp in milliseconds
  `bm`     | `Boolean`  | If true, the maker of the trade is the buyer. 
