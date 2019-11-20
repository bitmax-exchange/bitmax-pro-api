# Authentication

The authentication process for `v2` APIs are a bit different from the old version:

* We now enforce strong timestamp check.
* The response of the API call is more informative in case of authentication failure. 


## Creating a Request 

To access private data, you must include the following headers:

* `x-auth-key` - required, the api key as a string. 
* `x-auth-timestamp` - required, the UTC timestamp in milliseconds of your request
* `x-auth-signature` - required, the request signature (see #signing-a-request)
* `x-auth-coid` - the request Id, only required certain APIs (such as placing/canceling orders)

## Signing a Request

> Signing a request

```shell
# bash 
APIPATH=user/info
APIKEY=CEcrjGyipqt0OflgdQQSRGdrDXdDUY2x
SECRET=hV8FgjyJtpvVeAcMAgzgAFQCN36wmbWuN7o3WPcYcYhFd8qvE43gzFGVsFcCqMNk
TIMESTAMP=`date +%s%N | cut -c -13` # 1562952827927
MESSAGE=$TIMESTAMP+$APIPATH
SIGNATURE=`echo -n $MESSAGE | openssl dgst -sha256 -hmac $SECRET -binary | base64`
echo $SIGNATURE  # vBZf8OQuiTJIVbNpNHGY3zcUsK5gJpwb5lgCgarpxYI=

curl -X GET -i \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -H "x-auth-key: $APIKEY" \
  -H "x-auth-signature: $SIGNATURE" \
  -H "x-auth-timestamp: $TIMESTAMP" \
  https://bitmax.io/api/v1/user/info
```

```python
# python 3.6+
import time, hmac, hashlib, base64

api_path  = "user/info"
api_key   = "CEcrjGyipqt0OflgdQQSRGdrDXdDUY2x"
sec_key   = "hV8FgjyJtpvVeAcMAgzgAFQCN36wmbWuN7o3WPcYcYhFd8qvE43gzFGVsFcCqMNk"
timestamp = int(round(time.time() * 1e3)) # 1562952827927

message = bytes(f"{timestamp}+{api_path}", 'utf-8')
secret = bytes(sec_key, 'utf-8')

signature = base64.b64encode(hmac.new(secret, message, digestmod=hashlib.sha256).digest())

header = {
  "x-auth-key": api_key,
  "x-auth-signature": signature, 
  "x-auth-timestamp": timestamp,
}
print(signature)  # b'vBZf8OQuiTJIVbNpNHGY3zcUsK5gJpwb5lgCgarpxYI='
```

```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import org.apache.commons.codec.binary.Base64;

public class SignatureExample {

  public static void main(String[] args) {
    try {
      long timestamp = System.currentTimeMillis(); // 1562952827927
      String api_path = "user/info";
      String secret = "hV8FgjyJtpvVeAcMAgzgAFQCN36wmbWuN7o3WPcYcYhFd8qvE43gzFGVsFcCqMNk";
      String message = timestamp + "+" + api_path;

      Mac sha256_HMAC = Mac.getInstance("HmacSHA256");
      SecretKeySpec secret_key = new SecretKeySpec(secret.getBytes(), "HmacSHA256");
      sha256_HMAC.init(secret_key);

      String hash = Base64.encodeBase64String(sha256_HMAC.doFinal(message.getBytes()));
      System.out.println(hash); // vBZf8OQuiTJIVbNpNHGY3zcUsK5gJpwb5lgCgarpxYI=
    }
    catch (Exception e) {
      System.out.println("Error");
    }
  }
}
```

To query APIs with private data, you must include a signature using base64 encoded HMAC sha256 algorithm.




## Error Code

> Example: HTTP response when authentication failed

```json
// HTTP Response Status Code: 405 - Method Not Allowed
{
  "code":  21001,
  "msg": "xxx", 
}
```

If authentication failed, the server will response with `status code` other than `200 OK`. The respond body will contain more details including
the `code` field with value other than `0` and a `message` field with text explaining why the authentication failed. 

The table below lists all possible server responses if the request is rejected due to authentication failure. 

HTTP Status Code       | ErrorCode  | Description 
-----------------------| ---------- | ---------------------------------------------
405 Method Not Allowed | 21001      | API Access is currently disabled.
400 Bad Request        | 21002      | API header is missing.
400 Bad Request        | 21003      | Request ID Mismatch.
400 Bad Request        | 21004      | API request header error: invalid timestamp. This typically means the timestamp in request header differs from system time by more than 60 seconds.
400 Bad Request        | 21006      | Unable to find API key.
410 Gone               | 21005      | Unable to verify API signature: expired timestamp.
403 Forbidden          | 21007      | API key does not have view permission.
403 Forbidden          | 21010      | API key does not have withdraw permission.
403 Forbidden          | 21009      | API key does not have trade permission.
403 Forbidden          | 21008      | API key does not have transfer permission.
401 Unauthorized       | 2012       | Account group mismatch.
401 Unauthorized       | 21011      | Unable to verify API signature: signature mismatch.

