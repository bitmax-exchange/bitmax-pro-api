### Channel: Order

Order update stream is supported on both *account* and *account + symbol* level.

For account level, you could specify account category `cash`, `margin`, or specific account id.

If you already subscribe to *account* level, you cannot subject to *symbol* level. In order to change to *account + symbol* level, unsubscribe from *account* level first, then subscribe to symbol level.

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
    "data": {
        "s": "BTC/USDT",
        "orderId": "s16ecd8e618aU9490877774d9f1789b8",
        "t": 1575406690850,
        "sn": 72057600439748931,
        "st": "New",
        "sd": "Buy",
        "ot": "Limit",
        "sp": "0",
        "p": "7105",
        "q": "0.00083",
        "fp": "0",
        "fq": "0",
        "ap": "0",
        "fee": "0",
        "fa": "base",
        "btb": "0.028343365",
        "bab": "0.028343365",
        "qtb": "6305.501839976",
        "qab": "6299.598792826",
        "ac": "cash"
    }
}
```

The `data` field is a single order udpate object.  Each order update object contains the following fields:

Name     | Type     | Description                                                                                    
---------| -------- | ---------------------------------
`s`      | `String` | symbol
`orderId`| `String` | order id
`t`      | `Long`   | timestamp
`sn`     | `long`   | sequence number
`st`     | `String` | order status
`sd`     | `String` | order side
`ot`     | `String` | order type
`sp`     | `String` | stop price
`p`      | `String` | order price
`q`      | `String` | order quantity
`fp`     | `String` | filled price
`fq`     | `String` | filled qty
`ap`     | `String` | average price
`fee`    | `String` | commission
`fa`     | `String` | fee asset
`btb`    | `String` | base asset total balance
`bab`    | `String` | base asset available balance
`qtb`    | `String` | quote asset total balance
`qab`    | `String` | quote asset available balance
`ac`     | `String` | account category, `"cash"`, `"margin"`, etc. 
