## Order 

Trading and Order related APIs. API path usually depend on account-group and account-category: 

  * account-group   : get your account-group from 'Account Info' API

  * account-category: cash or margin

For all order related ack or data, there is *orderId* field to identify the order. 

###
### Order id generation method

We use the following method to generate an unique id for each order place/cancel request.

**Method**
  
  * A = Convert timestamp (in miliseconds) to hex string;

  * B = 'a' for order via rest api, or 's' for order via websocket;
  
  * C = Account Id + Symbol + 'b' for buy or 's' for sell + User generated 32 chars order id;
  
  * D = first 11 chars of A  + B + last 12 chars of Account Id + MD5(C);
  
  * Final order Id = first 32 chars of D.

**Code Sample**

Please refer to python code [gen_server_order_id](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/bitmax/util/auth.py)

