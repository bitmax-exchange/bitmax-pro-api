### Query Wallet Transaction History

> Query Wallet Transaction History - Sample Response

```json
{
    "code": 0,
    "data": {
        "data": [{
                "asset": "USDT",
                "amount": "400",
                "commission": "0",
                "destAddress": {
                    "address": "1wX8...iHih"
                },
                "networkTransactionId": "Slc8...xo2d",
                "numConfirmations": 3,
                "numConfirmed": 0,
                "requestId": "ZgO7...cctn",
                "status": "confirmed",
                "time": 1595001735000,
                "transactionType": "withdrawal"
            }
        ],
        "hasNext": true,
        "page": 1,
        "pageSize": 2
    }
}
```


#### HTTP Request

`GET /api/pro/v1/wallet/transactions`


#### Signature

You should sign the message in header as specified in [**Authenticate a RESTful Request**](#sign-a-request) section.

#### Prehash String

`<timestamp>+wallet/transactions`


#### Request Parameters

Name          |  Type    | Required | Value Range         | Description
------------- | -------- | -------- | ------------------- | -----------
**asset**     | `String` |   No     | valid asset code    | this allow you query single asset balance, e.g. `BTC`
**txType**    | `String` |   No     | deposit / withdrwal | add the (optional) transaction type filter
**page**      | `Int`    |   No     | a positive interger | the page number, starting at 1
**pageSize**  | `Int`    |   No     | a positive interger | the page size, must be positive


#### Response Content

 Name                    | Type     | Description                                                                        | Sample Response
------------------------ | -------- | ---------------------------------------------------------------------------------- | -------------------------
**asset**                | `String` | asset code                                                                         | `"USDT"`
**amount**               | `String` | the transaction amount                                                             | `"400"`
**commission**           | `String` | the commission charged by the exchange                                             | `"0"`
**destAddress**          | `Object` | the destination address, see below for details                                     |
**networkTransactionId** | `String` | the transaction hash ID                                                            |
**numConfirmations**     | `Int`    | the minimun number of confirmations for the transaction to be viewed as confirmed. |
**numConfirmed**         | `Int`    | current number of confirmations                                                    |
**requestId**            | `String` | the requestId of the request                                                       | 
**status**               | `String` | `pending` / `reviewing` / `confirmed` / `rejected` / `canceled` / `failed`         |
**time**                 | `Long`   | UTC timestamp in milliseconds, timestamp of the transaction.                       |
**transactionType**      | `String` | `deposit` / `withdrawal`                                                           |

Content of elements in the `destAddress` field:

 Name       | Type               | Description     
----------- | ------------------ | ----------------
**address** | `String`           | wallet address  
**destTag** | `Optional[String]` | the destination tag (or memo for some tokens) attached to the address. This field could be an empty string.


#### Code Sample 

Please refer to python code to [query wallet transactions](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/query_prv_wallet_tx_hist.py)
