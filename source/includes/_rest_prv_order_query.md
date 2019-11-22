###
### Query Order

> Query Order - Successful Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountCategory": "CASH",
        "accountId":       "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "avgPrice":        "8844.640000000",
        "baseAsset":       "BTC",
        "btmxCommission":  "0.000000000",        
        "errorCode":       "NULL_VAL",
        "execId":          "76877",
        "execInst":        "NULL_VAL",
        "fee":             "0.751794400",
        "feeAsset":        "USDT",
        "filledQty":       "0.100000000",
        "notional":        "884.464000000",
        "orderId":         "16e60458b97a8bXHbAwwoqDo4723edf8",
        "orderQty":        "0.100000000",
        "orderType":       "Market",
        "quoteAsset":      "USDT",
        "sendingTime":      1573573206843,
        "side":            "Buy",
        "status":          "Filled",
        "symbol":          "BTC/USDT",
        "time":             1573573206843,
        "userId":          "mNeGB66kTS3n1TOkrRSd2txkMYWNYXGO"
    }
}
```

Query order status, either open or history order. //TODO: not all order, specify order range later.

**HTTP Request**

`GET <account-group>/api/pro/{account-category}/order/status`

Set `account-category` to`cash` for cash account and `margin` for margin account. 

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String**

`<timestamp>+order/status`

***Response***

Returns order information in *"data"* field. Please use *orderId* field to match with your order.

**Code Sample**

Please refer to python code [get_order_status](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/query_order.py)
