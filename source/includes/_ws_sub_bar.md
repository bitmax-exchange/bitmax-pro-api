### Channel: Bar Data 

> Subscribe to `BTMX/USDT` 1 minute bar stream

```json
{ "op": "sub", "id": "abc123", "ch":"bar:1:BTMX/USDT" }
```

> Unsubscribe to `BTMX/USDT` 1 minute bar stream

```json
{ "op": "unsub", "id": "abc123", "ch":"bar:1:BTMX/USDT" }

//  Alternatively, you can unsubscribe all bar streams for BTMX/USDT
{ "op": "unsub", "id": "abc123", "ch":"bar:*:BTMX/USDT" }

// Or unsubscribe all 1 minute bar stream
{ "op": "unsub", "id": "abc123", "ch":"bar:1" }

// Or unsubscribe all bar stream
{ "op": "unsub", "id": "abc123", "ch":"bar" }
```

> Bar Data Message 

```json
{
    "m": "bar",
    "s": "BTMX/USDT",    
    "data": {
        "i":  "1",
        "ts": 1575398940000,
        "o":  "0.04993",
        "c":  "0.04970",
        "h":  "0.04993",
        "l":  "0.04970",
        "v":  "8052"
    }
}
```

The `data` field is a list containing one or more trade objects. The server may combine consecutive trades with the same price and `bm` 
value into one aggregated item. Each trade object contains the following fields:

 Name     | Type       | Description                                                                                    
--------- | ---------- | ---------------------------------------------------------------------------------------------- 
 `seqnum` | `Long`     | the sequence number of the trade record. `seqnum` is always increasing for each symbol, but may not be consecutive 
 `p`      | `String`   | the executed price expressed as a string                                                       
 `q`      | `String`   | the aggregated traded amount expressed as string                                               
 `ts`     | `Long`     | the UTC timestamp in milliseconds of the first trade                                           
 `bm`     | `Boolean`  | if true, the buyer of the trade is the maker.

