# Private RESTful APIs




### Account Info

> Account Info - Sample response:

```json
{
    "code": 0,
    "data": {
        "accountGroup": 0,
        "cashAccount": [
            "MPXFNEYEJIJ93CREXT3LTCIDIJPCFNIX"
        ],
        "email": "yzhao0527@gmail.com",
        "marginAccount": [
            "mar2z3CMIEQx4UvTFbtQ9JcxWJYgHmcb"
        ],
        "tradePermission":    True,
        "transferPermission": True,
        "viewPermission":     True
    }
}
```

Obtain the account information. 

You can obtain your `accountGroup` from this API, which you will need to include in the URL for all your private RESTful requests.

#### Response Content

 Name                 | Type           | Description                                                                                 
--------------------- | -------------- | --------------------- 
 `accountGroup`       | `Int`          | non-negative integer
 `email`              | `String`       | 
 `cashAccount`        | `List[String]` | 
 `marginAccount`      | `List[String]` | 
 `tradePermission`    | `Boolean`      | 
 `transferPermission` | `Boolean`      | 
 `viewPermission`     | `Boolean`      | 

See a demo at [https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_account_info.py](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_account_info.py).


### Fee Schedule 

@ToDo