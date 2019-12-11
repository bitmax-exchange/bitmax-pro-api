
###
### Cancel Batch Orders

> Cancel Batch Orders - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountCategory": "CASH",
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "batch-cancel-order",
        "status": "Ack",
        "info": [
            {
                "id":        "0a8bXHbAwwoqDo3b485d7ea0b09c2cd8",
                "orderId":   "16e61d5ff43s8bXHbAwwoqDo9d817339",
                "orderType": "NULL_VAL",
                "symbol":    "BTC/USDT",
                "timestamp":  1573619097746
            },
            {
                "id":        "0a8bXHbAwwoqDo7d303e2edf6c26d1be",
                "orderId":   "16e61adeee5a8bXHbAwwoqDo100e364e",
                "orderType": "NULL_VAL",
                "symbol":    "ETH/USDT",
                "timestamp":  1573619098342
            }
        ]
    }
}
```

> Cancel Batch Orders - Error Response (Status 200, code 0)

```json
{
    "code": 300013,
    "accountCategory": "CASH",
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "action": "batch-place-order", 
    "message": "Batch Order failed, please check each order info for detail.",
    "reason": "INVALID_BATCH_ORDER",
    "status": "Err", 
    "info": [
        {
            "code":     300006,
            "id":      "NUty15oXcNt9JAngZ1D6q6jY15LOpKPC",
            "orderId": "16e61d5ff43s8bXHbAwwoqDo9d817339",
            "message": "The order is already filled or canceled.",
            "reason":  "INVALID_ORDER_ID",
            "symbol":   ""
        },
        {
            "code":     300006,
            "id":      "mpoL0q8cheL8PL2UstJFRzp6yuPk1sGc",
            "orderId": "16e61adeee5a8bXHbAwwoqDo100e364e",
            "message": "The order is already filled or canceled.",
            "reason":  "INVALID_ORDER_ID",
            "symbol":   ""
        }
    ]
}
```

Cancel multiple orders in a batch. If some order in the batch failed our basic check, then the whole batch request failed.

**HTTP Request**

`DELETE <account-group>/api/pro/{account-category}/order/batch`

Set `account-category` to`cash` for cash account and `margin` for margin account. 

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String**

`<timestamp>+order/batch`

**Response**

*ACK*

Response with status "Ack" to indicate batch is received by server and pass some basic check.

*ERR* 

Response with status "Err" to explain detailed failure reason for each order in the batch request.


**Code Sample**

please refer to python code to [cancel batch order](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/cancel_order.py)
