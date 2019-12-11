### List all Products 

> List all Products 

```
curl -X GET https://bitmax.io/api/pro/products
```

> Sample Response 

```json
{
    "code": 0,
    "data": [
        {
            "symbol":                "BTMX/USDT",
            "baseAsset":             "BTMX",
            "quoteAsset":            "USDT",
            "status":                "Normal",
            "minNotional":           "5",
            "maxNotional":           "100000",
            "marginTradable":         true,
            "commissionType":        "Quote",
            "commissionReserveRate": "0.001",
            "tickSize":              "0.000001",
            "lotSize":               "0.001"
        }
    ]
}
```

**HTTP Request**

`GET /api/pro/products`

#### Response Content

You can obtain a list of all products traded on the exchange through this API.

The response contains the following general fields:

 Name         | Type     | Description                                                                                 
-------------- | -------- | --------------------- 
 `symbol`      | `String` | e.g. `"BTMX/USDT"`
 `baseAsset`   | `String` | e.g. `"BTMX"`
 `quoteAsset`  | `String` | e.g. `"USDT"`
 `status`      | `String` | `"Normal"`

The response also contains criteria for new order request. 

 Name                    | Type      | Description                                                                                 
------------------------ | --------- | --------------------- 
 `minNotional`           | `String`  | minimum notional of an order 
 `maxNotional`           | `String`  | maximum notional of an order 
 `tickSize`              | `String`  | tick size of order price 
 `lotSize`               | `String`  | lot size of order quantity 
 `marginTradable`        | `Boolean` | `true` if the product is tradable in the margin account; `false` otherwise.
 `commissionType`        | `String`  | `"Base"`, `"Quote"`, `"Received"`
 `commissionReserveRate` | `String`  | e.g. `"0.001"`, see below.


When placing orders, you should comply with all criteria above. More details can be found in the [Order Request Criteria](#order-request-criteria) section.


