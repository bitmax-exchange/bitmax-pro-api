## Order 

Trading and Order related APIs. API path usually depend on account-group and account-category: 

  * account-group   : get your account-group from 'Account Info' API

  * account-category: cash or margin

For all order related ack or data, there is *orderId* field to identify the order. 

###
### Order id generation method

We use the following method to generate an unique id for each order place/cancel request.

**Method**
  
  * A = Convert timestamp (in miliseconds) to hex string;

  * B = 'a' for order via rest api, or 's' for order via websocket;
  
  * C = Account Id + Symbol + 'b' for buy or 's' for sell + User generated 32 chars order id;
  
  * D = first 11 chars of A  + B + last 12 chars of Account Id + MD5(C);
  
  * Final order Id = first 32 chars of D.

**Code Sample**

Please refer to python code [gen_server_order_id](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/bitmax/util/auth.py)


###
### Place Order

> Place Order - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "place-order",
        "info": {
            "id":        "16e607e2b83a8bXHbAwwoqDo55c166fa",
            "orderId":   "16e85b4d9b9a8bXHbAwwoqDoc3d66830",
            "orderType": "Market",
            "symbol":    "BTC/USDT",
            "timestamp":  1573576916201
        },
        "status": "Ack"
    }
}
```

> Place Order - Successful ACCEPT Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountCategory":       "CASH",
        "accountId":             "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "avgPrice":              "0",
        "baseAvailableBalance":  "39.2010425",
        "baseTotalBalance":      "39.2010425",
        "errorCode":             "NULL_VAL",
        "execId":                "78271",
        "execInst":              "NULL_VAL",
        "fee":                   "0",
        "feeAsset":               "",
        "filledQty":             "0",
        "m":                     "order",
        "orderId":               "16e60fc831ba8bXHbAwwoqDo3d898cf3",
        "orderQty":              "0.11",
        "orderType":             "Market",
        "quoteAvailableBalance": "1113781.119315161",
        "quoteTotalBalance":     "1114852.305731461",
        "side":                  "Buy",
        "status":                "New",
        "symbol":                "BTC/USDT",
        "transactTime":           1573585191865
    }
}
```


> Place Order - Successful DONE Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountCategory":       "CASH",
        "accountId":             "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "avgPrice":              "8846.25",
        "baseAvailableBalance":  "39.2010425",
        "baseTotalBalance":      "39.2010425",        
        "errorCode":             "NULL_VAL",
        "execId":                "78266",
        "execInst":              "NULL_VAL",
        "fee":                   "0.827124375",
        "feeAsset":              "USDT",
        "filledQty":             "0.11",
        "m":                     "order",
        "orderId":               "16e60f6601ba8bXHbAwwoqDo345548c3",
        "orderQty":              "0.11",
        "orderType":             "Market",
        "quoteAvailableBalance": "1114852.305731461",
        "quoteTotalBalance":     "1114852.305731461",
        "side":                  "Buy",
        "status":                "Filled",
        "symbol":                "BTC/USDT",
        "transactTime":           1573584789682
    }
}
```

> Place Order - Error Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "place-order",
        "info": {
            "code":     300002,
            "id":      "ZPJNQSMGhGGse6y5e2Ft79MFEUCbBF9U",
            "message": "Order quantity is too small.",
            "reason":  "INVALID_QTY"
        },
        "status": "Err"
    }
}
```

Place a new order.

#### Signature

You should sign the message and include it in request header. (Please refer to section **Authenticate a RESTful Request**)

#### HTTP Request

`POST <account-group>/api/pro/{account-category}/order`

#### Request Parameters

Name       | Type   |Required| Value Range                          | Description
-----------|--------|------- | -------------------------------------|---------------
symbol     | String |  Yes   |                                      |
time       | Long   |  Yes   |milliseconds since UNIX epoch in UTC  |We do not process request placed more than 30 seconds ago.
orderQty   | String |  Yes   |                                      |Order size. Please set scale properly for each symbol.
orderType  | String |  Yes   |["market", "limit"]                   |Order type
side       | String |  Yes   |["buy", "sell"]                       |  
id         | String |  No    |32 chars(letter and digit number only)|Please generate unique ID for each trade, we echo it back to help you to match response with request.
orderPrice | String |  No    |                                      |The limit price for limit order. Please set price scale properly.
stopPrice  | String |  No    |                                      |Trigger price of stop limit order
postOnly   | Boolean|  No    |["true", "false"]                     |
timeInForce| String |  No    |["GTC", "IOC"]                        |GTC: good-till-canceled; IOC: immediate-or-cancel. GTC by default.
respInst   | String |  No    |["ACK", "ACCEPT", "DONE"]             |Response instruction. Refer to "Response" below. "ACK" by default.  

The table below shows how to correctly configure order of different types: (o - required, x - optional)

