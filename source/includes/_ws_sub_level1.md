### Channel: Level 1 Order Book Data (BBO)

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
    "symbol": "BTC/USDT",
    "data": {
        "ts": 1573068442532,
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

