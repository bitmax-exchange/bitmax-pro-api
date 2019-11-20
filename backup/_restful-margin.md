# RESTful APIs - Margin Trading

A margin account allows you to increase your purchasing power beyond the account total balance by borrowing assets. Compare to cash trading, 
margin trading has more complicated trading rules and may carry much greater risks. Please refer to 
[BitMax.io Margin Trading Rules](https://bitmaxhelp.zendesk.com/hc/en-us/articles/360016415774-BitMax-io-Margin-Trading-Rules) for more details. 


## Get Balance of one Asset of the Margin Account 

[Margin Balance - Single Balance V1](https://github.com/bitmax-exchange/api-doc/blob/master/bitmax-api-doc-v1.2.md#get-balance-of-one-asset-of-the-margin-account-api_pathmarginbalance)



## List all Balance of the Margin Account

[Margin Balance - All V1](https://github.com/bitmax-exchange/api-doc/blob/master/bitmax-api-doc-v1.2.md#list-all-balances-of-the-margin-account-api_pathmarginbalance)

## Get Risk(Summary) of one Symbol of the Margin Account

> Response

```json
{
  "code": 0,
  "data": {
    "totalBalanceInUSDT": "111300.232045955",             //Total Asset (in USDT)
    "netBalanceInUSDT": "106348.644635388",               //Net Asset (in USDT)
    "effectiveInitialMargin": "551.54026784",             //Init. Margin Req.
    "effectiveMaintenanceMargin": "261.184132719",        //Min Margin Req.
    "currentLeverage": "1.0466",                          //Current Leverage
    "accountMaxLeverage": "10",                           //Maximum Leverage
    "cushion": "100",                                     //Cushion Rate
    "pointsBalance": "1.466680936"                        //Available(Pts)
  },
  "email": "xxx@xxx.com",
  "status": "success" // the request has been submitted to the server
}
 ```

**HTTP Request**

`GET <account-group>/api/v2/margin/risk?symbol=<symbol>`

**Authentication**

You must have view permission enabled for the API key.

You must sign message `<timestamp>+margin/risk` and included the signature in the header.

**Parameters**

Name   | Data Type | Description
------ | --------- | -----------------
symbol | String    | symbol, e.g. `"BTC/USDT"`

## Transfer Asset from Cash Account to Margin Account

> Request Body - Transfer Asset from Cash Account to Margin Account

```json
{
  "asset":  "BTC",
  "amount": "1.05"
}
```

> Response

```json
{
  "code": 0,
  "data": {
    "requestId": "ftWU30JpY08Eu8MwmfYPzUX47QkUtsys"
  },
  "email": "xxx@xxx.com",
  "status": "success" // the request has been submitted to the server
}
 ```

**HTTP Request**

`POST <account-group>/api/v2/margin/transfer/deposit`

**Authentication**

You must have transfer permission enabled for the API key.

You must sign message `<timestamp>+margin/transfer/deposit` and included the signature in the header.

**Parameters**

Name   | Data Type | Description
------ | --------- | -----------------
asset  | String    | Asset code, e.g. `"BTC"`
amount | String    | The amount to transfer in string format




## Transfer Asset from Margin Account to Cash Account

> Request Body - Transfer Asset from Margin Account to Cash Account

```json
{
  "asset":  "BTC",
  "amount": "1.05"
}
```

> Response

```json
{
  "code": 0,
  "data": {
    "requestId": "L00HCI4uUQvFLFpguNC8B9zWANGZsJKV"
  },
  "email": "xxx@xxx.com",
  "status": "success" // the request has been submitted to the server
}
 ```

**HTTP Request**

`POST <account-group>/api/v2/margin/transfer/withdraw`


**Authentication**

You must have transfer permission enabled for the API key.

You must sign message `<timestamp>+margin/transfer/withdraw` and included the signature in the header.

**Parameters**

Name   | Data Type | Description
------ | --------- | -----------------
asset  | String    | Asset code, e.g. `"BTC"`
amount | String    | The amount to transfer in string format