Name        | Market | Limit | StopMarket | StopLimit
----------- | ------ | ----- | ---------- | ---------
id          | x      | x     | x          | x    
time        | o      | o     | o          | o
symbol      | o      | o     | o          | o
orderPrice  |        | o     |            | o
orderQty    | o      | o     | o          | o
orderType   | o      | o     | o          | o
side        | o      | o     | o          | o
postOnly    |        | x     |            | 
stopPrice   |        |       | o          | o
timeInForce |        | x     |            | 


#### Order Request Criteria

When placing a new **limit** order, the request parameters must meet all criteria defined in the [Products API](#list-all-products):

* The order notional must be within range `[minNotional, maxNotional]`. For limit orders, the order notional is defined as the product of `orderPrice` and `orderQty`.
* `orderPrice` and `stopPrice` must be multiples of `tickSize`.
* `orderQty` must be a multiple of `lotSize`.
* If you are trading using the margin account, `marginTradable` must be `true`. 
* For cash trading, you must have sufficient balance to fund the order. 
  * for buy orders, if `commissionType=Quote`, the quote asset balance must be no less than `orderPrice * orderQty * (1 + commissionReserveRate)`. For all other `commissionType`s (`Base` and `Received`), the quote asset balance must be no less than `orderPrice * orderQty`
  * for sell orders, if `commissionType=Base`, your base asset balance must be no less than `orderQty * (1 + commissionReserveRate)`, For other `commissionType`s (`Received` and `Quote`), the base asset balance must be no less than `orderQty`.
* For margin trading, you must make sure you have sufficient **max sellable amount** to fund the order. 


#### Response

In "Err" response, *id* is the id provided by user when placing order; for other responses, *orderId* is the id generated by server following "Order id generation method" above, and this is the id you should provide for future order query or cancel. 

In case you want to cancel an order before response from server, you could figure out the orderId following "Order id generation method" above.

*ACK*

Response with status 'Ack' to indicate new order request received by our server and passed some basic order field check. This is the default response type.

*ACCEPT*

Response with status "New" to indicate new order request is accepted by our match engine. Return normal 'Ack' response if no 'New' status update within 5 seconds.

*DONE*

Response with status "PartiallyFilled", "Filled", or "Rejected" to indicate the order request is partially filled, fully filled, or rejected by matching engine. Return normal 'Ack' response if no order status update within 5 seconds. 

*ERR*

Response with status "Err" to provide detailed error information on the order request. 


Error Response Messages (TODO: verify HTTP Status Code)

HTTP Status Code | Error Code | Reason           | Example
---------------- | ---------- | ---------------- | ----------------------------------------------------------------------
400              | xxx        | Parameter Error  | 


**Code Sample**

Refer to sample python code [place_order](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/place_order.py)

###
### Cancel Order

> Cancel Order - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "cancel-order",
        "status": "Ack",
        "info": {
            "id":        "wv8QGquoeamhssvQBeHOHGQCGlcBjj23",
            "orderId":   "16e6198afb4s8bXHbAwwoqDo2ebc19dc",
            "orderType": "NULL_VAL",
            "symbol":    "ETH/USDT",
            "timestamp":  1573594877822
        }
    }
}
```

> Cancel Order - Error Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "cancel-order",
        "status": "Err",
        "info": {
            "code":     300006,
            "id":      "jHAfoOqZmRv3GP1URJ5624moJ9RCG2@3",
            "message": "Invalid Client Order Id: jHAfoOqZmRv3GP1URJ5624moJ9RCG2@3",
            "reason":  "INVALID_ORDER_ID",
            "symbol":  "ETH/USDT"
        }
    }
}
```

Cancel an existing open order. 

**Signature**

You should sign the message in header as specified in **Authenticate a RESTful Request** section.

**HTTP Request**

`DELETE <account-group>/api/pro/{account-category}/order`

**Request Parameters**

Name      | Type   |Required| Value Range                            | Description
------------|--------|--------| -------------------------------------|---------------
id          | String |  Yes   |32 chars(letter and digit number only)|Please generate unique ID for each trade; we will echo it back to help you identify the response.
orderId     | String |  Yes   |32 chars order id responded by server when place order|
symbol      | String |  Yes   |                                      |  
time        | Long   |  Yes   |milliseconds since UNIX epoch in UTC  |We do not process request placed more than 30 seconds ago.

**Response**

*ACK*

Response with status "Ack" to indicate the cancel order request is received by server. And you should use provided "orderId" to check cancel status in the future; we also echo back *id* from your request for reference purpose.

*ERR*

Response with status "Err" to indicate there is something wrong with the cancel order request. We echo back the *coid* field in your request.


**Code Sample**

Refer to sample python code [cancel_order](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/cancel_order.py)

###
### Cancel All Orders

