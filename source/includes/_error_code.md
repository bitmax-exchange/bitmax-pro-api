
# Error Message

We structure our error message in three levels:
    * Error Group provide a broad error category (Error group id = error code / 10000)
    * Error Reason provide some intuitive information on the error
    * Error Message explains error detail.

In most situation, we provide simple error in this way: *{"code": XYABCDE, "reason": XXXXXXXX}*; for complicated scenatio (such as order place/cancel request, websocket request, and so on), we provide rich format error: *{"code": XYZBCDE, "reason":XXXXXXXX, "message":YYYYYYYY}*.

Rich format error is derived from simple error, so you could get error message with same error *code* and *reason*, but different *message* content.

## Error Base Group

We summary the major error group below.

group name   | group code | derived code | description
-------------|------------| ---------- | ------------
GeneralError | 10  | 10XXXX | Errors applied to general scenario
FormatError  | 15  | 15XXXX | Format related error
AuthError    | 20  | 20XXXX | Auth related error
OrderError   | 30  | 30XXXX | Order action and information related error
MarginError  | 31  | 31XXXX | Margin account and trading related error
SystemError  | 50  | 50XXXX | System related error
BehaviorError| 90  | 90XXXX | Behavior error


## 10XXXX - General Error 

code   | reason                 | descripion
-------|------------------------|---------
100001 |INVALID_HTTP_INPUT      | Http request is invalid
100002 |DATA_NOT_AVAILABLE      | Some required data is missing
100003 |KEY_CONFLICT            | The same key exists already
100004 |INVALID_REQUEST_DATA    | The HTTP request contains invalid field or argument
100005 |INVALID_WS_REQUEST_DATA | Websocket request contains invalid field or argument
100006 |INVALID_ARGUMENT        | The arugment is invalid
100007 |ENCRYPTION_ERROR        | Something wrong with data encryption 
100008 |SYMBOL_ERROR            | Symbol does not exist or not valid for the request
100009 |AUTHORIZATION_NEEDED    | Authorization is require for the API access or request
100010 |INVALID_OPERATION       | The action is invalid or not allowed for the account
100011 |INVALID_TIMESTAMP       | Not a valid timestamp
100012 |INVALID_STR_FORMAT      | String format does not 
100013 |INVALID_NUM_FORMAT      | Invalid number input
100101 | UNKNOWN_ERROR          | Some unknown error

## 15XXXX - Format Error

code  | reason                 | descripion
------|------------------------|---------
150001 |INVALID_JSON_FORMAT    | Require a valid json object

## 20XXXX - Auth Error

Auth related errors.

code   | reason               | descripion
-------|----------------------|---------
200001 |AUTHENTICATION_FAILED | Authorization failed
200002 |TOO_MANY_ATTEMPTS     | Tried and failed too many times 
200003 |ACCOUNT_NOT_FOUND     | Account not exist
200004 |ACCOUNT_NOT_SETUP     | Account not setup properly
200005 |ACCOUNT_ALREADY_EXIST | Account already exist
200006 |ACCOUNT_ERROR         | Some error related with error
200007 |CODE_NOT_FOUND        | 
200008 |CODE_EXPIRED          | Code expired
200009 |CODE_MISMATCH         | Code does not match
200010 |PASSWORD_ERROR        | Wrong assword
200011 |CODE_GEN_FAILED       | Do not generate required code promptly
200012 |FAKE_COKE_VERIFY      |
200013 |SECURITY_ALERT        | Provide security alert message
200014 |RESTRICTED_ACCOUNT    | Account is restricted for certain activity, such as trading, or withdraw.
200015 |PERMISSION_DENIED     | No enough permission for the operation

## 30XXXX - Order Error

Order place/cancel/query related errors. We usually provide rich format errors based on these simple ones.

code   | reason                  | descripion
-------|-------------------------|----------
300001 | INVALID_PRICE           | Order price is invalid
300002 | INVALID_QTY             | Order size is invalid
300003 | INVALID_SIDE            | Order side is invalid
300004 | INVALID_NOTIONAL        | Notional is too small or too large
300005 | INVALID_TYPE            | Order typs  is invalid
300006 | INVALID_ORDER_ID        | Order id is invalid
300007 | INVALID_TIME_IN_FORCE   | Time In Force in order request is invalid
300008 | INVALID_ORDER_PARAMETER | Some order parameter is invalid
300009 | TRADING_VIOLATION       | Trading violation on account or asset
300011 | INVALID_BALANCE         | No enough account or asset balance for the trading
300012 | INVALID_PRODUCT         | Not a valid product supported by exchange
300013 | INVALID_BATCH_ORDER     | Some or all orders are invalid in batch order request
300020 | TRADING_RESTRICTED      | There is some trading restriction on account or asset
300021 | TRADING_DISABLED        | Trading is disabled on account or asset
300031 | NO_MARKET_PRICE         | No market price for market type order trading

## 31XXXX - Margin Error

Margin trading related errors.

code   | reason                  | descripion
-------|-------------------------|----------
310001 | INVALID_MARGIN_BALANCE  | No enough margin balance
310002 | INVALID_MARGIN_ACCOUNT  | Not a valid account for margin trading
310003 | MARGIN_TOO_RISKY        | Leverage is too high
310004 | INVALID_MARGIN_ASSET    | This asset does not support margin trading
310005 | INVALID_REFERENCE_PRICE | There is no valid reference price

## 50XXXX - System Error

code   | reason                  | descripion
-------|-------------------------|----------
510001 | SERVER_ERROR            | Something wrong with server.


## 90XXXX - Behavior Error

code   | reason               | descripion
-------|----------------------|----------
900001 |HUMAN_CHALLENGE       | Human change do not pass