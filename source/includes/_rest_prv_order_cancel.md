###
### Cancel Order

> Cancel Order - Successful ACK Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
        "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
        "ac": "CASH",
        "action": "cancel-order",
        "status": "Ack",
        "info": {
            "id":        "wv8QGquoeamhssvQBeHOHGQCGlcBjj23",
            "orderId":   "16e6198afb4s8bXHbAwwoqDo2ebc19dc",
            "orderType": "", // could be empty
            "symbol":    "ETH/USDT",
            "timestamp":  1573594877822
        }
    }
}
```

> Cancel Order - Error Response (Status 200, code 0)

```json
{
    "code": 300006,
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "ac": "CASH",
    "action": "cancel-order",
    "status": "Err",
    "message": "Invalid Client Order Id: jHAfoOqZmRv3GP1URJ5624moJ9RCG2@3",
    "reason":  "INVALID_ORDER_ID",
    "info": {
        "id": "jHAfoOqZmRv3GP1URJ5624moJ9RCG2@3",
        "symbol":  "ETH/USDT"
    }
}
```

Cancel an existing open order. 


**HTTP Request**

`DELETE <account-group>/api/pro/v1/{account-category}/order`

Set `account-category` to `cash` for cash account and `margin` for margin account. 

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-request) section.

**Prehash String**

`<timestamp>+order`


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

Refer to sample python code to [cancel order](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/cancel_order.py)
