###
### List History Orders (v2)

>  History Orders - Successful Response (Status 200, code 0)

```json
{"code": 0,
 "data": [{"accountId": "cshwSjbpPjSwHmxPdz2CPQVU9mnbzPpt",
           "avgFillPrice": "11346.77",
           "createTime": 1596344995793,
           "fee": "-0.004992579",
           "feeAsset": "USDT",
           "fillQty": "0.01",
           "lastExecTime": 1596344996053,
           "orderId": "a173ad938fc3U22666567717788c3b66",
           "orderQty": "0.01",
           "orderType": "Limit",
           "price": "11346.77",
           "seqNum": 18777366360,
           "side": "Sell",
           "status": "Canceled",
           "stopPrice": "0",
           "symbol": "BTC/USDT"}]
}
```

This API returns history orders according to specified parameters (up to 500 records). Compared with [**Current Order History API**] (#list-current-history-orders), this API is more flexible, but usually expects higher latency.

#### HTTP Request

`GET <account-group>/api/pro/v2/order/hist`

#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-request) section.

#### Prehash String

`<timestamp>+order/hist`

#### Request Parameters

 Name            | Type      | Required | Description
---------------- | --------- | -------- | -------------------------------------------------------------------------------------------
 `account`       | `String`  | Yes      | account type: `cash`/`margin`/`futures`, or actual accountId
 `symbol`        | `String`  | No       | symbol filter, e.g. `BTMX/USDT`
 `startTime`     | `Long`    | No       | start time in milliseconds.
 `endTime`       | `Long`    | No       | end time in milliseconds.
 `seqNum`        | `Long`    | No       | seqNum .
 `limit`         | `Int`     | No       | number of records to return. default 500, max 1000. 

Please note `seqNum` increase regirously but not continuously in response.

Rule for combination usage of `startTime`, `endTime`, and `seqNum`:
 * If at least one of seqNum and startTime is provided, query start from the oldest possible record (after given `startTime` or `seqNum`).
 * if seqNum provided, search >= seqNum
 * If neither seqNum nor startTime is provided, query range should start from the latest record (or endTime if provided) to the oldest.

***Response***

Return a list of history orders in *"data"* field.

Name           | Type     | Description
---------------|----------|--------------
`accountId`    | `String` | account Id
`createTime`   | `Long`   | order sending time
`avgFillPrice` | `String` | average fill price
`fee`          | `String` | cumulated filled comission
`feeAsset`     | `String` | Fee asset, e.g, `USDT`
`fillQty`      | `String` | cumulated filled qty
`lastExecTime` | `String` | latest execution timestamp
`orderId`      | `String` | order id
`orderQty`     | `String` | order quantity
`orderType`    | `String` | order type
`price`        | `String` | order price
`seqNum`       | `Long`   | sequence number
`side`         | `String` | order side
`status`       | `String` | order status
`stopPrice`    | `String` | stop price(0 by default)
`symbol`       | `String` | symbol

***Code Sample***

Please refer to python code to [get hist orders](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_order_hist_v2.py)
