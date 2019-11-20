# Public RESTful APIs


## List all Assets

> Request 

```
curl -X GET https://bitmax.io/api/pro/assets
```

> Sample Response 

```json
{
    "code": 0,
    "data": [
        {
            "assetCode": "BTMX",
            "assetName": "BitMax.io Native Token",
            "precisionScale": 9,
            "nativeScale": 2,
            "withdrawalFee": 11,
            "minWithdrawalAmt": 22,
            "status": "Normal"
        }
    ]
}
```

You can obtain a list of all assets listed on the exchange through this API.



## List all Products 

> Request 

```
curl -X GET https://bitmax.io/api/pro/products
```

> Sample Response 

```json
{
    "code": 0,
    "data": [
        {
            "symbol": "BTMX/USDT",
            "baseAsset": "BTMX",
            "quoteAsset": "USDT",
            "status": "Normal",
            "minNotional": "5",
            "maxNotional": "100000",
            "marginTradable": true,
            "commissionType": "Quote",
            "commissionReserveRate": "0.001",
            "tickSize": "0.000001",
            "lotSize": "0.001"
        }
    ]
}
```

#### Response Content

You can obtain a list of all products traded on the exchange through this API.

The response contains the following general fields:

 Field         | Type     | Description                                                                                 
-------------- | -------- | --------------------- 
 `symbol`      | `String` | e.g. `"BTMX/USDT"`
 `baseAsset`   | `String` | e.g. `"BTMX"`
 `quoteAsset`  | `String` | e.g. `"USDT"`
 `status`      | `String` | `"Normal"`

The response also contains criteria for new order request. 

 Field                   | Type      | Description                                                                                 
------------------------ | --------- | --------------------- 
 `minNotional`           | `String`  | 
 `maxNotional`           | `String`  | 
 `tickSize`              | `String`  | 
 `quoteSize`             | `String`  | 
 `marginTradable`        | `Boolean` | 
 `commissionType`        | `String`  | `"Base"`, `"Quote"`, `"Received"`
 `commissionReserveRate` | `String`  | e.g. `"0.001"`, see below.


