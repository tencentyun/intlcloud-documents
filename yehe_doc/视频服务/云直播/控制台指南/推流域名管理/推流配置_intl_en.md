To protect the information security of live streaming, push authentication is enabled for CSS push domain names by default. You can use the push address generator on the push address details page to generate a push URL. Then, you can use the URL to push the stream (upload the live streaming video) to the CSS platform.

## Notes

- CSS provides a test domain name `xxxx.tlivepush.com`. You can use it to test live push, but you’re not advised to use it as the push domain name for business purposes. 
- CSS can only generate push URLs in RTMP format.
- The generated push URL is valid before the set expiration time. You can generate a new URL after the old one expires.

## Prerequisites

You have activated the CSS service and completed identity verification.

## Authentication Configuration
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the target **push domain name** or click **Manage** to enter the domain details page. 
2. Click **Push Configuration**, view the **Authentication Configuration** section, and click **Edit** on the right.
	![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
3. On the **Authentication Configuration** page, toggle ![](https://main.qcloudimg.com/raw/5637a9d55de965fa5d35725a955f4c00.png) to enable or disable push configuration.
4. Enter the primary key and backup key, and click **Save**.
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
>? Primary key is required and backup key is optional. Entering both allows you to switch keys when one key is disclosed.

## Push Address Generator

### Directions
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the target domain name or click **Manage** on its right to enter its details page.
2. Select **Push Configuration** and, in **Push Address Generator**, complete the following settings:
   1. Select an expiration time, such as `2021-06-30 19:26:02`.
   2. Enter a custom `StreamName`, such as `liveteststream`.
   3. Click **Generate Push Address** to generate an RTMP push URL containing the `StreamName`.
![](https://main.qcloudimg.com/raw/6f5ac8dcac2082aedca950c5341946ab.png)
3. If you haven’t enabled authentication for your push domain, you can find RTMP and UDP URLs in the **Push URL** section. Replace `StreamName` with your stream name and you can use the corresponding playback URLs to play the stream. 
![](https://main.qcloudimg.com/raw/aa129bd839cb307993bfed247e636a41.png)



### Notes

RTMP push URL format:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
Where:
- `domain`: push domain name
- `AppName`: live streaming application name, which is `live` by default and customizable
- `StreamName`: custom stream name used to identify a live stream
- `txSecret`: authentication string generated after push authentication is enabled
- `txTime`: expiration timestamp set for a push URL in the console

>!
>- If you have enabled authentication, the actual expiration time of a URL will be `txTime` plus the validity period of the key.
>- For the sake of convenience, the time you set in the console is the actual expiration time. **If you have enabled authentication, the system will calculate the `txTime` when generating push URLs.**
>- As long as you start push or playback before the expiration time and the stream is not interrupted, the push or playback can continue even after the URL expires.



## Sample Code of Push URL

Sample code for generating a push URL in PHP and Java is provided for your reference, which can be viewed by performing the following steps:

1. Log in to the CSS console and click **[Domain Management](https://console.cloud.tencent.com/live/domainmanage).**
2. Click a push domain name or click **Manage** on the right to enter its details page.
3. Select **Push Configuration** and scroll down to find **Push Address Sample Code**.
4. Click the tab to view the sample code for PHP or Java, as shown below:
<dx-codeblock>
::: PHP php
```
/**
    * Get the push URL
    * If you do not pass in the authentication key and URL expiration time, a URL without hotlink protection will be returned.
    * @param domain   Your push domain name
    *        streamName   Unique stream name to identify its push URLs
    *        key   Authentication key
    *        time   Expiration time (accurate to the second). Example: 2016-11-12 12:00:00
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
:::
::: Java java
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
:::
</dx-codeblock>



## Subsequent Operations
After the push URL is generated, you can use it based on business scenarios. For specific operations, please see [Live Push](https://intl.cloud.tencent.com/document/product/267/31558).

