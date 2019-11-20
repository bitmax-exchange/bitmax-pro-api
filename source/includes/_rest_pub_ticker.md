## Ticker 

> Ticker for one product

```json
// curl -X GET 'https://bitmax.io/api/pro/ticker?symbol=BTMX/USDT'
{
    "code": 0,
    "data": {
        "symbol": "BTMX/USDT",
        "open": "0.06777",
        "close": "0.06809",
        "high": "0.06899",
        "low": "0.06708",
        "volume": "19823722",
        "ask": [
            "0.0681",
            "43641"
        ],
        "bid": [
            "0.0676",
            "443"
        ]
    }
}
```

> List of Tickers for one or multiple products

```json
// curl -X GET "https://bitmax.io/api/pro/ticker?symbol=BTMX/USDT,"
{
    "code": 0,
    "data": [
        {
            "symbol": "BTMX/USDT",
            "open": "0.06777",
            "close": "0.06809",
            "high": "0.06809",
            "low": "0.06809",
            "volume": "19825870",
            "ask": [
                "0.0681",
                "43641"
            ],
            "bid": [
                "0.0676",
                "443"
            ]
        }
    ]
}
```

You can get summary statistics of one or multiple symbols with this API. 


#### URL

`GET api/pro/ticker`


#### Request Parameters

Name       | Type      | Required | Value Range | Description
-----------| --------- | -------- | ----------- | ---------------
`symbol`   | `String`  |  No      |             | you may specify one, multiple, or all symbols of interest. See below.


This API endpoint accepts one optional string field `symbol`: 

* If you do not specify `symbol`, the API will responde with tickers of all symbols in a list. 
* If you set `symbol` to be a single symbol, such as `BTMX/USDT`, the API will respond with the ticker of the target symbol as an object. 
  If you want to wrap the object in a one-element list, append a comma to the symbol, e.g. `BTMX/USDT,`.
* You shall specify `symbol` as a comma separated symbol list, e.g. `BTMX/USDT,BTC/USDT`. The API will respond with a list of tickers. 

#### Respond Content

The API will respond with a ticker object or a list of ticker objects, depending on how you set the `symbol` parameter. 

Each ticker object contains the following fields:

 Field      | Type                 | Description                                                                                 
----------- | -------------------- | --------------------- 
 `symbol`   |  `String`            | 
 `open`     |  `String`            | the traded price 24 hour ago
 `close`    |  `String`            | the last traded price
 `high`     |  `String`            | the highest price over the past 24 hours 
 `low`      |  `String`            | the lowest price over the past 24 hours 
 `volume`   |  `String`            | the total traded volume in quote asset over the paste 24 hours
 `ask`      |  `[String, String]`  | the price and size at the current best ask level
 `bid`      |  `[String, String]`  | the price and size at the current best bid level

