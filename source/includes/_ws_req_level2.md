### WS: Orderbook Snapshot

> Requesting the current order book snapshot

```json
{ "op": "req", "id": "abcdefg", "action": "depth-snapshot", "args": { "symbol": "BTMX/USDT" } }
```

> Depth snapshot message

```json
{
    "m": "depth-snapshot",
    "symbol": "BTMX/USDT",
    "data": {
        "seqnum": 3167819629,
        "ts": 1573142900389,
        "asks": [
            [
                "0.06758",
                "585"
            ],
            [
                "0.06773",
                "8732"
            ]
        ],
        "bids": [
            [
                "0.06733",
                "667"
            ],
            [
                "0.06732",
                "750"
            ]
        ]
    }
}
```

You can request the current order book via websocket by an `depth-snapshot` request.

The `args` schema:

 Name          | Data Type           | Description
-------------- | ------------------- | -------------------------- 
 `op`          | `String`            | `req`
 `action`      | `String`            | `depth-snapshot`
 `id`          | `String`            | echo back in case of error
 `args:symbol` | `String`            | Symbol, e.g. `BTMX/USDT`

The response schema:

 Name          | Data Type             | Description
-------------- | --------------------- | -----------------------------
 `m`           | `String`              | `depth-snapshot`
 `symbol`      | `String`              | Symbol, e.g. `BTMX/USDT`  
 `data:seqnum` | `Long`                |
 `data:ts`     | `Long`                | UTC Timestamp in milliseconds
 `data:asks`   | `[[String, String]]`  | List of (price, size) pair
 `data:bids`   | `[[String, String]]`  | List of (price, size) pair

You can following the steps below to keep track of the the most recent order book:

* Connecting to WebSocket Stream
* Subscribe to the depth update stream, see [Level 2 Order Book Updates (Depth)](#level-2-order-book-updates-depth).
* Send a `depth-snapshot` request to the server.
* Once you obtain the snapshot message from the server, initialize the snapshot.
* Using consequent `depth` messages to update the order book.

Please note that field `seqnum` should strictly increase by 1 for each new depth update (each `symbol` maintain its own `seqnum`). 
If you see a larger than 1 gap from previous `seqnum` (for the same `symbol`), then there might be data loss, 
you need to repeat above steps to maintain a new order book.

The `depth-snapshot` message is constructed in a consistent way with all `depth` message. 

Please note that the `depth-snapshot` API has higher latency. The response time is usually between 
1000 - 2000 milliseconds. It is intended to help you initialize the orderbook, not to be used to obtain 
the timely order book data. 

More comprehensive examples can be found at:

* Python: [websocket orderbook snapshot](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/websocket_orderbook_snapshot.py)
