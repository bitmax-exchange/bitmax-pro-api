### Bar Info 

> Request 

```
curl -X GET https://bitmax.io/api/pro/v1/barhist/info
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

**HTTP Request**

`GET /api/pro/v1/barhist/info`

This API returns a list of all bar intervals supported by the server. 


#### Request Parameters 

This API endpoint does not take any parameters. 

#### Resposne

 Name               | Type      | Description                                        
------------------- | --------- | ---------------------------------------------------
 `name`             | `String`  | name of the interval
 `intervalInMillis` | `Long`    | length of the interval 

Plesae note that the one-month bar (`1m`) always resets at the month start. The `intervalInMillis` value for the one-month `bar` is only indicative. 

The value in the `name` field should be your input to the [Historical Bar Data](#historical-bar-data) API.







### Historical Bar Data

> Request 

```
curl -X GET https://bitmax.io/api/pro/v1/barhist?symbol=BTMX/USDT&interval=1
```

> Sample response

```json
{
    "code": 0,
    "data": [
        {
            "data": {
                "c": "0.05019",
                "h": "0.05019",
                "i": "1",
                "l": "0.05019",
                "o": "0.05019",
                "ts": 1575409260000,
                "v": "1612"},
           "m": "bar",
           "s": "BTMX/USDT"},
        {
            "data": {
                "c": "0.05019",
                "h": "0.05027",
                "i": "1",
                "l": "0.05017",
                "o": "0.05017",
                "ts": 1575409200000,
                "v": "57242"
                },
           "m": "bar",
           "s": "BTMX/USDT"},
    ]
}
```

#### HTTP Request

`GET /api/pro/v1/barhist`

This API returns a list of **bar**s, with each contains the open/close/high/low prices of a symbol for a specific time range. 

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

Name     | Type   |   value  | Description
---------| -------| ---------| -------------------------------
`m`      | String |`bar`     | message type
`s`      | String |          | symbol
`data:ts`| Long   |          | bar start time in milliseconds
`i`      | String |          | interval
`o`      | String |          | open price
`c`      | String |          | close price
`h`      | String |          | high price
`l`      | String |          | low price
`v`      | String |          | volume in quote asset

#### Code Sample

Please refer python code to [get bar history]{https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_pub_barhist.py}