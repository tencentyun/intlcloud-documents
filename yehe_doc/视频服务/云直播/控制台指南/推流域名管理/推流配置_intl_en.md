To protect your live streaming content, push authentication is enabled for push domains by default. You can use the address generator on the details page of a push domain to generate a push URL, which you can use to push streams (upload live videos) to the CSS platform.

## Notes

- CSS provides a test domain name `xxxx.tlivepush.com`. You can use it to test live push, but you’re not advised to use it as the push domain name for business purposes. 
- A push URL is valid before the expiration time you specify. After it expires, you need to generate a new URL.

## Prerequisites

You have activated the CSS service.

## Authentication Configuration
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the target **push domain name** or click **Manage** to enter the domain details page. 
2. Click **Push Configuration** and, in the **Authentication Configuration** area, click **Edit**.
	![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
3. In the pop-up window, toggle on **Push Authentication**.
4. Enter the primary key and backup key, and click **Save**.
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
>? The primary key is required and the backup key is optional. Entering both allows you to switch to the other key when one key is disclosed.

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



### Push URL format

An RTMP push URL looks like this:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
It includes the following fields:
- `domain`: Push domain name
- `AppName`: Live streaming application name, which is `live` by default and is customizable
- `StreamName`: Custom stream name used to identify a live stream
- `txSecret`: Authentication string generated after push authentication is enabled
- `txTime`: Expiration timestamp set for the push URL in the console

>!
>- If you have enabled authentication, the actual expiration time of a URL will be `txTime` plus the validity period of the key.
>- For the sake of convenience, the time you set in the console is the actual expiration time. **If you enable authentication, the system will calculate the `txTime` when generating push URLs.**
>- As long as you start push or playback before the expiration time and the stream is not interrupted, the push or playback can continue even after the URL expires.



## Sample Code of Push URL

We offer sample code in PHP and Java for generating push URLs. To view the code, follow the steps below:

1. Log in to the CSS console and click **[Domain Management](https://console.cloud.tencent.com/live/domainmanage).**
2. Click a push domain name or click **Manage** on the right to enter its details page.
3. Select **Push Configuration** and scroll down to find **Push Address Sample Code**.
4. Click the tab to view the sample code for PHP or Java.
<dx-codeblock>
::: PHP php
```
/**
    * Get the push URL
    * If you do not pass in the authentication key and URL expiration time, a URL without hotlink protection will be returned.
    * @param domain: Your push domain name
    *        streamName: A unique stream name to identify the push URL
    *        key: Authentication key
    *        time: Expiration time (accurate to the second). Example: 2016-11-12 12:00:00
    * @return String url

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
You can start pushing streams after the push URL is generated. For details, see [Live Push](https://intl.cloud.tencent.com/document/product/267/31558).

