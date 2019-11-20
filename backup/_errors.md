# Error Codes

(Work in progress)

Code  | Message 
----- | -----------------------------------
1900  | Invalid Http Request Input. 
21008 | API key does not have transfer permission
6010  | Not enough balance

## FAQ

### 1900 - Invalid Http Request Input. 

This usually happens when numeric values are provided for parameters of string type. 
For instance, when placing new orders, we require both order price and order quantity 
to be strings. You will receive `error = 1900` if you use numeric value for either of them.

