### WS: Recent Market Trades 

> Requesting the most recent 12 trades for symbol BTMX/USDT

```json
{ "op": "req", "action": "market-trades", "args": { "symbol": "BTMX/USDT", "level": 12} }
```

> Trades snapshot message

```json
{
    "m": "market-trades",
    "id": "abcd1334",
    "symbol": "BTMX/USDT",
    "data": [
        {
            "p":      "0.068600",
            "q":      "100.000",
            "ts":      1573069903254,
            "bm":      false,
            "seqnum":  144115188077966308
        }
    ]
}
```

You can request the current order book via websocket by an `market-trades` request. 

The request schema:

 Name          | Data Type           | Description                
-------------- | ------------------- | -------------------------- 
 `op`          | `String`            | `req`                      
 `action`      | `String`            | `market-trades`           
`args`         | `{key:value}`       | see `args` below for detail

The `args` schema:

 `symbol` | `String`            | Symbol, e.g. `BTMX/USDT`  
 `level`  | Int                 | Number of trades to request

The response schema:

 Name          | Data Type             | Description                   
-------------- | --------------------- | ----------------------------- 
 `m`           | `String`              | `market-trades`
 `symbol`      | `String`              | Symbol, e.g. `BTMX/USDT`      
 `data`        | `Json Array`          | A list of trade json objects                              

The `data` field is a list containing one or more trade objects. The server may combine consecutive trades with the same price and `bm` 
value into one aggregated item. Each trade object contains the following fields:


 Name     | Type       | Description                                                                                    
--------- | ---------- | ---------------------------------------------------------------------------------------------- 
 `seqnum` | `Long`     | the sequence number of the trade record. `seqnum` is always increasing for each symbol, but may not be consecutive 
 `p`      | `String`   | the executed price expressed as a string                                                       
 `q`      | `String`   | the aggregated traded amount expressed as string                                               
 `ts`     | `Long`     | the UTC timestamp in milliseconds of the first trade                                           
 `bm`     | `Boolean`  | if true, the buyer of the trade is the maker.     