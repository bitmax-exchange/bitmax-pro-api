###
### Place Batch Orders

> Place Batch Orders - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "batch-place-order",
        "info": [
            {
                "id":        "0r9LFylwSF3Pj6vOQC4j33Nv2pQnuFD9",
                "orderId":   "16e80b75cbda8bXHbAwwoqDoa5be7384",
                "orderType": "Limit",
                "symbol":    "BTC/USDT",
                "timestamp":  1573596819185
            },
            {
                "id":        "mYnbq6xcTLdAs9qzq1tY57lUZ1iWWIac",
                "orderId":   "16e61adeee5a8bXHbAwwoqDo100e364e",
                "orderType": "Limit",
                "symbol":    "BTC/USDT",
                "timestamp":  1573596819185
            }
        ],
        "status": "Ack"
    }
}
```

> Place Batch Orders - Error Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "batch-place-order",
        "info": [
            {
                "code":     300013,
                "id":      "N7PxdMH8iGWiCZOau14i3SGLEzfZpO06",
                "message": "Some invalid order in this batch",
                "reason":  "INVALID_BATCH_ORDER",
                "symbol":  "ETH/USDT"
            },
            {
                "code":     300004,
                "id":      "R1LWczhWvAP3DGTEfAOzD3XmXybywXiC",
                "message": "Notional is too small.",
                "reason":  "INVALID_NOTIONAL",
                "symbol":  "BTC/USDT"
            }
        ],
        "status": "Err"
    }
}
```

Place multiple orders in a batch. If some order in the batch failed our basic check, then the whole batch request fail.

You may submit up to 10 orders at a time. Server will respond with error if you submit more than 10 orders.

**HTTP Request**

`POST <account-group>/api/pro/{account-category}/order/batch`

Set `account-category` to`cash` for cash account and `margin` for margin account.

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String**

`<timestamp>+order/batch`

**Response**

*ACK*

Status "Ack" to indicate the batch order request is accepted by server. Field "info" includes server generated "coid" for each order in the batch request, and this is the id you should use for future status query.

*ERR*

Status "ERR" to indicate the batch order request is accepted by server. Field "info" includes detailed order information to explain why the batch request fail for each individual order. "coid" is original order id provided by user for each order.


**Code Sample**

Please refer to python code to [place batch order](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/place_order.py)
