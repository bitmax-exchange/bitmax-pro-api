### Channel: Order

Order update stream is supported on both *account* and *account + symbol* level.

For account level, you could specify account category `cash`, `margin`, or specific account id.

If you already subscribe to *account* level, you cannot subject to *symbol* level. In order to change to *account + symbol* level, unsubscribe from *account* level first, then subscribe to symbol level.

> Subscribe to `cash` account order update stream

```json
{ "op": "sub", "id": "abc123", "ch":"order:cash" }
```

> Subscribe to specific account id *cshQtyfq8XLAA9kcf19h8bXHbAwwoqDoaccount* for order update stream

```json
{ "op": "sub", "id": "abc123", "ch":"order:cshQtyfq8XLAA9kcf19h8bXHbAwwoqDo" }
```

> Subscribe to `cash` account and symbol `BTMX/USDT` order update stream

```json
{ "op": "sub", "id": "abc123", "ch":"order:cash:BTMX/USDT" }
```

> Unsubscribe from `cash` account order update stream

```json
{ "op": "unsub", "id": "abc123", "ch":"order:cash" }
```

> Unsubscribe from `cash` account and symbol `BTMX/USDT` order update stream

```json
{ "op": "unsub", "id": "abc123", "ch":"order:cash:BTMX/USDT" }
```

> Order update message

```json
{
    "m": "order", 
    "accountId": "simtrader0000", 
    "data": {
        "s": "ETC/USDT", 
        "orderId": "16e85af7bc8simtrader0000fb6255dd", 
        "t": 1574200900684, 
        "st": "New", 
        "p": "100.8365", 
        "q": "9.91704", 
        "fp": "0", 
        "fq": "0", 
        "fee": "0", 
        "fa": "base", 
        "bb": "0", 
        "bpb": "0", 
        "qb": "115137.964757493", 
        "qpb": "114136.965153929"
    }
}
```

The `data` field is a single order udpate object.  Each order update object contains the following fields:

Name     | Type | Description                                                                                    
---------| -----| ---------------------------------
`s`      | `String` | symbol
`orderId`| `String` | order id
`t`      | `Long`   | timestamp
`st`     | `String` | order status
`p`      | `String` | order price
`q`      | `String` | order quantity
`fp`     | `String` | filled price
`fq`     | `String` | filled qty
`fee`    | `String` | commission
`fa`     | `String` | fee asset
`bb`     | `String` | base asset total balance
`bpb`    | `String` | base asset available balance
`qb`     | `String` | quote asset total balance
`qpb`    | `String` | quote asset available balance

