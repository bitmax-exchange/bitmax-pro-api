## Sending Data Request via WebSocket


### Orderbook Snapshot

> Requesting the current order book snapshot

```json
{ "op": "req", "action": "depth-snapshot", "args": { "symbol": "BTMX/USDT" } }
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
 `args:symbol` | `String`            | Symbol, e.g. `BTMX/USDT`   

The response schema:

 Name          | Data Type             | Description                   
-------------- | --------------------- | ----------------------------- 
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

The `depth-snapshot` message is constructed in a consistent way with all `depth` message. 

Please note that the `depth-snapshot` API has higher latency. The response time is usually between 
1000 - 2000 milliseconds. It is intended to help you initialize the orderbook, not to be used to obtain 
the timely order book data. 

More comprehensive examples can be found at:

* Python: [https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/websocket_orderbook_snapshot.py](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/websocket_orderbook_snapshot.py)


### Trades Snapshot


## Sending Order Request via WebSocket

###
###Place Order 

> Request to place new order

```json
{
    "op": "req",
    "action": "place-Order",
    "args": {
        "time":        1573772908483,
        "coid":       "11eb9a8355fc41bd9bf5b08bc0d18f6b",
        "symbol":     "EOS/USDT",
        "orderPrice": "3.27255",
        "orderQty":   "30.557210737803853",
        "orderType":  "limit",
        "side":       "buy",
        "postOnly":    false,
        "respInst":   "ACK"
    }
}
```

> Successful ACK message

```json
{
    "m": "order",
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "action": "place-order",
    "status": "Ack",
    "info": {
        "symbol":    "ETC/USDT",
        "orderType": "Market",
        "timestamp":  1573623067556,
        "id":        "8a7612a36ab44766abec4bbb45fd84ea",
        "orderId":   "16e83845dcdsimtrader00008c645f67"
    }
}
```

> Error response message

```json
{
    "m": "order",
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "action": "place-order",
    "status": "Err",
    "info": {
        "id":      "69c482a3f29540a0b0d83e00551bb623",
        "symbol":  "ETH/USDT",
        "code":     300011,
        "message": "Not Enough Account Balance",
        "reason":  "INVALID_BALANCE"
    }
}
```

Place order via websocket 

**Request**

Make new order request follow the general websocket request rule, with proper place new order parameters as specified in rest api for *args* field.

**Response**

Respond with *m* field as *order*, and *action* field as *place-order*; *status* field to indicate if this is a successful *Ack* or failed *Err*.

*ACK* 

With *status* field as *Ack* to indicate this new order request pass some basic sanity check, and has been sent to matching engine. 

*info* field provide some detail: if you provide *id* in your request, it will be echoed back as *id* to help you identify; we also provide server side generated *orderId*, which is the id you should use for future track or action on the order.  


*ERR* 

With *status* field as *Err* to indicate there is some obvisous errors in your order. 

*info* field provide some detail: if you provide *id* in your request, it will be echoed back as *id* to help you identify; we also provide error *code*, *reason*, and *message* detail.

### 
###Cancel Order

> Request to cancel existing open order

```json
{"op": "req", 
"action": "cancel-Order", 
"args": {
    "time":     1574165050128, 
    "id":      "2d4c3fa1e5c249e49f990ce86aebb607", 
    "orderId": "16e83845dcdsimtrader00008c645f67", 
    "symbol":  "ETH/USDT"
    }
}
```

> Successful ACK message

```json
{"m": "order", 
"accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo", 
"action": "cancel-order", 
"status": "Ack", 
"info": {
    "symbol":    "ETH/USDT", 
    "orderType": "NULL_VAL", 
    "timestamp":  1574165050147, 
    "id":        "7b73dcd8e8c847d5a99df5ef5ae5088b", 
    "orderId":   "16e83845dcdsimtrader00008c645f67"}}
```

> Error response message

```json
{"m": "order", 
"accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo", 
"action": "cancel-order", 
"status": "Ack", 
"info": {
    "code":     300006,
    "id":      "x@fabs",
    "message": "Invalid Client Order Id: x@fabs",     
    "symbol":  "ETH/USDT", 
    "reason":  "INVALID_ORDER_ID"
    }
}
```

Cancel an existing open order via websocket 

**Request**

Make order cancelling request follow the general websocket request rule, with proper cancel order parameters as specified in rest api for *args* field.

**Response**

*ACK* 

With *status* field as *Ack* to indicate this cancel order request pass some basic sanity check, and has been sent to matching engine. 

*info* field provide some detail: if you provide *id* in your request, it will be echoed back as *id* to help you idintify; we also echo back target *orderId* to be cancelled.  

*Err*

With *status* field as *Err* to indicate there is some obvisous errors in your cancel order request. 

*info* field provide some detail: if you provide *id* in your request, it will be echoed back as *id* to help you identify; we also provide error *code*, *reason*, and *message* detail.

### 
###Cancel All Order

> Request to cancel all existing open orders 

```json
{
    "op": "req",
    "action": "cancel-All",
    "args": {}
}
```

> Request to cancel existing open order related to symbol "BTC/USDT"

```json
{
    "op": "req",
    "action": "cancel-All",
    "args": {
        "symbol": "BTC/USDT"
    }
}
```

> Successful ACK message

```json
{
    "m": "order",
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "action": "cancel-all",
    "status": "Ack",
    "info": {
        "symbol":    "",
        "orderType": "NULL_VAL",
        "timestamp":  1574165159732,
        "id":        "69c482a3f29540a0b0d83e00551bb623",
        "orderId":   ""
    }
}
```

Cancel all open orders via websocket with optional symbol.

**Request**

Make general websocket request with *action* field as *cancel-All*, and provide *time* value in *args*.

**Response**

With *status* field as *Ack* to indicate this cancel all order request has been received by server and sent to matching engine. 

*info* field provide some detail: if you provide *id* in your request, it will be echoed back as *id* to help you match ack with request.
