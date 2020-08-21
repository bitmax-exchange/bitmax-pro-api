### Channel: Level 2 Order Book Updates

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

See [Orderbook Snapshot](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/websocket_orderbook_snapshot.py) for code examples.

