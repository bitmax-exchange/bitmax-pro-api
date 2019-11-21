### 
### List Open Orders

> Open Orders - Successful Response (Status 200, code 0)

```json
{
  "code": 0,
  "data": [
    { 
      "accountCategory":    "CASH",
      "userId":             "supEQeSJQllKkxYSgLOoVk7hJAX59WSz",
      "accountId":          "cshKAhmTHQNUKhR1pQyrDOdotE3Tsnz4",
      "symbol":             "ETH/BTC",
      "baseAsset":          "ETH",
      "quoteAsset":         "BTC",
      "orderPrice":         "0.310000000",                      // only available for limit and stop limit orders
      "orderQty":           "1.000000000",
      "side":               "Buy",
      "avgPrice":           "0.000000000",                      // Average filled price of the order      
      "execInst":           "NULL_VAL",
      "fee":                "0.000000000",                      // cumulative fee paid for this order
      "feeAsset":           "BTC",                              // the asset
      "filledQty":          "0.000000000",                      // filled quantity
      "orderId":            "16e85a95e35a8bXHbAwwoqDo297932b1", // the unique identifier, you will need
                                                                // this value to cancel this order
      "orderType":          "StopLimit",
      "status":             "PendingNew",
      "stopPrice":          "0.300000000",                      // only available for stop market and stop limit orders
      "time":                1566091628227,                     // The last execution time of the order @TODO@FixMe
      "sendingTime":         1566091503547                      // The sending time of the order
    }
  ]
}
```

This API returns all current open orders for the account specified. 

**HTTP Request**

`GET <account-group>/api/pro/{account-category}/order/open`

Set `account-category` to`cash` for cash account and `margin` for margin account. 

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#signing-a-Request) section.

**Prehash String**

`<timestamp>+order/open`

**Response**

Return order infomation in *"data"* field. 

Error Response Messages

HTTP Status Code | Error Code | Reason           | Example
---------------- | ---------- | ---------------- | ----------------------------------------------------------------------
400              | xxx        | Parameter Error  | `{"code": xxx, "message": "missing requird parameter \"account\"} "}`  @TODO


**Code Sample**

Please refer to python code [get_open_orders](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/query_order.py)

Change from the previous version:

* `execId`, `btmxCommission`, `notional` are no longer included in the response. 
* `errorCode` is no longer included in the open order response. It is still included in the historical order query response.

