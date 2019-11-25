## Keep the Connection Alive via Ping/Pong

In order to keep the websocket connection alive, you have two options, detailed below.


#### Method 1: Responding to Server ping messages

> Method 1. keep the connection alive by responding to Server pushed ping message 

```
>>> { "op": "ping" }  # Server pushed ping message
<<< { "m": "pong" }   # Client responds with pong
```

If the server doesn't receive any client message after a while, it will send a `ping` message to the client. Once the `ping` message is received,
the client should promptly send a `pong` message to the server. If you missed two consecutive `ping` messages, the session will be disconnected. 


#### Method 2: Sending ping messages to Server 

> Method 2. keep the connection alive by sending ping message to the server

```
>>> { "op": "ping" }                             # Client initiated ping message (every 30 seconds)
<<< { "m":"pong", "code":0, "ts":1574260701259 } # Server responds to client ping 
``` 

You can also send `ping` message to the server every 15 seconds to keep the connection alive. The server will stop sending `ping` message 
for 30 seconds if a client initiated `ping` message is received. 

