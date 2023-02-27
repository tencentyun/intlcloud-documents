To protect your live streaming content, push authentication is enabled for push domains by default. You can use the address generator on the details page of a push domain to generate a push URL, which you can use to push streams (upload live videos) to the CSS platform.

## Must-Knows

- CSS provides a test domain name `xxxx.tlivepush.com`. You can use it to push streams for test purposes, but the test domain should not be used in production environments. 
- A push URL is valid before the expiration time you specify. After it expires, you need to generate a new URL.

## Prerequisites

You have activated CSS.

## Authentication Configuration
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), click the target **push domain name** or click **Manage** to enter the domain details page. 
2. Click **Push Configuration** and, in the **Authentication Configuration** area, click **Edit**.
![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
3. In the pop-up window, toggle on **Push Authentication**.
4. Enter the primary key and backup key, and click **Save**.
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
>? The primary key is required and the backup key is optional. Entering both allows you to switch to the other key when one key is disclosed.

## Push Address Generator

### Directions
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), click the target domain name or click **Manage** on its right to enter the details page.
2. Select **Push Configuration** and, in **Push Address Generator**, complete the following settings:
   1. Select an expiration time, such as `2022-11-24 16:00:35`.
   2. Enter a custom stream name (`StreamName`).
   3. Click **Generate Push Address** to generate a push URL containing the `StreamName`.
![](https://main.qcloudimg.com/raw/6f5ac8dcac2082aedca950c5341946ab.png)
3. If you haven’t enabled authentication for your push domain, then you will also find RTMP, WebRTC, SRT, and RTMP over SRT URLs in the **Push URL** area. Replace `StreamName` in your playback URL with the stream name used for push, and you can use the URL to play the stream. 
![](https://main.qcloudimg.com/raw/aa129bd839cb307993bfed247e636a41.png)


### Push URL format

An RTMP push URL looks like this:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```

Parameter description
- `domain`: The push domain name.
- `AppName`: The live streaming application name, which is `live` by default and is customizable.
- `StreamName`: The custom stream name used to identify a live stream.
- `txSecret`: The authentication string generated after push authentication is enabled.
- `txTime`: The expiration timestamp for the push URL.

>!
>- If you have enabled authentication, `txTime` indicates the expiration time of the URL.
>- For the sake of convenience, the console allows you to specify the URL expiration time in human-readable format. **If you enable authentication, when generating push URLs, the system will convert it to a hex timestamp (the value of `txTime`)**.
>- As long as you start push or playback before the expiration time and the stream is not interrupted, the push or playback can continue even after the URL expires.

## Sample Code of Push URL
We offer sample code in PHP, Java, and Go for generating push URLs. To view the code, follow the steps below:

1. Log in to the CSS console and click [Domain Management](https://console.cloud.tencent.com/live/domainmanage).
2. Click a push domain name or click **Manage** on the right to enter its details page.
3. Select **Push Configuration** and scroll down to find **Push Address Sample Code**.
4. Click the tab to view the sample code for PHP, Java, or Go.
<dx-codeblock>
::: PHP php
/**
* Get the push URL
* If you do not pass in the authentication key and URL expiration time, a URL without hotlink protection will be returned.
* @param domain: Your push domain name.
*        streamName: A unique stream name to identify the push URL.
*        key: The authentication key.
*        time:   The URL expiration time (example: 2016-11-12 12:00:00).
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
:::
::: Java java
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
:::
::: GO go
package a

import (
	"crypto/md5"
	"fmt"
	"strconv"
	"strings"
	"time"
)

func GetPushUrl(domain, streamName, key string, time int64)(addrstr string){
	var ext_str string
	if key != "" && time != 0{
		txTime := strings.ToUpper(strconv.FormatInt(time, 16))
		txSecret := md5.Sum([]byte(key + streamName + txTime))
		txSecretStr := fmt.Sprintf("%x", txSecret)
		ext_str = "?txSecret=" + txSecretStr + "&txTime=" + txTime
	}
	addrstr = "rtmp://" + domain + "/live/" + streamName + ext_str
	return
}
/*
*domain: 123.test.com
*streamName: streamname
*key: 69e0daf7234b01f257a7adb9f807ae9f
*time: 2022-04-26 14:57:19 CST
*/
func main(){
	domain, streamName, key := "123.test.com", "streamname", "69e0daf7234b01f257a7adb9f807ae9f"
	//CST: ChinaStandardTimeUT, "2006-01-02 15:04:05 MST" must be const
	t, err := time.Parse("2006-01-02 15:04:05 MST", "2022-04-26 14:57:19 CST")
	if err != nil{
		fmt.Println("time transfor error!")
		return
	}
	fmt.Println(GetPushUrl(domain, streamName, key, t.Unix()))
	return
}
:::
</dx-codeblock>

## Related Operations
You can start pushing streams after the push URL is generated. For details, see [Live Push](https://intl.cloud.tencent.com/document/product/267/31558).
