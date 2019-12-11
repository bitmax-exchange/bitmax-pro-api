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
            "avgPx": "7391.13",
            "cumFee": "0.005151618",
            "cumFilledQty": "0.00082",
            "errorCode": "",
            "feeAsset": "USDT",
            "lastExecTime": 1575953134011,
            "orderId": "a16eee206d610866943712rPNknIyhH",
            "orderQty": "0.00082",
            "orderType": "Market",
            "price": "8130.24",
            "seqNum": 2622058,
            "side": "Buy",
            "status": "Filled",
            "stopPrice": "",
            "symbol": "BTC/USDT"
        },
        {
            "avgPx": "7392.02",
            "cumFee": "0.005152238",
            "cumFilledQty": "0.00082",
            "errorCode": "",
            "feeAsset": "USDT",
            "lastExecTime": 1575953151764,
            "orderId": "a16eee20b6750866943712zWEDdAjt3",
            "orderQty": "0.00082",
            "orderType": "Market",
            "price": "8131.22",
            "seqNum": 2623469,
            "side": "Buy",
            "status": "Filled",
            "stopPrice": "",
            "symbol": "BTC/USDT"
        }
    ]
}
```

Query order status, either open or history order. //TODO: not all order, specify order range later.

**HTTP Request**

`GET <account-group>/api/pro/{account-category}/order/status?OrderId={orderId}`

`orderId` could be a single order Id, or multiple order Ids separated by `,`. 

Set `account-category` to`cash` for cash account and `margin` for margin account. 

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String**

`<timestamp>+order/status`

***Response***

Returns order information in *"data"* field. Please use *orderId* field to match with your order.

**Code Sample**

Please refer to python code to [get order status](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_order.py)
