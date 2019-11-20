WebSocket API (Beta Version)
===========================================================

## WebSocket Data Feed 

> websocket URL examples:

```
wss://bitmax.io/3/api/stream/cash-beta/ETH-BTC
wss://bitmax.io/3/api/stream/margin-beta/ETH-BTC
```

**WebSocket URL**

* cash trading: `wss://bitmax.io/<account-group>/api/stream/cash-beta/<symbol>`
* margin trading:  `wss://bitmax.io/<account-group>/api/stream/margin-beta/<symbol>`

Note: `<symbol>` in URLs above must be seperated by hyphen (`-`), e.g, `ETH-BTC`. Symbols separated by slash (`/`) are not allowed. 

**Authorization**

You must have view permission enabled for your API key to open websocket connection. If you want to place orders, you will need trade 
permission enabled as well.

You must sign the following messages and included the signature in the header:

* cash trading: `<timestamp>+stream/cash-beta`
* margin trading: `<timestamp>+stream/margin-beta`


### WebSocket Authentication 

Connecting to websocket API follows almost the same authentication process as authenticated RESTful APIs. You need to include the following
fields in the request header:

* `x-auth-key` - the API key with view permission. Trade permission is needed if you want to place orders.
* `x-auth-signature` - the request signature.
* `x-auth-timestamp` - the current UTC timestamp in milliseconds.


### Subscribe to WebSocket Streams 

After connecting to websocket, you need to send an `subscribe` message to start receiving data. (Note that unlike V1, you will not receive any data unless you sent the `subscribe` in V2) The subscribe message is a JSON object 
in plain text format and contains the following fields:

> Subscribe Message

```json
{
  "messageType": "subscribe",
  "marketDepthLevel": 20,
  "recentTradeMaxCount": 20,
  "skipSummary": false,
  "skipBars": false
}
```

Field Name            | Data Type | Description
--------------------- | --------- | -----------
`messageType`         | String    | set this field to `subscribe` in the subscribe message.
`marketDepthLevel`    | Integer   | optional, default value 20. This field specifies the max number of price levels on each side to be included in the first market depth message.
`recentTradeMaxCount` | Integer   | optional, default value 20. This field specifies the max number of recent trades to be included in the first market trades message.
`skipSummary`         | Boolean   | optional, default value `false`. If `false`, client will receive market summary data with rolling 24 hour O/H/L/C price data for all symbols every 30 seconds.
`skipBars`            | Boolean   | optional, default value `false`. If `false`, client will receive bar data of all frequencies (1 minute, 5 minutes, etc.) for the current symbol every 30 seconds.

After sending `subscribe` message, you will receive a message indicating the subscription is successful or not. 
> Success Subscribe Message (Success Response)

```json
{
"m": "subscribe",
"msg": "success"
}
```
Field Name | Data Type | Description
-----------| --------- | -----------
`m`        | String    | `subscribe` if the subscription succeeds, `error` if it fails
`msg`      | String    | `success` if the subscrioption succeeds, or it will print out the error message

### Ping/Pong

After connected to websocket, you can send a `ping` message to the server. After receiving the `ping` message, the server will response with a `pong` message. The `pong` message has a `ts` field indicating the server time .
> Ping Message

```json
{
"messageType": "ping"
}
```

> Pong Message

```json
{
"m": "pong",
"ts": 1569016717541
}
```


Field Name | Data Type | Description
-----------| --------- | -----------
`m`        | String    | `pong`
`ts`       | Long      |  timestamp of the server time in milliseconds



