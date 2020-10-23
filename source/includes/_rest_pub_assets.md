### List all Assets

> List all Assets

```
curl -X GET https://bitmax.io/api/pro/v1/assets
```

> Sample Response 

```json
{
    "code": 0,
    "data": [
        {   
	    "assetCode" : "BTC",
    	    "assetName" : "Bitcoin",
    	    "precisionScale" : 9,
    	    "nativeScale" : 8,
    	    "withdrawalFee" : "5.0E-4",
    	    "minWithdrawalAmt" : "0.01",
    	    "status" : "Normal"
        }
    ]
}
```

#### HTTP Request

`GET /api/pro/v1/assets`

You can obtain a list of all assets listed on the exchange through this API.

#### Response Content

 Name               | Type     | Description                                                                                 
------------------- | -------- | --------------------- 
 `assetCode`        | `String` | asset code. e.g. `"BTC"`
 `assetname`        | `String` | full name of the asset, e.g. `"Bitcoin"`
 `minWithdrawalAmt` | `String` | minimum amount required for the withdrawal request e.g. "5.0E-4"
 `nativeScale`      | `Int`    | scale used in deposit/withdraw transaction from/to chain. 
 `positionScale`    | `Int`    | scale used in internal position keeping.
 `withdrawFee`      | `String` | fee charged for each withdrawal request. e.g. "0.01"
 `status`           | `String` | values: `Normal`, `NoDeposit`, `NoWithdraw`, `NoTransaction`
