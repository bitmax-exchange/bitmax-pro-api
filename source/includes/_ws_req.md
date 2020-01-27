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


####Supported action


Name                    | Description
------------------------|---------------------------------
`place-order`           | Place new order
`cancel-order`          | Cancel exisitng open order
`cancel-all`            | Cancel all open orders on account level
`batch-place-order`     | Place new order in batch
`batch-cancel-order`    | Cancel orders in batch
`depth-snapshot`        | Get market depth for symbol up to 500 level
`depth-snapshot-top100` | Get top 100 depth
`market-trades`         | Get market trades for a symbol
`balance`               | Request balance
`open-order`            | Query open order
`margin-risk`           | Get margin risk


### WebSocket Response Schema

We try to provide all data in uniform format.

*Ack or Data*

Response follow the following schema

 Name          | Type               | Description                                                                                    
---------------| ------------------ | ---------------------------------------------------------------------------------------------- 
 `m`           | `String`           | message topic related with request `action`                                                                              
 `id`          | `Optional[String]` | user specified UUID, if provided, the server will echo back this value in the response message 
 `action`      | `String`           | echo `action` field in request    
 `data` or `info`| `Json`   | detailed `data` for data request, or `info` for operation result(e.g. order place/cancel)


*Error*

 Name          | Type               | Description                                                                                    
---------------| ------------------ | ---------------------------------------------------------------------------------------------- 
 `m`           | `String`           | "error"                                                                        
 `id`          | `String`           | Echo back the error 
 `code`        | Long               |
 `reason`      | `String`           | simple error  message
`info`         | `String`           | detailed error message


> Example error response

```json
{
    "m":      "error",
    "id":     "ab123",
    "code":   100005,
    "reason": "INVALID_WS_REQUEST_DATA",
    "info":   "Invalid request action: trade-snapshot"
}
```