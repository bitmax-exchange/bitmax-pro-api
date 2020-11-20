###
### Query Order

> Query Order - Successful Response (Status 200, code 0)

```json
{
    "code": 0,
    "accountCategory": "CASH",
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "data": [
        {
            "symbol":       "BTC/USDT",
            "price":        "8130.24",
            "orderQty":     "0.00082",
            "orderType":    "Limit",
            "avgPx":        "7391.13",
            "cumFee":       "0.005151618",
            "cumFilledQty": "0.00082",
            "errorCode":    "",
            "feeAsset":     "USDT",
            "lastExecTime": 1575953134011,
            "orderId":      "a16eee206d610866943712rPNknIyhH",
            "seqNum":       2622058,
            "side":         "Buy",
            "status":       "Filled",
            "stopPrice":    "",
            "execInst":     "NULL_VAL"
        },
        {
            "symbol":       "BTC/USDT",
            "price":        "8131.22",
            "orderQty":     "0.00082",
            "orderType":    "Market",
            "avgPx":        "7392.02",
            "cumFee":       "0.005152238",
            "cumFilledQty": "0.00082",
            "errorCode":    "",
            "feeAsset":     "USDT",
            "lastExecTime": 1575953151764,
            "orderId":      "a16eee20b6750866943712zWEDdAjt3",
            "seqNum":       2623469,
            "side":         "Buy",
            "status":       "Filled",
            "stopPrice":    "",
            "execInst":     "NULL_VAL"
        }
    ]
}
```

Query order status, either open or history order.

#### HTTP Request

`GET <account-group>/api/pro/v1/{account-category}/order/status?orderId={orderId}`

Set `account-category` to`cash` for cash account and `margin` for margin account. 

#### Request Parameters

Name       | Type      | Required | Value Range                              | Description
-----------| --------- | -------- | ---------------------------------------- | ---------------
`orderId`  | `String`  |  No      | one or more order Ids separated by comma | 


`orderId` could be a single order Id, or multiple order Ids separated by a comma (`,`):

* If you set `symbol` to be a single symbol, such as `BTMX/USDT`, the API will respond with the ticker of the target symbol as an object. 
  If you want to wrap the object in a one-element list, append a comma to the symbol, e.g. `BTMX/USDT,`.
* You shall specify `symbol` as a comma separated symbol list, e.g. `BTMX/USDT,BTC/USDT`. The API will respond with a list of tickers. 


#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-request) section.

#### Prehash String

`<timestamp>+order/status`

#### Response

Returns a list order information in `data` field. Please use `orderId` field to match with your order.

Name           | Type     | Description
---------------|----------|-------------- 
`avgPx`        | `String` | average fill price
`cumFee`       | `String` | cumulated filled comission
`cumFilledQty` | `String` | cumulated filled qty
`errorCode`    | `String` | Could be empty
`feeAsset`     | `String` | Fee asset, e.g, `USDT`
`lastExecTime` | `String` | latest execution timestamp
`orderId`      | `String` | order id
`orderQty`     | `String` | order quantity
`orderType`    | `String` | order type
`price`        | `String` | order price
`seqNum`       | `Long`   | sequence number
`side`         | `String` | order side
`status`       | `String` | order status
`stopPrice`    | `String` | stop price(could be empty)
`symbol`       | `String` | symbol
`execInst`     | `String` | execution instruction, `POST` for Post-Only orders, `Liquidation` for forced-liquidation orders, and `NULL_VAL` otherwise.

#### Code Sample

Please refer to python code to [get order status](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/order_query.py)
