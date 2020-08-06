###
### List History Orders

>  History Orders - Successful Response (Status 200, code 0)

```json
{
    "code": 0,
    "data": {
            "data":
                [
                    {
                        "ac": "FUTURES",
                        "accountId": "testabcdefg",
                        "avgPx": "0",
                        "cumFee": "0",
                        "cumQty": "0",
                        "errorCode": "NULL_VAL",
                        "execInst": "NULL_VAL",
                        "feeAsset": "USDT",
                        "lastExecTime": 1584072844085,
                        "orderId": "r170d21956dd5450276356bbtcpKa74",
                        "orderQty": "1.1499",
                        "orderType": "Limit",
                        "price": "4000",
                        "sendingTime": 1584072841033,
                        "seqNum": 24105338,
                        "side": "Buy",
                        "status": "Canceled",
                        "stopPrice": "",
                        "symbol": "BTC-PERP"},
                 ] 
            "hasNext": False,
            "limit": 500,
            "page": 1,
            "pageSize": 20
        }
}
```

This API returns history orders according to specified parameters (up to 500 records). Compared with [**Current Order History API**] (#list-current-history-orders), this API is more flexible, but usually expects higher latency.

#### HTTP Request

`GET <account-group>/api/pro/v1/order/hist`

#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-request) section.

#### Prehash String

`<timestamp>+order/hist`

#### Request Parameters

 Name            | Type      | Required | Description
---------------- | --------- | -------- | -------------------------------------------------------------------------------------------
 `symbol`        | `String`  | No       | symbol filter, e.g. `BTMX/USDT`
 `category`      | `String`  | No       | account filter: `cash`/`margin`/`futures`
 `orderType`     | `String`  | No       | `market`, `limit`, and so on.
 `side`          | `String`  | No       | `buy`/`sell`
 `status`        | `String`  | No       | `Canceled`/`Filled`  
 `startTime`     | `Long`    | No       | start time in milliseconds.
 `endTime`       | `Long`    | No       | end time in milliseconds.
 `page`          | `Int`     | No       | number of page, default 1.
 `pageSize`      | `Int`     | No       | number of record per page, default 20.

***Response***

Return a list of history orders in *"data"* field.

`data` schema:

Name        |  Type       | Description
------------| ----------- | -------------
`data`      | `Array`     | List of orders, see below for detail
`hasNext`   | `Boolean`   | If more data available
`limit`     | `Int`       | Total number of orders to be returned
`page`      | `Int`       | Current page
`pageSize`  | `Int`       | Page Size

Order `data` schema:

Name           | Type     | Description
---------------|----------|--------------
`ac`           | `String` | `CASH`/`MARGIN`/`FUTURES`
`accountId`    | `String` | account Id
`avgPx`        | `String` | average fill price
`cumFee`       | `String` | cumulated filled comission
`cumQty`       | `String` | cumulated filled qty
`errorCode`    | `String` | Could be empty
`feeAsset`     | `String` | Fee asset, e.g, `USDT`
`lastExecTime` | `String` | latest execution timestamp
`orderId`      | `String` | order id
`orderQty`     | `String` | order quantity
`orderType`    | `String` | order type
`price`        | `String` | order price
`sendingTime`  | `Long`   | order sending time
`seqNum`       | `Long`   | sequence number
`side`         | `String` | order side
`status`       | `String` | order status
`stopPrice`    | `String` | stop price(could be empty)
`symbol`       | `String` | symbol
`execInst`     | `String` | execution instruction, `POST` for Post-Only orders, `Liquidation` for forced-liquidation orders, and `NULL_VAL` otherwise.

***Code Sample***

Please refer to python code to [get hist orders](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_order_hist.py)
