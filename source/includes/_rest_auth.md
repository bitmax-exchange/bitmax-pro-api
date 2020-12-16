## Authenticate a RESTful Request 

### Create Request 

To access private data via RESTful APIs, you must include the following headers:

* `x-auth-key` - required, the api key as a string. 
* `x-auth-timestamp` - required, the UTC timestamp in milliseconds of your request
* `x-auth-signature` - required, the request signature (see [Sign a Request](#sign-a-request))

The timestamp in the header will be checked against server time. If the difference is greater than 30 seconds, the request will 
be rejected. 


### Sign a Request

> Signing a RESTful Request

```shell
# bash 
APIPATH=info
APIKEY=CEcrjGyipqt0OflgdQQSRGdrDXdDUY2x
SECRET=hV8FgjyJtpvVeAcMAgzgAFQCN36wmbWuN7o3WPcYcYhFd8qvE43gzFGVsFcCqMNk
TIMESTAMP=`date +%s%N | cut -c -13` # 1608133910000
MESSAGE=$TIMESTAMP+$APIPATH
SIGNATURE=`echo -n $MESSAGE | openssl dgst -sha256 -hmac $SECRET -binary | base64`
echo $SIGNATURE  # /pwaAgWZQ1Xd/J4yZ4ReHSPQxd3ORP/YR8TvAttqqYM=

curl -X GET -i \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -H "x-auth-key: $APIKEY" \
  -H "x-auth-signature: $SIGNATURE" \
  -H "x-auth-timestamp: $TIMESTAMP" \
  https://bitmax.io/api/pro/v1/info
```

```python
# python 3.6+
import time, hmac, hashlib, base64

api_path  = "info"
api_key   = "CEcrjGyipqt0OflgdQQSRGdrDXdDUY2x"
sec_key   = "hV8FgjyJtpvVeAcMAgzgAFQCN36wmbWuN7o3WPcYcYhFd8qvE43gzFGVsFcCqMNk"
timestamp = int(round(time.time() * 1e3)) # 1608133910000

message = bytes(f"{timestamp}+{api_path}", 'utf-8')
secret = bytes(sec_key, 'utf-8')

signature = base64.b64encode(hmac.new(secret, message, digestmod=hashlib.sha256).digest())

header = {
  "x-auth-key": api_key,
  "x-auth-signature": signature, 
  "x-auth-timestamp": timestamp,
}
print(signature)  # b'/pwaAgWZQ1Xd/J4yZ4ReHSPQxd3ORP/YR8TvAttqqYM='
```

```java
// java 1.8+
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

To query APIs with private data, you must include a signature using base64 encoded HMAC sha256 algorithm. The prehash string is `<timestamp>+<api-path>`. 
The `timestamp` is the UTC timestamp in milliseconds.  


See the code demos in (`bash`/`python`/`java`) on the right.


