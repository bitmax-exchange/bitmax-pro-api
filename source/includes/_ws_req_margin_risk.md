### WS: Margin Risk for Symbol

>  Request margin risk for symbol `BTC/USDT`

```json
{
    "op": "req", 
    "action": "margin-risk", 
    "id": "abcefg", 
    "account": "margin", 
    "args": {
        "symbol": "BTC/USDT"
    }
}
```

> Margin Risk Response 

```json
{
    "m":"margin-risk", 
    "accountId":"marGad02EnGqSo6P2SMBoNUX4lGyxjsy",
    "ac":"MARGIN", 
    "id":"abcefg", 
    "data": {
        "tb":"14058.242182715",
        "ab":"14058.242182715",
        "nb":"14058.242182715",
        "eim":"0",
        "emm":"0",
        "clv":"1",
        "ilv":"3",
        "alv":"10",
        "cus":"-1",
        "pts":"0"
    }
}
```

You can request margin risk for a symbol via websocket by an `margin-risk` request. 

The `args` schema:

 Name          | Data Type           | Description                
-------------- | ------------------- | -------------------------- 
 `op`          | `String`            | `req`                      
 `action`      | `String`            | `depth-snapshot`      
 `id`          | `String`            | for result match purpose     
 `args:symbol` | `String`            | Symbol, e.g. `BTMX/USDT`   

The response schema:

 Name             | Data Type | Description                   
----------------- | ----------| ----------------------------- 
 `m`              | `String`  | `depth-snapshot`
 `accountId`      | `String`  | margin accountId
 `ac`             | `String`  | `MARGIN`
 `symbol`         | `String`  | Symbol, e.g. `BTMX/USDT`  
 `id`             | `String`  | echo back `id` in request    
 `data`           | `Json`    | See `data` detail below

`data` field detail

 Name   | Data Type | Description                   
--------| ----------| ----------------------------- 
 `tb`   | `String`  | total balance                               
 `ab`   | `String`  | available balance    
 `nb`   | `String`  | net balance  
 `eim`  | `String`  |
 `emm`  | `String`  | 
 `clv`  | `String`  | 
 `ilv`  | `String`  | 
 `cus`  | `String`  |            
 `pts`  | `String`  |        
