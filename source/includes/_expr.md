# Experimental APIs

## Real Time Level 2 Orderbook Updates

WebSocket messages from the default `depth` channel are throttled with 300 milliseconds throttling intervals. If you want to 
subscribe to realtime orderbook updates, please refer to this [article](https://github.com/bitmax-exchange/bitmax-pro-api/blob/master/misc/bitmax_real_time_orderbook_feed.md).


## Subscribe to Order Channel with Ready Ack Mode

By default, when you subscribe to the order channel via WebSocket, you automatically enter the New Ack Mode. In this mode, when the 
order is accepted by the matching engine, you will receive an order message with status `st=New`. This is true even when the order will 
immediately change status. For instance, when you place a Post-only order that crosses the book, it will immediately be rejected. However, 
in the New Ack Mode, you will first receive an order message with `st=New`, then immediately receive another message with `st=Canceled`. However, 
if your order successfully enters the orderbook without crossing with order on the opposite side, you will only receive one message with `st=New`. 
This makes it hard for trading bots to decide when to take actions.

To address this issue, we introduced the **Ready Ack** mode. Follow this [link](https://github.com/bitmax-exchange/bitmax-pro-api/blob/master/misc/bitmax_ws_order_channel_ready_mode.md) for more details.

