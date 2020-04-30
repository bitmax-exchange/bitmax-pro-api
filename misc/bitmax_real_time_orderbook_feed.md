# WebSocket - Real-time Level 2 Order Book Update 

In addition to the regular `depth` channel,  you shall subscribe to the `depth-realtime` channel for data feed with loweMX/USDTcy.
If the request is successful, you will receive the full orderbook in the WebSocket: 

    {
      "m": "depth-snapshot-realtime",
      "symbol": "BTMX/USDT",
      "data": {
        "ts": 0,
        "seqnum": 33346,
        "asks": [
          ["0.045", "3350"],
          ["0.044", "4760"],
        ],
        "bids": [
          ["0.043", "2720"],
          ["0.042", "9600"],
       ]
      }
    }

If the request failed, you will receive an ack message with non-zero value `code`.

    {
      "m": "depth-snapshot-realtime",
      "id": "ec1L5cDt",
      "code": 100008,
      "reason": "SYMBOL_ERROR",
      "info": "Unable to handle symbol USDT/BTMX, expecting BTC-PERP"
    }



The main difference between the two channels is that the `depth` channel streams throttled data by aggregating updates using 300 millisecond 
intervals while `depth-realtime` streams the unthrottled data feed. As a result, the amount of data from the `depth` channel will be lighter.


## Subscribe to Real-time Order Book Updates

Subscribing to the real-time depht channle is similar to subscribing the regular `depth` channel. 

To subscribe to `BTMX/USDT` real-time depth update stream, send a json messge to the server:

    {
      "op": "sub",
      "id": "abc123", // optional
      "ch": "depth-realtime:BTMX/USDT"
    }

In the above message, the `id` field is an optional string field. If an string value is provided, the server will echo back the `id` field 
in the ack message. It is recommended to always include an `id` field in the request.

If the subscription is successful, you will receive an ack message with `code=0`: 

    {
      "m": "sub",
      "ch": "depth-realtime:BTMX/USDT",
      "id": "abc123",
      "code": 0
    }

If the subscription failed, you will receive an ack message with non-zero `code` value, for instance:

    {
      "m": "sub",
      "ch": "depth-realtime:BTMX/USDT",
      "id": "abc123",
      "code": 100008,
      "reason": "Unable to handle symbol USDT/BTMX"
    }


## Data Stream 

Once subscribed to the `depth-realtime` channel, you will start receiving updates in json format:

    {
      "m": "depth-realtime",
      "symbol": "BTMX/USDT",
      "data": {
        "ts": 1573069021376,
        "seqnum": 2097965,
        "asks": [
          [
            "0.06844", // price
            "10760" // size
          ]
        ],
        "bids": []
      }
    }

Here:

* `ts` - the UTC timestamp in milliseconds
* `seqnum` - a sequence number of long integer type. It is continuous for each WebSocket session. 
* `asks` - see below.
* `bids` - see below.

Each `depth-realtime` message contains a `bids` list and an `asks` list in its `data` field. Each list contains a series of `[price, size]` pairs 
you can use to update the order book snapshot. You should use the following rules to update the orderbook:

* if `size` is positive and the `price` doesn't exist in the current order book, you should **add** a new level `[price, size]`. 
* if `size` is positive and the `price` exists in the current order book, you should **update** the existing level to `[price, size]`. 
* if `size` is zero, you should **delete** the level at `price`. 

## Requesting the Full Orderbook 

To request a full orderbook of `BTMX/USDT`, send a `depth-snapshot-realtime` request in json format to the server via WebSocket.

    {
      "op": "req",
      "id": "Q9rK5r74",  // optional
      "action": "depth-snapshot-realtime",
      "args": {
        "symbol": "BTMX/USDT"
      }
    }

If the request is successful, you will receive the full orderbook in the WebSocket: 

    {
      "m": "depth-snapshot-realtime",
      "symbol": "BTMX/USDT",
      "data": {
        "ts": 0,
        "seqnum": 33346,
        "asks": [
          ["0.045", "3350"],  // price, size
          ["0.044", "4760"],
        ],
        "bids": [
          ["0.043", "2720"],
          ["0.042", "9600"],
       ]
      }
    }

If the request failed, you will receive an ack message with non-zero `code` value, for instance:

    {
      "m": "depth-snapshot-realtime",
      "id": "ec1L5cDt",
      "code": 100008,
      "reason": "SYMBOL_ERROR",
      "info": "Unable to handle symbol USDT/BTMX, expecting BTC-PERP"
    }


If you are already subscribed to the `depth-realtime` channel, our server guarentees that the order of the `depth-snapshot-realtime` message and 
`depth-snapshot` messages. When you receive the `depth-snapshot-realtime` message, you can reset your cached orderbook using the snapshot data 
and update the cached orderbook with following `depth-realtime` updates.

