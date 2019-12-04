## Data Query / Order Request

Besides subscript mesages, you could also send **request message** via websocket. You will receive exactly one message regarding each 
request message. Here are some use cases: 

* Place/cancel orders 
* Request orderbook snapshot data to initialize/rebuild orderbook. 

### WebSocket Request Schema

All operation or data request follow the same uniform format:

 Name      | Type         | Required| Value                  |Description                                            
---------- | -------------| --------| ---------------------- | ---------------------------------------------------------------------------------------- 
 `op`      | `String`     | Yes     | `req`                  |                                                                                 
 `id`      | `String`     | No      | digits and numbers     | if provided, the server will echo back this value in the response message 
 `action`  | `String`     | Yes     | See below              | name of the request action with optional arguments  
 `account` | `String`     | NO      | `cash`, `margin`       | the account of the interest, this field is not required for public data request
 `args`    | `{key:value}`| No      |                        | each `action` has different args, please see each action for detail.

supported action


### WebSocket Response Schema

We try to provide all data in consistent format.

*Ack or Data*

Response follow the following schema

 Name          | Type               | Description                                                                                    
---------------| ------------------ | ---------------------------------------------------------------------------------------------- 
 `m`           | `String`           | message topic related with request `action`                                                                              
 `id`          | `Optional[String]` | user specified UUID, if provided, the server will echo back this value in the response message 
 `action`      | `String`           | echo `action` in request    
 `data` or 
 <br>`info`<br>| `Json`             | detailed `data` for data request, or `info` for operation result(e.g. order place/cancel)

*Error*


