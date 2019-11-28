## Data Query / Order Request

Besides subscript mesages, you could also send **request message** via websocket. You will receive exactly one message regarding each 
request message. Here are some use cases: 

* Place/cancel orders 
* Request orderbook snapshot data to initialize/rebuild orderbook. 

### WebSocket Request Schema

All operation or data request follow the same uniform format:

 Name      | Type                   | Required  | Description                                                                                    
---------- | ---------------------- | --------- | ---------------------------------------------------------------------------------------------- 
 `op`      | `String`               | Yes       | `req`                                                                               
 `id`      | `String`               | No        | user specified UUID, if provided, the server will echo back this value in the response message 
 `action`  | `String`               | Yes       | name of the request action with optional arguments, see below for details    
 `account` | `String`               | NO        | the account of the interest, this field is not required for public data request
 `args`    | `List of [key: value]` | No        | each `action` has different args, please see each action for detail.


### WebSocket Response Schema

Response follow the following schema

 Name     | Type               | Description                                                                                    
--------- | ------------------ | ---------------------------------------------------------------------------------------------- 
 `m`      | `String`           | action field from request                                                                               
 `id`     | `Optional[String]` | user specified UUID, if provided, the server will echo back this value in the response message 
 `action` | `String`           | name of the request action with optional arguments, see below for details    
 `args`   | `List[key: value]` | Each `action` has different args, please see each action for detail.


*Ack or Data*

*Error*

