## Getting Event Push
**Create a URL**

Event push is a channel to receive specific delivery results. After you use an API to initiate an emailing request to DMS, it will return the **request result** synchronously and return the **delivery result** and **other event results** asynchronously through event push.

When an event occurs, it will trigger DMS to send data (POST) to your configured URL. After receiving the data, you can parse out the event and corresponding data and perform subsequent operations.

Currently, the following events are supported: request, successful delivery, failed delivery, soft bounce, spam report, open, and click. For specific event message formats, please see [Event Push](https://intl.cloud.tencent.com/document/product/1070/38236).

You can get an event push in the following steps:
1.  Log in to the [DMS Console](https://console.cloud.tencent.com/dms).
2.  Click **Event Push** on the left sidebar and click **Add Push Rule**.
3.  In the pop-up window for adding push rule, enter the configured URL that can correctly respond to GET and POST requests and return a 200 HTTP status code.
4.  Click **Verify**. After the verification succeeds, click **OK**.
> Note: currently, only one URL is supported for event push. You can perform corresponding operations after receiving the event push. If you want to add multiple URLs, please [submit a ticket](https://console.cloud.tencent.com/workorder) for assistance.


**Verify the signature**
To ensure that the message source is DMS, you can perform security verification for the POST data source (you can also skip the verification and directly parse the POST data).

Security verification can be performed as follows:

-   Click **Send Key** to get the `APP KEY`, which DMS will send to your account email address.
-   Parse the POST data to get the `token`, `timestamp`, and `signature`.
-   Use the `APP KEY`, `token`, and `timestamp` to generate a `signature` and compare it with the `signature` in the POST data for verification (signature algorithm: [SHA-256](http://en.wikipedia.org/wiki/SHA-2)).

**Sample code in Python**

```
import hashlib, hmac
def verify(appkey, token, timestamp, signature):
    return signature == hmac.new(
        key=appkey,
        msg='{}{}'.format(timestamp, token),
        digestmod=hashlib.sha256).hexdigest()

```

**Sample code in Java** (dependent on [Apache Codec](http://commons.apache.org/proper/commons-codec/download_codec.cgi))

```
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;

import org.apache.commons.codec.binary.Hex;

public boolean verify(String appkey, String token, long timestamp,
            String signature) throws NoSuchAlgorithmException, InvalidKeyException {
    Mac sha256HMAC = Mac.getInstance("HmacSHA256");
    SecretKeySpec secretKey = new SecretKeySpec(appkey.getBytes(),"HmacSHA256");
    sha256HMAC.init(secretKey);
    StringBuffer buf = new StringBuffer();
    buf.append(timestamp).append(token);
    String signatureCal = new String(Hex.encodeHex(sha256HMAC.doFinal(buf
            .toString().getBytes())));
    return signatureCal.equals(signature);
}

```

**Sample code in PHP**

```
function verify($appkey,$token,$timestamp,$signature){
    $hash="sha256";
    $result=hash_hmac($hash,$timestamp.$token,$appkey);
    return strcmp($result,$signature)==0?1:0;
}
```

**Retry mechanism**

If an error or timeout of URL access occurs, DMS will retry for up to six times. The shortest time intervals between the retries are 3 minutes, 10 minutes, 30 minutes, 1 hour, 6 hours, 12 hours, and 24 hours. This allows you to have enough time to repair the URL before the message gets lost.

If the retry limit is exceeded, DMS will discard the message.

A 200 status code should be returned within 3 seconds for each data parsing during event processing; otherwise, DMS will send the message again.