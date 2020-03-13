### List Current History Orders

> Current History Orders - Successful Response (Status 200, code 0)

```json
{
    "ac": "CASH",
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "code": 0,
    "data": [
        {
            "avgPx": "7243.34",
            "cumFee": "0.051101764",
            "cumFilledQty": "0.0083",
            "errorCode": "",
            "feeAsset": "USDT",
            "lastExecTime": 1576019215402,
            "orderId": "s16ef210b1a50866943712bfaf1584b",
            "orderQty": "0.0083",
            "orderType": "Market",
            "price": "7967.62",
            "seqNum": 8159713,
            "side": "Buy",
            "status": "Filled",
            "stopPrice": "",
            "symbol": "BTC/USDT",
            "execInst": "NULL_VAL"
        },
        ...
    ]
}
```

This API returns all current history orders for the account specified. If you need earlier data, please refer to #list-history-orders.

#### HTTP Request

`GET <account-group>/api/pro/v1/{account-category}/order/hist/current`

Set `account-category` to`cash` for cash account and `margin` for margin account. 

#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-request) section.

#### Prehash String

`<timestamp>+order/hist/current`

#### Request Parameters

 Name            | Type      | Required | Description                                                                                 
---------------- | --------- | -------- | ------------------------------------------------------------------------------------------- 
 `n`             | `Int`     | No       | maximum number of orders to be included in the response
 `symbol`        | `String`  | No       | symbol filter, e.g. `"BTMX/USDT"`
 `executedOnly`  | `Boolean` | No       | if `True`, include orders with non-zero filled quantities only.

#### Response

Return a list of history orders in *"data"* field.

#### Code Sample

Please refer to python code to [get recent hist orders](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_order_hist_curr.py)
