### Account Info

> Account Info - Sample response:

```json
{
    "code": 0,
    "data": {
        "accountGroup": 0,
        "email": "yzhao0527@gmail.com",
        "cashAccount": [
            "MPXFNEYEJIJ93CREXT3LTCIDIJPCFNIX"
        ],
        "marginAccount": [
            "mar2z3CMIEQx4UvTFbtQ9JcxWJYgHmcb"
        ],
        "tradePermission":    True,
        "transferPermission": True,
        "userUID": "U0866943712",
        "viewPermission":     True
    }
}
```

**HTTP Request** 

`GET /api/pro/info`

**Signature**

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-Request) section.

**prehash string** 

`<timestamp>+info`

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
 `userUID`            | `String`       | an unique id associated with user

See a demo at [query private account info](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_account_info.py).

