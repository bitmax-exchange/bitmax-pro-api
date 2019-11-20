## Bar Info 

> Request 

```shell
curl -X GET https://bitmax.io/api/pro/barhist/info
```

> Sample response

```json
{
    "code": 0,
    "data": [
        {
            "name": "1",
            "intervalInMillis": 60000
        },
        {
            "name": "5",
            "intervalInMillis": 300000
        },
        {
            "name": "15",
            "intervalInMillis": 900000
        },
        {
            "name": "30",
            "intervalInMillis": 1800000
        },
        {
            "name": "60",
            "intervalInMillis": 3600000
        },
        {
            "name": "120",
            "intervalInMillis": 7200000
        },
        {
            "name": "240",
            "intervalInMillis": 14400000
        },
        {
            "name": "360",
            "intervalInMillis": 21600000
        },
        {
            "name": "720",
            "intervalInMillis": 43200000
        },
        {
            "name": "1d",
            "intervalInMillis": 86400000
        },
        {
            "name": "1w",
            "intervalInMillis": 604800000
        },
        {
            "name": "1m",
            "intervalInMillis": 2592000000
        }
    ]
}
```

This API returns a list of all bar intervals supported by the server. 

#### URL

`GET /api/pro/barhist/info`

#### Request Parameters 

This API endpoint does not take any parameters. 

#### Resposne

 Name              | Type | Description                                        
------------------- | --------- | ---------------------------------------------------
 `name`             | `String`  | name of the interval
 `intervalInMillis` | `Long`    | length of the interval 

Plesae note that the one-month bar (`1m`) always resets at the month start. The `intervalInMillis` value for the one-month `bar` is only indicative. 

The value in the `name` field should be your input to the [Historical Bar Data](#historical-bar-data) API.



## Historical Bar Data

> Request 

```shell
curl -X GET https://bitmax.io/api/pro/trades?symbol=BTMX/USDT&interval=1
```

> Sample response

```json
{
    "code": 0,
    "data": [
        {
            "m": "bar",           // message 
            "ts": 1573584540000,  // bar start time 
            "s": "BTMX/USDT",     // symbol 
            "i": "1",             // interval 
            "o": "0.06736",       // open price 
            "c": "0.06736",       // close price 
            "h": "0.06736",       // high price 
            "l": "0.06736",       // low price 
            "v": "4606"           // volume in quote asset
        }
    ]
}
```

This API returns a list of **bar**s, with each contains the open/close/high/low prices of a symbol for a specific time range. 

#### URL 

`GET /api/pro/barhist`

#### Request Parameters

 Name       | Type     | Required | Description                                                                                 
----------- | -------- | -------- | ------------------------------------------------------------------------------------------- 
 `symbol`   | `String` | Yes      | e.g. `"BTMX/USDT"`                                                                          
 `interval` | `String` | Yes      | a string representing the interval type.                                                    
 `to`       | `Long`   | No       | UTC timestamp in milliseconds. If not provided, this field will be set to the current time. 
 `from`     | `Long`   | No       | UTC timestamp in milliseconds.                                                              
 `n`        | `Int`    | No       | default 10, number of bars to be returned, this number will be capped at 500                

The requested time range is determined by three parameters - `to`, `from`, and `n` - according to rules below:

* `from`/`to` each specifies the start timestamp of the first/last bar. 
* `to` is always honored. If not provided, this field will be set to the current system time. 
* For `from` and `to`: 
  * if only `from` is provided, then the request range is determined by `[from, to]`, inclusive. However, if the range is too wide,
    the server will increase `from` so the number of bars in the response won't exceed 500. 
  * if only `n` is provided, then the server will return the most recent `n` data bars to time `to`. However, if `n` is greater than 500, 
    only 500 bars will be returned. 
  * if both `from` and `n` are specified, the server will pick one that returns fewer bars. 

#### Response 

@ToDo