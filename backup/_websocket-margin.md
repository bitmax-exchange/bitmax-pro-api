## WebSocket for Margin Trading

<aside class="notice">This API is in beta version and is subject to change. </aside>

**WebSocket URL**

`wss://bitmax.io/<account-group>/api/stream/margin-beta/<symbol>`


### Data Channel - Market Depth

See [cash trading market depth](#data-channel-market-depth)


### Data Channel - Market Trades 

See [cash trading market trades](#data-channel-market-trades)


### Data Channel - Market Summary

See [cash trading market summary](#data-channel-market-summary)


### Data Channel - Bar Data

See [cash trading market bar data](#data-channel-market-bar)


### Data Channel - Reference Prices

> Reference Prices

```json
{
  "m":  "ref-px",  // message
  "ba": "XRP",     // base asset
  "qa": "USDT",    // quote asset
  "p":  "0.3406"   // price 
}
```

Reference prices are composite price indices for the calculation of margin requirement and forced liquidation. 
The reference price is computed by taking an average last trade price from the following five exchanges (upon 
availability at the time of computation) - BitMax.io, Binance, Huobi, OKEx and Poloniex , and removing the 
highest and lowest price. 

BitMax.io reserves the right of updating pricing sources without notice.

The server sends out `ref-px` message every 10 seconds.



### Data Channel - Order Updates

See [cash trading order updates](#data-channel-order-updates)


### Data Channel - Margin Summary 

> Margin Summary

```json 
{
  "m":"margin-summary", // message
  "data": {
    "b":   "100000",  // total balance
    "pb":  "99499.5", // pending (available) balance 
    "nb":  "100000",  // net asset  
    "eim": "0",       // effective initial margin
    "emm": "0",       // effective maintanence margin
    "clv": "1",       // current leverage
    "ilv": "3.0303",  // deprecated, will be removed shortly
    "alv": "10",      // account maximum leverage
    "cus": "-1",      // cusion rate
    "pts": "346"      // point card balance
  }
}
```

The `margin-summary` message contains risk metrics of the overall account. It is important to monitor the risk metrics closely and adjust your positions accordingly 
to avoid forced account liquidation. 

* `b` - account's overall total asset value in USDT calculated based on constituent assets' reference prices. 
* `pb` - account's overall pending (available) asset value in USDT.
* `nb` - account's  overall net asset value, which is calculated as **total asset value - total borrowed amount - total interest owed**, based on USDT value. 
* `eim` - effective initial margin. 
* `emm` - effective maintanence margin.
* `clv` - current leverage. If the net asset value is positive, `clv` is defined as the ratio of total asset value and net asset value; if the net asset value is zero or negative, `clv` is set to be -1 (undefined).
* `ilv` - this field is **deprecated**, it will be removed shortly.
* `alv` - account leverage, the maximum leverage allowed for the current account. This value may increase / decrease based on the account's net asset value
* `cus` - cushion rate, defined as the the ratio of **net asset value** over **effective maintanence margin** if both values are positive. Otherwise, `cus` is set to be -1 (undefined). 
  If cushion rate is defined but below 1, your account could be liquidated at any time. 
* `pts` - the total balance of your point card for margin interest repayment. 

The server emits the `margin-summary` message along with reference prices updates. 


### Data Channel - Margin Balance 

> Margin Balance

```json
{
  "m":"margin-balance", 
  "data": {
    "baseAsset": {
      "a":  "BTC",         // asset code 
      "b":  "0",           // total balance
      "pb": "0",           // pending (available) balance
      "br": "0",           // borrowed amount
      "i":  "0",           // interest owed
      "ms": "0",           // maximum sellable amount
      "r":  "0.00062"      // daily interest rate 
    },
    "quoteAsset": {
      "a":  "USDT",        // asset code 
      "b":  "100000",      // total balance
      "pb": "99499.5",     // pending (available) balance
      "br": "0",           // borrowed amount
      "i":  "0",           // interest owed
      "ms": "117109.454",  // maximum sellable amount
      "r":  "0.0012"       // daily interest rate 
    }
  }
}
```

The `margin-balance` message contains the balance data regarding the current symbol - the symbol specified in the URL of the API call. 

* `a` - asset code
* `b` - the asset's total balance.
* `pb` - the asset's pending (available) balance. You won't incurr any borrowing if you try to sell a quantity less than `pb`.
* `br` - the asset's borrowed amount, in most cases, when `br` is positive, `pb` should be zero, meaning that in order to sell the asset you must increase borrowing. 
* `i` - the asset's total interest owed. 
* `ms` - the asset's maximum sellable amount. It usually includes buying power from your available balance and the additional buying power from your account's borrowing power. 
* `r` - the asset's daily interest rate. 

The server emits the `margin-balance` message along with reference prices updates. 



