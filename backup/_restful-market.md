# RESTful APIs - Public



## Get Market Trades

> Response example (symbol=BTC/USDT, n=2) 

```json
{
  "m": "marketTrades",
  "s": "BTC/USDT",
  "trades": [
    {
     "bm": True,
     "id": 72057594043333564,
     "p":  "11406.35",
     "q":  "0.0305710",
     "t":  1565646523666
    },
    {
     "bm": True,
     "id": 72057594043333566,
     "p":  "11406.00",
     "q":  "1.4226290",
     "t":  1565646523666
    }
  ]
}
 ```

**HTTP Request**

`GET api/v2/trades/symbol=<symbol>&n=<n>`

**Parameters**

Name   | Data Type | Description
------ | --------- | -----------------
symbol | String    | a valid smbol, e.g. `symbol=ETH-BTC`
n      | Int       | number of trades to be included in the response. n is currently limited to 100 or fewer. e.g. `n=10` 

Each element in `trades` is an object containing recent trade data with the following fields:

Field    | Data Type | Description
-------- | --------- | ---------------------------------------
`bm`     | Boolean   | if `true`, the buyer of the trade is the market maker 
`id`     | Long      | Unique ID of the market trade
`p`      | String    | price
`q`      | String    | quantity 
`t`      | Long      | timestamp 

















