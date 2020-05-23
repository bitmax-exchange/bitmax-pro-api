### Channel: Order (and Balance)

> Subscribe to `cash` account order update stream

```json
{ "op": "sub", "id": "abc123", "ch":"order:cash" }
```

> Subscribe to specific account id *cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo* account for order update stream

```json
{ "op": "sub", "id": "abc123", "ch":"order:cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo" }
```

> Unsubscribe from `cash` account order update stream

```json
{ "op": "unsub", "id": "abc123", "ch":"order:cash" }
```


> Order update message

```json
{
    "m": "order", 
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo", 
    "ac": "CASH", 
    "data": {
        "s":       "BTC/USDT", 
        "sn":       8159711, 
        "sd":      "Buy", 
        "ap":      "0", 
        "bab":     "2006.5974027", 
        "btb":     "2006.5974027",
        "cf":      "0", 
        "cfq":     "0", 
        "err":     "", 
        "fa":      "USDT",
        "orderId": "s16ef210b1a50866943712bfaf1584b", 
        "ot":      "Market", 
        "p":       "7967.62", 
        "q":       "0.0083", 
        "qab":     "793.23", 
        "qtb":     "860.23", 
        "sp":      "", 
        "st":      "New", 
        "t":        1576019215402,
        "ei":      "NULL_VAL"
    }
}
```

> Balance Update Message (Cash Account)

```json
{
    "m": "balance",
    "accountId": "cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo",
    "ac": "CASH",
    "data": {
        "a" : "USDT",
        "sn": 8159798,
        "tb": "600",
        "ab": "600"
    }
}
```

> Balance Update Message (Margin Account)

```json
{
    "m": "balance",
    "accountId": "marOxpKJV83dxTRx0Eyxpa0gxc4Txt0P",
    "ac": "MARGIN",
    "data": {
        "a"  : "USDT",
        "sn" : 8159802,
        "tb" : "400",
        "ab" : "400",
        "brw": "0",
        "int": "0"
    }
}
```


Note: once you subscribe to the **order** channel, you will start receiving messages from the **balance** channel automatically. If you unsubscribe from the **order** channel, you will simultaneously unsubscribe from the **balance** channel.

You need to specify the account when subscribing to the order channel. You could specify account category `cash`, `margin`, or specific account id.

#### Order Messages

You can track the state change of each order thoughout its life cycle with the order update message (`m=order`). The `data` field is a single order udpate object.  Each order update object contains the following fields:

Name     | Type     | Description                                                                                    
---------| -------- | ---------------------------------
`s`      | `String` | symbol
`sn`     | `long`   | sequence number
`ap`     | `String` | average fill price
`bab`    | `String` | base asset available balance
`btb`    | `String` | base asset total balance
`cf`     | `String` | cumulated commission
`cfq`    | `String` | cumulated filled qty
`err`    | `String` | error code; could be empty
`fa`     | `String` | fee asset
`orderId`| `String` | order id
`ot`     | `String` | order type
`p`      | `String` | order price
`q`      | `String` | order quantity
`qab`    | `String` | quote asset available balance
`qtb`    | `String` | quote asset total balance
`sd`     | `String` | order side
`sp`     | `String` | stop price; could be empty
`st`     | `String` | order status
`t`      | `Long`   | latest execution timestamp
`ei`     | `String` | execution instruction

#### Balance Messages

You will also receive balance update message (`m=balance`) for the asset balance updates not caused by orders. For instance, when you make wallet deposits/withdrawals, or when you transfer asset from the cash account 
to the margin account, you will receive balance update message.

For *Cash Account Balance Update*, the data field contains:

Name     | Type     | Description                                                                                    
---------| -------- | ---------------------------------
`a`      | `String` | asset
`sn`     | `long`   | sequence number
`tb`     | `String` | total balance
`ab`     | `String` | available balance

For *Margin Account Balance Update*, the data field contains:

Name     | Type     | Description                                                                                    
---------| -------- | ---------------------------------
`a`      | `String` | asset
`sn`     | `long`   | sequence number
`tb`     | `String` | total balance
`ab`     | `String` | available balance
`brw`    | `String` | borrowed amount
`int`    | `String` | interest amount

