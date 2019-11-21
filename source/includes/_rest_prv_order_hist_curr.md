### List Current History Orders

> Current History Orders - Successful Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": [
        {
            "accountCategory": "CASH",
            "accountId":       "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
            "avgPrice":        "0.000000000",
            "baseAsset":       "BTC",
            "btmxCommission":  "0.000000000",
            "errorCode":       "NULL_VAL",
            "execId":          "79923",
            "execInst":        "NULL_VAL",
            "fee":             "0.000000000",
            "feeAsset":        "USDT",
            "filledQty":       "0.000000000",
            "notional":        "0.000000000",
            "orderId":         "16e61d5ff43s8bXHbAwwoqDo9d817339",
            "orderPrice":      "9048.210000000",
            "orderQty":        "0.110519000",
            "orderType":       "Limit",
            "quoteAsset":      "USDT",
            "sendingTime":      1573599444807,
            "side":            "Sell",
            "status":          "Canceled",
            "stopPrice":       "0.000000000",
            "symbol":          "BTC/USDT",
            "time":             1573619099000,
            "userId":          "mNeGB66kTS3n1TOkrRSd2txkMYWNYXGO"
        },
        ...
    ]
}
```

This API returns all current history orders for the account specified. //TODO: not all history, specify order range later.

**HTTP Request**

`GET <account-group>/api/pro/{account-category}/order/hist/current`

Set `account-category` to`cash` for cash account and `margin` for margin account. 

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#signing-a-Request) section.

**Prehash String**

`<timestamp>+order/hist/current`

**Response**

Return a list of history orders in *"data"* field.

**Code Sample**

Please refer to python code [get_hist_orders](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/query_order.py)
