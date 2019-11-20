# WebSocket 


## Data Channels 

### Subscription 

> Use `wscat` from Node.js to connect to websocket data.

```bash
# install wscat if you haven't
npm install -g wscat

# Connect to websocket
wscat -c wss://bitmax-test.io/0/api/t/stream -x '{"op":"sub", "ch": "depth:BTMX/USDT"}'


echo '{"op":"sub", "ch": "depth:BTMX/USDT"}' > wscat -c wss://bitmax.io/0/api/t/stream
```

> You can also setup authorized session

```bash
@ToDo
```

### URL 

`<account-group>/api/pro/stream`


In order to authorize the sessionm you must include `<account-group>` in the URL. Without `<account-group>`, you can 
only subscribe to public data. 

### Request Body Schema 

The standard messages to subscribe(`sub`)/unsubscribe(`unsub`) to a data channel is an JSON object with fields:

 Field | Type               | Description                                                                                    
-------| ------------------ | ---------------------------------------------------------------------------------------------- 
 `op`  | `String`           | `sub` or `unsub`                                                                               
 `id`  | `Optional[String]` | user specified UUID, if provided, the server will echo back this value in the response message 
 `ch`  | `String`           | name of the data channel with optional arguments, see below for details                        


###  Customize Channel content with `ch`

You can subscription to different data channels by setting `ch` to `name:<arg1>[:<arg2>]` with `arg1` being the required argument 
and `arg2` being optinal:

 Type    | Value                        | Description                                      
-------- | ---------------------------- | ------------------------------------------------ 
 public  | `depth:<symbol>`             |                                                  
 public  | `bbo:<symbol>`               |                                                  
 public  | `trade:<symbol>`             |                                                  
 public  | `bar:<symbol>`               |                                                  
 public  | `ticker:<symbol>`            |                                                  
 public  | `ref-px:<symbol>`            | Reference prices used by margin risk Calculation 
 Private | `order:<account>`            | Order Update Stream                              
 Private | `order:<account>[:<symbol>]` |                                                  

You can subscribe/unsubscribe one channel per subscription message. You can subscribe to multiple data channels by sending multiple 
subscription messages. However, the exchange limits the total number of data channels per client (**NOT per session**) according to 
the following rules:

@ToDo rule: maximum number of channels 


## Operation or Data Request

You could place/cancel order and take snapshot for some data via websocket.

### Request Schema

All operation or data request follow the same uniform format:

 Field   | Type                 | Description                                                                                    
---------| ---------------------| ---------------------------------------------------------------------------------------------- 
 `op`    |`String`              | `req`                                                                               
 `id`    |`Optional[String]`    | user specified UUID, if provided, the server will echo back this value in the response message 
 `action`|`String`              | name of the request action with optional arguments, see below for details    
 `args`  |`List of [key: value]`| Each `action` has different args, please see each action for detail.


### Response 

Response follow the following schema

 Field | Type               | Description                                                                                    
-------| ------------------ | ---------------------------------------------------------------------------------------------- 
 `m`  | `String`            | action field from request                                                                               
 `id`  | `Optional[String]` | user specified UUID, if provided, the server will echo back this value in the response message 
 `action`| `String`           | name of the request action with optional arguments, see below for details    
 `args` | `List of [key: value]` | Each `action` has different args, please see each action for detail.


*Ack or Data*

*Error*



### Data


### Order

