In order to protect the information security of live streaming, push authentication is enabled for LVB push domain names by default. You can generate the corresponding push address online with the push address generator on the push address details page. By pushing a live stream online with the push address, the stream can be transmitted (uploaded) to LVB.

## Notes

- LVB provides a test domain name `xxxx.livepush.myqcloud.com` by default. You can use it for push testing, but you are not recommended to use it as the push domain name for your real business. 
- Only push addresses in RTMP format can be generated.
- The generated push address is valid before the set expiration time. You need to generate a new address after the old one expires.

## Prerequisites

You have activated the LVB service and completed identity verification.

## Authentication Configuration
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the **push domain** to be configured or **Manage** to enter the domain name details page. 
2. Click **Push Configuration**, view the **Authentication Configuration** section, and click **Edit** on the right.
	![](https://main.qcloudimg.com/raw/9928eda10a0759bcf2a433e101cb3e7d.jpg)
3. Modify the push authentication information and click **Save** to make the change take effect.
![](https://main.qcloudimg.com/raw/315b71b8315d30ade496b3861e8d403c.jpg)


## Push Address Generator

### Directions

1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and select the push domain name to be configured or click **Manage** to enter its details page.
2. Select **Push Configuration** > **Push Address Generator** and configure as follows:
   1. Select an expiration time, such as `2019-10-31 23:59:59`.
   2. Enter a custom `StreamName`, such as `liveteststream`.
   3. Click **Generate Push Address** to generate an RTMP push address containing the `StreamName`.
 ![](https://main.qcloudimg.com/raw/be893a10e50189c1ded53cc03cf6dbe8.jpg)
4. You can test, disable, or delete it in [stream management](https://intl.cloud.tencent.com/document/product/267/31068) after implementing [LVB push](https://intl.cloud.tencent.com/document/product/267/31558) according to your business scenario.
5. After the push address is generated, LVB push can be started. However, to view live streaming, a playback address is required. For more information, please see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).



### Push address description

An RTMP push address is in the following format:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
Here:
- `domain`: LVB push domain name.
- `AppName`: LVB application name, which is `live` by default and customizable.
- `StreamName`: user-defined stream name which is used to identify a live stream.
- `txSecret`: authentication string generated after push authentication is enabled.
- `txTime`: timestamp set for a push address which represents the expiration time of the address in the console.



## Push Address Sample Code

Sample code for generating push addresses in PHP and Java is provided for your reference, which can be viewed in the following way:

1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**.
2. Select a push domain name or click **Manage** on the right to enter its details page.
3. Select **Push Configuration** and scroll down to find **Push Address Sample Code**.
4. Click the tab to view the PHP/Java sample code accordingly.

**Sample code for push (PHP):**

```
/**
    * Get a push address
    * If no `key` and expiration time are passed in, a URL without hotlink protection enabled will be returned
    * @param domain   Your push domain name
    *        streamName   Your unique stream name used to distinguish between different push addresses
    *        key   Security key
    *        time   Expiration time, such as 2016-11-12 12:00:00
    * @return String url
*/
function getPushUrl($domain, $streamName, $key = null, $time = null){
	if($key && $time){
		$txTime = strtoupper(base_convert(strtotime($time),10,16));
		//txSecret = MD5( KEY + streamName + txTime )
		$txSecret = md5($key.$streamName.$txTime);
		$ext_str = "?".http_build_query(array(
			       "txSecret"=> $txSecret,
			       "txTime"=> $txTime
		));
    }
	return "rtmp://".$domain."/live/".$streamName . (isset($ext_str) ? $ext_str : "");
}
echo getPushUrl("123.test.com","123456","69e0daf7234b01f257a7adb9f807ae9f","2016-09-11 20:08:07");
```

**Sample code for push (Java):**

```
package com.test;
import java.io.UnsupportedEncodingException;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
public class Test {
    public static void main(String[] args) {
        System.out.println(getSafeUrl("txrtmp", "11212122", 1469762325L));
    }
    private static final char[] DIGITS_LOWER =
        {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};
    /*
    * KEY+ streamName + txTime
    */
    private static String getSafeUrl(String key, String streamName, long txTime) {
        String input = new StringBuilder().
                            append(key).
                            append(streamName).
                            append(Long.toHexString(txTime).toUpperCase()).toString();
        String txSecret = null;
        try {
            MessageDigest messageDigest = MessageDigest.getInstance("MD5");
            txSecret  = byteArrayToHexString(
                        messageDigest.digest(input.getBytes("UTF-8")));
        } catch (NoSuchAlgorithmException e) {
                e.printStackTrace();
        } catch (UnsupportedEncodingException e) {
                e.printStackTrace();
        }
        return txSecret == null ? "" :
                           new StringBuilder().
                           append("txSecret=").
                           append(txSecret).
                           append("&").
                           append("txTime=").
                           append(Long.toHexString(txTime).toUpperCase()).
                           toString();
        }
    private static String byteArrayToHexString(byte[] data) {
        char[] out = new char[data.length << 1];
        for (int i = 0, j = 0; i < data.length; i++) {
                out[j++] = DIGITS_LOWER[(0xF0 & data[i]) >>> 4];
                out[j++] = DIGITS_LOWER[0x0F & data[i]];
        }
        return new String(out);
    }
}
```
