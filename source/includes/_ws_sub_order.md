### Channel: Order

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
    "accountCategory": "CASH",
    "data": {
        "ap": "0",
        "bab": "0.028343365",
        "btb": "0.028343365",
        "cf": "0",
        "cfq": "0",
        "err": "",
        "fa": "base",        
        "orderId": "s16ecd8e618aU9490877774d9f1789b8",
        "ot": "Limit",
        "p": "7105",
        "q": "0.00083",
        "qab": "6299.598792826",
        "qtb": "6305.501839976",
        "s": "BTC/USDT",
        "sd": "Buy",
        "sn": 72057600439748931,
        "sp": "0",
        "st": "New",
        "t": 1575406690850,
    }
}
```

Order update stream is supported on both *account* and *account + symbol* level.

For account level, you could specify account category `cash`, `margin`, or specific account id.

If you already subscribe to *account* level, you cannot subject to *symbol* level. In order to change to *account + symbol* level, unsubscribe from *account* level first, then subscribe to symbol level.

The `data` field is a single order udpate object.  Each order update object contains the following fields:

Name     | Type     | Description                                                                                    
---------| -------- | ---------------------------------
`ap`     | `String` | average fill price
`bab`    | `String` | base asset available balance
`btb`    | `String` | base asset total balance
`cf`     | `String` | cumulated commission
`cfq`    | `String` | cumulated filled qty
`err`    | `String` | error code
`fa`     | `String` | fee asset
`orderId`| `String` | order id
`ot`     | `String` | order type
`p`      | `String` | order price
`q`      | `String` | order quantity
`qab`    | `String` | quote asset available balance
`qtb`    | `String` | quote asset total balance
`s`      | `String` | symbol
`sd`     | `String` | order side
`sn`     | `long`   | sequence number
`sp`     | `String` | stop price
`st`     | `String` | order status
`t`      | `Long`   | latest execution timestamp
