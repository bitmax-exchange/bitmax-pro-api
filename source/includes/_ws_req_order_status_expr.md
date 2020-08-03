### WS: Query Order Status by ID (Pending Release)

> Requesting order status on two orderIds

```json
{
    "op"     : "req",
    "id"     : "6ogiJZJ3",
    "action" : "order-status",
    "account": "cash",  // you could also use the actual accountId
    "args": {
        "orderId": "r173b199149dU6846912707bbtcuKQyG,r173b1872c58U6846912707bbtcuAJW5"
    }
}
```

> Order Status Response Message

```json
{
    "m"   : "order-status", 
    "code": 0,              # when code = 0, the request is successful. 
    "id"  : "6ogiJZJ3",     # the same id as specified in the request. 
    "data": [{
        "sn"     :   20,                                 // sequence number
        "e"      :   "ExecutionReport",                  // event name, for orders, this field is always ExecutionReport
        "a"      :   "cshsWhHrfh4TO8KwJc17p051L1JklWRi", // accountId
        "ac"     :   "CASH",                             // account category: CASH/MARGIN/FUTURES
        "t"      :   1596412468486,                      // last execution time
        "ct"     :   1596412468477,                      // create time
        "orderId":   "r173b199149dU6846912707bbtcuKQyG", // order Id
        "sd"     :   "Buy",                              // order side: Buy/Sell
        "ot"     :   "Limit",                            // order type: Market, Limit, etc.
        "ei"     :   "NULL_VAL",                         // execution instruction
        "q"      :   "0.001",                            // order quantity
        "p"      :   "11050",                            // order price 
        "sp"     :   "0",                                // stop price
        "spb"    :   "",                                 // stop price trigger
        "s"      :   "BTC/USDT",                         // symbol
        "st"     :   "Filled",                           // order status: New/Filled/PartiallyFileed/Canceled/Rejected
        "err"    :   "",                                 // error code
        "lp"     :   "11050",                            // last filled price
        "lq"     :   "0.001",                            // last filled quantity
        "ap"     :   "11050",                            // average filled price 
        "cfq"    :   "0.001",                            // cummulative filled quantity
        "f"      :   "0",                                // fee
        "cf"     :   "0.001105",                         // cumuulative fee
        "fa"     :   "USDT"                              // fee asset
    },
    ...
  ]
}
```

You can query order status by order Id via websocket with an `order-status` request. 

The request schema:

 Name          | Data Type | Description                
-------------- | --------- | -------------------------- 
 `op`          | `String`  | `req`                      
 `action`      | `String`  | `order-status`  
 `id`          | `String`  | for result match purpose
 `account`     | `String`  | `cash`, `margin`         
 `args:orderId`| `String`  | orderIds separated by comma


The Response Schema:

 Name     | Data Type          | Description                   
--------- | ------------------ | ----------------------------- 
 `m`      | `String`           | `order-status`
 `code`   | `Int`              | error code, if `code = 0`, the request is successful.
 `id`     | `String`           | echo back `id` in request
 `data`   | `Json`             | See `data` detail below
 `reason` | `Optional[String]` | error mnemonic
 `info`   | `Optional[String]` | detailed error info


`data` field details:

Name      | Data Type | Description
--------- | ----------| -----------------------------
`sn`      | Long      | sequence number
`e`       | `String`  | event name, for orders, this field is always ExecutionReport
`a`       | `String`  | accountId
`ac`      | `String`  | account category: CASH/MARGIN/FUTURES
`t`       | Long      | last execution time, UTC timestamp in milliseconds
`ct`      | Long      | create time, UTC timestamp in milliseconds
`orderId` | `String`  | order Id
`sd`      | `String`  | order side: Buy/Sell
`ot`      | `String`  | order type: Market, Limit, etc.
`ei`      | `String`  | execution instruction
`q`       | `String`  | order quantity
`p`       | `String`  | order price 
`sp`      | `String`  | stop price
`spb`     | `String`  | stop price trigger
`s`       | `String`  | symbol
`st`      | `String`  | order status: New/Filled/PartiallyFileed/Canceled/Rejected
`err`     | `String`  | error code
`lp`      | `String`  | last filled price
`lq`      | `String`  | last filled quantity
`ap`      | `String`  | average filled price 
`cfq`     | `String`  | cummulative filled quantity
`f`       | `String`  | fee
`cf`      | `String`  | cumuulative fee
`fa`      | `String`  | fee asset


By default, the data field in the response is a list of object, each contains info of a single order. However, when `orderId` in the request contains only a single orderId,
the server will set the data field to a single object. If you want the server to respond with a list of one object in this case, append a comma to the orderId, for instance:
`{"orderId": "r173b199149dU6846912707bbtcuKQyG,"}`.


