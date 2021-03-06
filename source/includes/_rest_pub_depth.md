### Order Book (Depth)

> Request for Order Book (Depth) Data

```
curl -X GET https://bitmax.io/api/pro/v1/depth?symbol=BTMX/USDT
```

> Order Book (Depth) Data - Sample response 

```json
{
    "code": 0,
    "data": {
        "m":      "depth-snapshot",
        "symbol": "BTMX/USDT",
        "data": {
            "seqnum":  5068757,
            "ts":      1573165838976,
            "asks": [
                [
                    "0.06848",
                    "4084.2"
                ],
                [
                    "0.0696",
                    "15890.6"
                ]
            ],
            "bids": [
                [
                    "0.06703",
                    "13500"
                ],
                [
                    "0.06615",
                    "24036.9"
                ]
            ]
        }
    }
}
```

#### HTTP Request

`GET /api/pro/v1/depth`

#### Request Parameters

   Name    | Type    | Required | Value Range                         | Description
---------- | ------- | -------- | ----------------------------------- |---------------
 `symbol`  | String  | Yes      |  Valid symbol supported by exchange | 

#### Response Content

`data` field in response contains depth data and meta info.

   Name    | Type               | Description 
---------- | ------------------ | -----------------------------
 `m`       | `String`           | `"depth-snapshot"`
 `symbol`  | `String`           | e.g. `"BTMX/USDT"`
 `data`    | `Json`             | actual bid and ask info. See below for detail.

Actual depth data in `data` section:

    Name   | Type               | Description 
---------- | ------------------ | -----------------------------
 `seqnum`  | `Long`             | a sequence number that is guaranteed to increase for each symbol. 
 `ts`      | `Long`             | UTC timestamp in milliseconds when the message is generated by the server
 `asks`    | `[String, String]` | pair of price and size of ask levels
 `bids`    | `[String, String]` | pair of price and size of bid levels

#### Demo Sample

Pleas refer to python code to [take depth snapshot](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_pub_depth.py)
