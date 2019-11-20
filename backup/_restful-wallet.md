# RESTful APIs - Wallet(Deposit and Withdraw)



## Get Deposit address of one Asset

> Response example (asset = USDT which has two blockchains) 

```json
{
  "code": 0,
  "data": [
    {
     "asset": "USDT",
     "blockChain": "Omni",
     "addressData": {"address": "17nbKg26jBStZHmdq9jLETHPh8EzjiaQ9J"}
    },
    {
     "asset": "USDT",
     "blockChain": "ERC20",
     "addressData": {"address": "0x7dcf0192e4a78593fd360dbc2fa50855a3f4505a"}
    }
  ],
  "email": "xxx@xxx.com",
  "status": "success" // the request has been submitted to the server
}
 ```
 > Response example (asset = XRP which requires both Tag and deposit address for deposit) 

```json
{
  "code": 0,
  "data": [
    {
     "asset": "XRP",
     "blockChain": "Ripple",
     "addressData": 
         {
         "address": "rpinhtY4p35bPmVXPbfWRUtZ1w1K1gYShB",
         "destTag": "54301"
         }
    }
  ],
  "email": "xxx@xxx.com",
  "status": "success" // the request has been submitted to the server
}
 ```



**HTTP Request**

`GET <account-group>/api/v2/deposit?asset=<asset>`

**Authentication**

You must have view permission enabled for the API key.

You must sign message `<timestamp>+deposit` and included the signature in the header.

**Parameters**

Name   | Data Type | Description
------ | --------- | -----------------
asset  | String    | Asset code, e.g. `"BTC"`






