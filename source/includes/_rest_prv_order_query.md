###
### Query Order

> Query Order - Successful Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountCategory": "CASH",
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "avgPrice": "7323.240000000",
        "baseAsset": "BTC",
        "btmxCommission": "0.000000000",
        "errorCode": "NULL_VAL",
        "execInst": "NULL_VAL",
        "fee": "0.003302782",
        "feeAsset": "USDT",
        "filledQty": "0.000820000",
        "notional": "6.005056800",
        "orderId": "a16ecd4c0caeU9490877774BwHW0fCYn",
        "orderQty": "0.000820000",
        "orderType": "Market",
        "quoteAsset": "USDT",
        "sendingTime": 1575402344401,
        "seqNum": "2259385850",
        "side": "Sell",
        "status": "Filled",
        "stopPrice": "0.000000000",
        "symbol": "BTC/USDT",
        "time": 1575402344424,
        "userId": "H1FR4LY7qxZDGMsVzBvt6ElDwtOjPL7Z"
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

Please refer to python code to [get order status](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_order.py)
