### WS: Cancel Order

> Request to cancel existing open order

```json
{
  "op": "req",
  "action": "cancel-Order",
  "account": "cash",
  "args": {
    "time":    1574165050128,
    "id":      "2d4c3fa1e5c249e49f990ce86aebb607",
    "orderId": "16e83845dcdsimtrader00008c645f67",
    "symbol":  "ETH/USDT"
  }
}
```

> Successful ACK message

```json
{
  "m": "order",
  "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
  "ac": "CASH",
  "action": "cancel-order",
  "status": "Ack",
  "info": {
    "symbol":    "ETH/USDT",
    "orderType": "NULL_VAL",
    "timestamp":  1574165050147,
    "id":        "7b73dcd8e8c847d5a99df5ef5ae5088b",
    "orderId":   "16e83845dcdsimtrader00008c645f67"
  }
}
```

> Error response message

```json
{
  "m": "order",
  "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
  "ac": "CASH",
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

Make order cancelling request follow the general websocket request rule by setting `action` to be `cancel-orde`, with proper cancel order parameters as specified in rest api for *args* field.

**Response**

*ACK* 

With *status* field as *Ack* to indicate this cancel order request pass some basic sanity check, and has been sent to matching engine. 

*info* field provide some detail: if you provide *id* in your request, it will be echoed back as *id* to help you idintify; we also echo back target *orderId* to be cancelled.  

*Err*

With *status* field as *Err* to indicate there is some obvisous errors in your cancel order request. 

*info* field provide some detail: if you provide *id* in your request, it will be echoed back as *id* to help you identify; we also provide error *code*, *reason*, and *message* detail.
