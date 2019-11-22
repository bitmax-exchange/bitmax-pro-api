## Subscribe to Data Channels

> Use `wscat` from Node.js to connect to websocket data.

```bash
# # Install wscat from Node.js if you haven't
# npm install -g wscat  
npm install -g wscat

# Connect to websocket
wscat -c wss://bitmax.io/0/api/pro/stream -x '{"op":"sub", "ch": "depth:BTMX/USDT"}'
```

> You can also setup authorized session

```bash
@ToDo
```

You can **subscribe/unsubscribe** to one or multiple data channels.

* If the subscription is successful, you will receive one ack message confirming the request is successful and you will start receiving data streams. 
* If the subscription is unsuccessful, you will receive one ack message with text explaining why the subscription failed. 

#### Request Body Schema 

The standard messages to subscribe(`sub`)/unsubscribe(`unsub`) to a data channel is an JSON object with fields:

 Name  | Type               | Description                                                                                    
-------| ------------------ | ---------------------------------------------------------------------------------------------- 
 `op`  | `String`           | `sub` or `unsub`                                                                               
 `id`  | `Optional[String]` | user specified UUID, if provided, the server will echo back this value in the response message 
 `ch`  | `String`           | name of the data channel with optional arguments, see below for details                        


####  Customize Channel content with `ch`

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
