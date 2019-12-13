###
### Place Batch Orders

> Place Batch Orders - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "ac": "CASH",
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
    "ac": "CASH",
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "action": "batch-place-order",
    "code": 300013,
    "info": [
        {
            "code": 300004,
            "id": "nGFdep927xsqSaL2B4R3jDSm1IGwcfmr",
            "message": "Notional is too small.",
            "reason": "INVALID_NOTIONAL",
            "symbol": "BTC/USDT"},
            {"code": 300013,
            "id": "PGEcSVsoQWythsYTs2hWfogLoRs6hhi8",
            "message": "Some invalid order in this batch.",
            "reason": "INVALID_BATCH_ORDER",
            "symbol": "ETH/USDT"}],
    "message": "Batch Order failed, please check each order info for detail.",
    "reason": "INVALID_BATCH_ORDER",
    "status": "Err"
}
```

Place multiple orders in a batch. If some order in the batch failed our basic check, then the whole batch request fail.

You may submit up to 10 orders at a time. Server will respond with error if you submit more than 10 orders.

**HTTP Request**

`POST <account-group>/api/pro/v1/{account-category}/order/batch`

Set `account-category` to`cash` for cash account and `margin` for margin account.

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String**

`<timestamp>+order/batch`

**Response**

*ACK*

0 for `code` and status `Ack` to indicate the batch order request is accepted by server. Field "info" includes server generated "coid" for each order in the batch request, and this is the id you should use for future status query.

`data` schema:

Name        |  Type    | Description
------------| ---------| -------- 
`ac`        | `String` | `CASH`, `MARGIN`
`accountId` | `String` | account Id
`action`    | `String` | `cancel-all`
`status`    | `String` |  `Ack` 
`info`      | `List`   | See below for detail

`info` schema:

Name       |  Type    | Description
-----------| ---------| -------- 
`id`       | `String` | echo back the `id` in request
`orderId`  | `String` | server assigned order Id for this single order
`orderType`| `String` | order type
`symbol`   | `String` | `symbol` in request
`timestamp`| `Long`   | server received timestamp

*ERR*

Non 0 `code` and status `ERR` to indicate the batch order request is accepted by server. Field `info` includes detailed order information to explain why the batch request fail for each individual order. "coid" is original order id provided by user for each order.

Error schema

Name        |  Type    | Description
------------| ---------| -------- 
`code`      | `Long`   | 0
`ac`        | `String` | `CASH`, `MARGIN`
`accountId` | `String` | account Id
`action`    | `String` | `batch-cancel-order`
`message`   | `String` | error message detail
`reason`    | `String` | short error message 
`status`    | `String` |  `Err` 
`info`      | `List`   | See below for detail

`info` schema:

Name        |  Type    | Description
------------| ---------| -------- 
`code`      | `Long`   | 0
`id`        | `String` | echo `id` in request
`orderId`   | `String` | empty
`message`   | `String` | error message detail
`reason`    | `String` | short error message 
`symbol`    | `String` | symbol in order

**Code Sample**

Please refer to python code to [place batch order](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/place_order.py)
