### List Current History Orders

> Current History Orders - Successful Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": [
        {
            "accountCategory": "CASH",
            "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
            "avgPrice": "7290.520000000",
            "baseAsset": "BTC",
            "btmxCommission": "0.000000000",
            "errorCode": "NULL_VAL",
            "execInst": "NULL_VAL",
            "fee": "0.003288025",
            "feeAsset": "USDT",
            "filledQty": "0.000820000",
            "notional": "5.978226400",
            "orderId": "a16eca1ca893U9490877774G90ClwU19",
            "orderQty": "0.000820000",
            "orderType": "Market",
            "quoteAsset": "USDT",
            "sendingTime": 1575348906967,
            "seqNum": "2242870574",
            "side": "Buy",
            "status": "Filled",
            "stopPrice": "0.000000000",
            "symbol": "BTC/USDT",
            "time": 1575348906991,
            "userId": "H1FR4LY7qxZDGMsVzBvt6ElDwtOjPL7Z"
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

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String**

`<timestamp>+order/hist/current`

**Response**

Return a list of history orders in *"data"* field.

**Code Sample**

Please refer to python code to [get hist orders](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_order.py)
