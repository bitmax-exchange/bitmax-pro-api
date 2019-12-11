# REST APIs

We always respond with json include `code` field to indicate request result. `0` usually means success response, and you could find data in json format in field `data`; any code other than `0` indicate failure during the request process. For failure response, usually you could find detailed error in fields `message`, `reason`, and possibly extra `info`.

For private data, such as `open order`, `balance`, we usually include `accountId`, and `accountCategory` value in top level of response. 