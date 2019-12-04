## Order 

Trading and Order related APIs. API path usually depend on account-group and account-category: 

  * account-group   : get your account-group from 'Account Info' API

  * account-category: cash or margin

For all order related ack or data, there is *orderId* field to identify the order. 

###
### Generate Order Id

We use the following method to generate an unique id for each order place/cancel request.

**Method**
  
  * A = 'a' for order via rest api, or 's' for order via websocket;

  * B = Convert timestamp (in miliseconds) to hex string;
  
  * C = User UID (11 chars, starting with 'U' followed by 10 digits);
  
  * D = If user provide client order Id (with length >= 9, letters and digits only), then take the right 9 chars; otherwise, we randomly generate 9 chars;
  
  * Final order Id = A + B + C + D.

**Code Sample**

Please refer to python code [gen_server_order_id](https://github.com/bitmax-exchange/bitmax-pro-api-demo/blob/master/python/bitmax/util/auth.py)

