### List History Orders (v2)

>  History Orders - Successful Response (Status 200, code 0)

```json
{
  "code": 0,
  "data": [
    {
      "orderId"     :  "a173ad938fc3U22666567717788c3b66", // orderId
      "seqNum"      :  18777366360,                        // sequence number
      "accountId"   :  "cshwSjbpPjSwHmxPdz2CPQVU9mnbzPpt", // accountId 
      "symbol"      :  "BTC/USDT",                         // symbol
      "orderType"   :  "Limit",                            // order type (Limit/Market/StopMarket/StopLimit)
      "side"        :  "Sell",                             // order side (Buy/Sell)
      "price"       :  "11346.77",                         // order price
      "stopPrice"   :  "0",                                // stop price (0 by default)
      "orderQty"    :  "0.01",                             // order quantity (in base asset)
      "status"      :  "Canceled",                         // order status (Filled/Canceled/Rejected)
      "createTime"  :  1596344995793,                      // order creation time
      "lastExecTime":  1596344996053,                      // last execution time
      "avgFillPrice":  "11346.77",                         // average filled price
      "fillQty"     :  "0.01",                             // filled quantity (in base asset)
      "fee"         :  "-0.004992579",                     // cummulative fee. if negative, this value is the commission charged; if possitive, this value is the rebate received.
      "feeAsset"    :  "USDT"                              // fee asset
    }
  ]
}
```

This API returns history orders according to specified parameters (up to 500 records).

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
 `seqNum`        | `Long`    | No       | the seqNum to search from. All records in the response have seqNum no less than the input argument.
 `limit`         | `Int`     | No       | number of records to return. default 500, max 1000. 

Please note `seqNum` increases regirously but not continuously in response.

Rule for combination usage of `startTime`, `endTime`, and `seqNum`: 
 * If at least one of `seqNum` and `startTime` is provided, the search will start from the oldest possible record (after given `startTime` or `seqNum`).
 * If neither `seqNum` nor `startTime` is provided, the search will start from the latest record (or `endTime` if provided) to the oldest.

To retrieve the full history of orders, it is recommended to use `seqNum` and follow the procedure below:
 * Query the first batch of orders by sending a query with only `startTime` specifying. 
 * Let `n` be the largest `seqNum` of orders obtained from the previous query, query the next batch by only setting `seqNum = n+1`. 
 * repeat the previous step until you have reached the latest record.


***Response***

Return a list of history orders in *"data"* field.

Name           | Type     | Description
---------------|----------|--------------
`orderId`      | `String` | order id
`seqNum`       | `Long`   | sequence number
`accountId`    | `String` | account Id
`symbol`       | `String` | symbol
`orderType`    | `String` | order type
`side`         | `String` | order side
`price`        | `String` | order price
`stopPrice`    | `String` | stop price (0 by default)
`orderQty`     | `String` | order quantity
`status`       | `String` | order status
`createTime`   | `Long`   | order sending time
`lastExecTime` | `String` | latest execution timestamp
`avgFillPrice` | `String` | average fill price
`fillQty`      | `String` | cumulated filled qty
`fee`          | `String` | cummulative fee. if negative, this value is the commission charged; if possitive, this value is the rebate received.
`feeAsset`     | `String` | Fee asset, e.g, `USDT`

***Code Sample***

Please refer to python code to [get hist orders](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_order_hist_v2.py)
