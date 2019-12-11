### 
### List Open Orders

> Open Orders - Successful Response (Status 200, code 0)

```json
{"accountCategory": "CASH",
 "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
 "code": 0,
 "data": [
   {
     "avgPx": "0", // Average filled price of the order   
      "cumFee": "0", // cumulative fee paid for this order
      "cumFilledQty": "0", // cumulative filled quantity
      "errorCode": "", // error code; could be empty
      "feeAsset": "USDT", // fee asset
      "lastExecTime": 1576019723550, //  The last execution time of the order
      "orderId": "s16ef21882ea0866943712034f36d83", // server provided orderId
      "orderQty": "0.0083", // order quantity
      "orderType": "Limit", // order type
      "price": "7105", // order price
      "seqNum": 8193258, // sequence number
      "side": "Buy", // order side
      "status": "New", // order status on matching engine
      "stopPrice": "", // only available for stop market and stop limit orders; otherwise empty 
      "symbol": "BTC/USDT"},
      ...
  ]
}
```

This API returns all current open orders for the account specified. 

**HTTP Request**

`GET <account-group>/api/pro/{account-category}/order/open`

Set `account-category` to`cash` for cash account and `margin` for margin account. 

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String**

`<timestamp>+order/open`

**Response**

Return order infomation in *"data"* field. 

Error Response Messages

HTTP Status Code | Error Code | Reason           | Example
---------------- | ---------- | ---------------- | ----------------------------------------------------------------------
400              | xxx        | Parameter Error  | `{"code": xxx, "message": "missing requird parameter \"account\"} "}`  @TODO


**Code Sample**

Please refer to python code to [get open orders](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_order.py)

Change from the previous version:

* `execId`, `btmxCommission`, `notional` are no longer included in the response. 
* `errorCode` is no longer included in the open order response. It is still included in the historical order query response.

