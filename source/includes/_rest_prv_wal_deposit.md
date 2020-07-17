### Query Deposit Addresses

> Query Deposit Addresses - Sample Response


```json
{
    "code": 0,
    "data": {
        "asset": "USDT",
        "assetName": "Tether",
        "address": [{
                "address": "1P67...TnG3",
                "blockchain": "Omni",
                "destTag": ""
            },
            {
                "address": "0xd3...c466",
                "blockchain": "ERC20",
                "destTag": ""
            },
            {
                "address": "TPpK...ovJk",
                "blockchain": "TRC20",
                "destTag": ""
            }
        ]
    }
}
```

#### HTTP Request

`GET /api/pro/v1/wallet/deposit/address`

#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-request) section.

#### Prehash String

`<timestamp>+wallet/deposit/address`


#### Request Parameters

Name           |  Type     | Required | Value Range       | Description
-------------- | --------- | -------- | ----------------- | -----------
**asset**      | `String`  |   Yes    | valid asset code  | this allow you query single asset balance, e.g. `BTC`
**blockchain** | `Boolean` |   No     | blockchain name   | the (optional) blockchain filter 


#### Response Content

 Name                | Type     | Description             | Sample Response
-------------------- | -------- | ----------------------- | -------------------------
**asset**            | `String` | asset code              | `"USDT"`
**assetName**        | `String` | asset name              | `"Tether"`
**address**          | `List`   | list of address objects |

Content of elements in the `address` field:

 Name          | Type     | Description             | Sample Response
-------------- | -------- | ----------------------- | -------------------------
**address**    | `String` | wallet address          | 
**blockchain** | `String` | blockchain name         | `"ERC20"`
**destTag**    | `String` | the destination tag (or memo for some tokens) attached to the address. This field could be an empty string. |


#### Code Sample

Please refer to python code to [query deposit addresses](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_deposit_address.py)