> Cancel All Orders - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "cancel-all",
        "info": {
            "id":        "2bmYvi7lyTrneMzpcJcf2D7Pe9V1P9wy",
            "orderId":   "",
            "orderType": "NULL_VAL",
            "symbol":    "",
            "timestamp":  1574118495462
        },
        "status": "Ack"
    }
}
```

Cancel all current open orders for the account specified, and optional symbol.

**HTTP Request**

`DELETE <account-group>/api/pro/{account-category}/order/all`

**Request Parameters**

      Name      | Type   |Required| Value Range                           | Description
----------------|--------|-------| -------------------------------------- |---------------
    symbol      | String |  No   |  Valid symbol supported by exchange    |  If provided, only cancel all orders on this symbol; otherwise, cancel all open orders under this account.

**Response**

Response with status "Ack" to indicate cancel all order request is received by server.

**Code Sample**

Refer to sample python code [cancel_all_order](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/cancel_order.py)

#### Caveat 

The server will process the cancel all request with best effort. Orders sent but un-acked will not be canceled. You should rely on websocket order update messages or the RESTful api 
to obtain the latest status of each order. 


###
### Place Batch Orders

> Place Batch Orders - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
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
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "batch-place-order",
        "info": [
            {
                "code":     300013,
                "id":      "N7PxdMH8iGWiCZOau14i3SGLEzfZpO06",
                "message": "Some invalid order in this batch",
                "reason":  "INVALID_BATCH_ORDER",
                "symbol":  "ETH/USDT"
            },
            {
                "code":     300004,
                "id":      "R1LWczhWvAP3DGTEfAOzD3XmXybywXiC",
                "message": "Notional is too small.",
                "reason":  "INVALID_NOTIONAL",
                "symbol":  "BTC/USDT"
            }
        ],
        "status": "Err"
    }
}
```

Place multiple orders in a batch. If some order in the batch failed our basic check, then the whole batch request fail.

You may submit up to 10 orders at a time. Server will respond with error if you submit more than 10 orders.

**HTTP Request**

`POST <account-group>/api/pro/{account-category}/order/batch`

**Signature**

For this API you must include *x-auth-coid* in your request header. You must concatenate IDs of all orders with character *+*. The order of IDs in the header must match the orders in the request.

**Response**

*ACK*

Status "Ack" to indicate the batch order request is accepted by server. Field "info" includes server generated "coid" for each order in the batch request, and this is the id you should use for future status query.

*ERR*

Status "ERR" to indicate the batch order request is accepted by server. Field "info" includes detailed order information to explain why the batch request fail for each individual order. "coid" is original order id provided by user for each order.


**Code Sample**

Please refer to python code [place_batch_order] (https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/place_order.py)

###
### Cancel Batch Orders

> Cancel Batch Orders - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "batch-cancel-order",
        "status": "Ack",
        "info": [
            {
                "id":        "0a8bXHbAwwoqDo3b485d7ea0b09c2cd8",
                "orderId":   "16e61d5ff43s8bXHbAwwoqDo9d817339",
                "orderType": "NULL_VAL",
                "symbol":    "BTC/USDT",
                "timestamp":  1573619097746
            },
            {
                "id":        "0a8bXHbAwwoqDo7d303e2edf6c26d1be",
                "orderId":   "16e61adeee5a8bXHbAwwoqDo100e364e",
                "orderType": "NULL_VAL",
                "symbol":    "ETH/USDT",
                "timestamp":  1573619098342
            }
        ]
    }
}
```

> Cancel Batch Orders - Error Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "action": "batch-cancel-order",
        "status": "Err",
        "info": [
            {
                "code":     300006,
                "id":      "NUty15oXcNt9JAngZ1D6q6jY15LOpKPC",
                "orderId": "16e61d5ff43s8bXHbAwwoqDo9d817339",
                "message": "The order is already filled or canceled.",
                "reason":  "INVALID_ORDER_ID",
                "symbol":   ""
            },
            {
                "code":     300006,
                "id":      "mpoL0q8cheL8PL2UstJFRzp6yuPk1sGc",
                "orderId": "16e61adeee5a8bXHbAwwoqDo100e364e",
                "message": "The order is already filled or canceled.",
                "reason":  "INVALID_ORDER_ID",
                "symbol":   ""
            }
        ]
    }
}
```

Cancel multiple orders in a batch. If some order in the batch failed our basic check, then the whole batch request failed.

**HTTP Request**

`DELETE <account-group>/api/pro/{account-category}/order/batch`

**Signature**

For this API you must include *x-auth-coid* in your request header. You must concatenate IDs of all orders with character *+*. The order of IDs in the header must match the orders in the request.

**Response**

*ACK*

Response with status "Ack" to indicate batch is received by server and pass some basic check.

*ERR* 

Response with status "Err" to explain detailed failure reason for each order in the batch request.


**Code Sample**

please refer to python code [cancel_batch_order](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/cancel_order.py)

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

***Response***

Returns order information in *"data"* field. Please use *orderId* field to match with your order.

**Code Sample**

Please refer to python code [get_order_status](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/query_order.py)

### 
### Open Orders

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

**Signature** 

You should sign the message 

**HTTP Request**

`GET <account-group>/api/pro/{account-category}/order/open`

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


### Current History Orders

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

**Response**

Return a list of history orders in *"data"* field.

**Code Sample**

Please refer to python code [get_hist_orders](https://github.com/gdm-exchange/bitmax-api-demo/blob/master/python/query_order.py)
