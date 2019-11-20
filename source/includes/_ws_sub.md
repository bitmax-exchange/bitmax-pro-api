## Subscribing Data Channels


### Level 1 Order Book Data (BBO)

> Subscribe to `BTMX/USDT` quote stream

```json
{ "op": "sub", "id": "abc123", "ch":"bbo:BTMX/USDT" }
```

> Unsubscribe to `BTMX/USDT` quote stream

```json
{ "op": "unsub", "id": "abc123", "ch":"bbo:BTMX/USDT" }
```

> BBO Message 

```json
{
    "m": "bbo",
    "ts": 1573068442532,
    "symbol": "BTC/USDT",
    "data": {
        "bid": [
            "9309.11",
            "0.0197172"
        ],
        "ask": [
            "9309.12",
            "0.8851266"
        ]
    }
}
```

You can subscribe to updates of best bid/offer data stream only. Once subscribed, you will receive BBO message whenever 
the price and/or size changes at the top of the order book. 

Each BBO message contains price and size data for exactly one bid level and one ask level. 



### Level 2 Order Book Updates (Depth)

> Subscribe to `BTMX/USDT` depth updates stream

```json
{ "op": "sub", "id": "abc123", "ch":"depth:BTMX/USDT" }
```

> Unsubscribe to `BTMX/USDT` depth updates stream

```json
{ "op": "unsub", "id": "abc123", "ch":"depth:BTMX/USDT" }
```

> The Depth Message 

```json
{
    "m": "depth",
    "symbol": "BTMX/USDT",
    "data": {
        "ts": 1573069021376,
        "seqnum": 2097965,
        "asks": [
            [
                "0.06844",
                "10760"
            ]
        ],
        "bids": [
            [
                "0.06777",
                "562.4"
            ],
            [
                "0.05",
                "221760.6"
            ]
        ]
    }
}
```

If you want to keep track of the most recent order book snapshot in its entirety, the most efficient way is to subscribe to the `depth` channel. 

Each `depth` message contains a `bids` list and an `asks` list in its `data` field. Each list contains a series of `[price, size]` pairs that 
you can use to update the order book snapshot. In the message, `price` is always positive and `size` is always non-negative. 

* if `size` is positive and the `price` doesn't exist in the current order book, you should **add** a new level `[price, size]`. 
* if `size` is positive and the `price` exists in the current order book, you should **update** the existing level to `[price, size]`. 
* if `size` is zero, you should **delete** the level at `price`. 

See [Orderbook Snapshot](#orderbook-snapshot) for code examples.



### Market Trades 

> Subscribe to `BTMX/USDT` market trades stream

```json
{ "op": "sub", "id": "abc123", "ch":"trades:BTMX/USDT" }
```

> Unsubscribe to `BTMX/USDT` market trades stream

```json
{ "op": "unsub", "id": "abc123", "ch":"trades:BTMX/USDT" }
```

> Trade Message 

```json
{
    "m": "trades",
    "symbol": "BTMX/USDT",
    "data": [
        {
            "p": "0.068600",
            "q": "100.000",
            "ts": 1573069903254,
            "bm": false,
            "id": 144115188077966308
        }
    ]
}
```

The `data` field is a list containing one or more trade objects. The server may combine consecutive trades with the same price and `bm` 
value into one aggregated item. Each trade object contains the following fields:

 Name  | Type             | Description                                                                                    
-------| ---------------- | ---------------------------------------------------------------------------------------------- 
 `id`  | `Long`           | the sequence number of the trade record. `id` is always increasing, but may not be consecutive 
 `p`   | `String`         | the executed price expressed as a string                                                       
 `q`   | `String`         | the aggregated traded amount expressed as string                                               
 `ts`  | `Long`           | the UTC timestamp in milliseconds of the first trade                                           
 `bm`  | `Boolean`        | if true, the buyer of the trade is the maker.                                                  


### Account Order

Order update stream is supported on both *account* and *account + symbol* level.

For account level, you could specify account category `cash`, `margin`, or specific account id.

If you already subscribe to *account* level, you cannot subject to *symbol* level. In order to change to *account + symbol* level, unsubscribe from *account* level first, then subscribe to symbol level.

> Subscribe to `cash` account order update stream

```json
{ "op": "sub", "id": "abc123", "ch":"order:cash" }
```

> Subscribe to specific account id *cshQtyfq8XLAA9kcf19h8bXHbAwwoqDoaccount* for order update stream

```json
{ "op": "sub", "id": "abc123", "ch":"order:cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo" }
```

> Subscribe to `cash` account and symbol `BTMX/USDT` order update stream

```json
{ "op": "sub", "id": "abc123", "ch":"order:cash:BTMX/USDT" }
```

> Unsubscribe from `cash` account order update stream

```json
{ "op": "unsub", "id": "abc123", "ch":"order:cash" }
```

> Unsubscribe from `cash` account and symbol `BTMX/USDT` order update stream

```json
{ "op": "unsub", "id": "abc123", "ch":"order:cash:BTMX/USDT" }
```

> Order update message

```json
{
    "m": "order", 
    "accountId": "simtrader0000", 
    "data": {
        "s": "ETC/USDT", 
        "orderId": "16e85af7bc8simtrader0000fb6255dd", 
        "t": 1574200900684, 
        "st": "New", 
        "p": "100.8365", 
        "q": "9.91704", 
        "fp": "0", 
        "fq": "0", 
        "fee": "0", 
        "fa": "base", 
        "bb": "0", 
        "bpb": "0", 
        "qb": "115137.964757493", 
        "qpb": "114136.965153929"
    }
}
```

The `data` field is a single order udpate object.  Each order update object contains the following fields:

Name     | Type | Description                                                                                    
---------| -----| ---------------------------------
`s`      | `String` | symbol
`orderId`| `String` | order id
`t`      | `Long`   | timestamp
`st`     | `String` | order status
`p`      | `String` | order price
`q`      | `String` | order quantity
`fp`     | `String` | filled price
`fq`     | `String` | filled qty
`fee`    | `String` | commission
`fa`     | `String` | fee asset
`bb`     | `String` | base asset total balance
`bpb`    | `String` | base asset available balance
`qb`     | `String` | quote asset total balance
`qpb`    | `String` | quote asset available balance

