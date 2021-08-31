## Operation Scenarios

This document describes how to authenticate and manage your APIs through key pair authentication in Java.

## Directions
1. In the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "key pair authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create a key pair on the key management page in the console.
4. Create a usage plan on the usage plan page in the console and bind it to the created key pair (for more information, please see [Sample Usage Plan](https://intl.cloud.tencent.com/document/product/628/11816)).
5. Bind the usage plan to the API or the service where the API resides.
6. Generate signing information in Java by referring to the [Sample Code](#example).

## Notes
- The eventually delivered HTTP request contains at least two headers: `Date` or `X-Date` and `Authorization`. More optional headers can be added in the request. If `Date` is used, the server will not check the time; if `X-Date` is used, the server will check the time.
- The value of `Date` header is the construction time of the HTTP request in GMT format, such as Fri, 09 Oct 2015 00:00:00 GMT.
- The value of `X-Date` header is the construction time of the HTTP request in GMT format, such as Mon, 19 Mar 2018 12:08:40 GMT. It cannot deviate from the current time for more than 15 minutes.
- If it is a microservice API, you need to add two fields in the header: `X-NameSpace-Code` and `X-MicroService-Name`. They are not needed for general APIs and are included in the demo by default.
- This Demo contains samples of the `GET` and `POST` methods for your choice.

<span id="example"></span>
## Sample Code
#### Base64.java

```Java
package apigatewayDemo;

import java.io.UnsupportedEncodingException;

public class Base64 {
    private static char[] base64EncodeChars = new char[] { 'A', 'B', 'C', 'D',
            'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q',
            'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', 'a', 'b', 'c', 'd',
            'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q',
            'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', '0', '1', '2', '3',
            '4', '5', '6', '7', '8', '9', '+', '/' };

    private static byte[] base64DecodeChars = new byte[] { -1, -1, -1, -1, -1,
            -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
            -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1, -1,
            -1, -1, -1, -1, 62, -1, -1, -1, 63, 52, 53, 54, 55, 56, 57, 58, 59,
            60, 61, -1, -1, -1, -1, -1, -1, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9,
            10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, -1,
            -1, -1, -1, -1, -1, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37,
            38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, -1, -1, -1,
            -1, -1 };

    public static String encode(byte[] data) {
        StringBuffer sb = new StringBuffer();
        int len = data.length;
        int i = 0;
                                int b1, b2, b3;
        while (i < len) {
            b1 = data[i++] & 0xff;
            if (i == len) {
                sb.append(base64EncodeChars[b1 >>> 2]);
                sb.append(base64EncodeChars[(b1 & 0x3) << 4]);
                sb.append("==");
                break;
            }
            b2 = data[i++] & 0xff;
            if (i == len) {
                sb.append(base64EncodeChars[b1 >>> 2]);
                sb.append(base64EncodeChars[((b1 & 0x03) << 4)
                        | ((b2 & 0xf0) >>> 4)]);
                sb.append(base64EncodeChars[(b2 & 0x0f) << 2]);
                sb.append("=");
                break;
            }
            b3 = data[i++] & 0xff;
            sb.append(base64EncodeChars[b1 >>> 2]);
            sb.append(base64EncodeChars[((b1 & 0x03) << 4)
                    | ((b2 & 0xf0) >>> 4)]);
            sb.append(base64EncodeChars[((b2 & 0x0f) << 2)
                    | ((b3 & 0xc0) >>> 6)]);
                        sb.append(base64EncodeChars[b3 & 0x3f]);
        }
        return sb.toString();
    }

    public static byte[] decode(String str) throws UnsupportedEncodingException {
        StringBuffer sb = new StringBuffer();
        byte[] data = str.getBytes("US-ASCII");
        int len = data.length;
        int i = 0;
        int b1, b2, b3, b4;
        while (i < len) {
            /* b1 */
            do {
                b1 = base64DecodeChars[data[i++]];
            } while (i < len && b1 == -1);
            if (b1 == -1)
                break;
            /* b2 */
            do {
                b2 = base64DecodeChars[data[i++]];
            } while (i < len && b2 == -1);
            if (b2 == -1)
                break;
            sb.append((char) ((b1 << 2) | ((b2 & 0x30) >>> 4)));
            /* b3 */
            do {
                b3 = data[i++];
                if (b3 == 61)
                    return sb.toString().getBytes("ISO-8859-1");
                b3 = base64DecodeChars[b3];
            } while (i < len && b3 == -1);
            if (b3 == -1)
                break;
            sb.append((char) (((b2 & 0x0f) << 4) | ((b3 & 0x3c) >>> 2)));
            /* b4 */
            do {
                b4 = data[i++];
                if (b4 == 61)
                    return sb.toString().getBytes("ISO-8859-1");
                b4 = base64DecodeChars[b4];
            } while (i < len && b4 == -1);
            if (b4 == -1)
                break;
            sb.append((char) (((b3 & 0x03) << 6) | b4));
        }
        return sb.toString().getBytes("ISO-8859-1");
    }
}
```

#### SignAndSend.java

```Java
package apigatewayDemo;
import java.io.UnsupportedEncodingException;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.text.SimpleDateFormat;
import java.util.*;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.URL;
import java.net.URLConnection;
import java.net.HttpURLConnection;
import java.io.OutputStreamWriter;

public class SignAndSend {
    private static final String CONTENT_CHARSET = "UTF-8";
    private static final String HMAC_ALGORITHM = "HmacSHA1";
    public static String sign(String secret, String timeStr)
            throws NoSuchAlgorithmException, UnsupportedEncodingException, InvalidKeyException
    {
        // Get the signature string
        String signStr = "date: "+timeStr+"\n"+"source: "+"source";
        // Get the API signature
        String sig = null;
        Mac mac1 = Mac.getInstance(HMAC_ALGORITHM);
        byte[] hash;
        SecretKeySpec secretKey = new SecretKeySpec(secret.getBytes(CONTENT_CHARSET), mac1.getAlgorithm());
        mac1.init(secretKey);
        hash = mac1.doFinal(signStr.getBytes(CONTENT_CHARSET));
        sig = new String(Base64.encode(hash));
        System.out.println("signValue--->" + sig);
        return sig;
    }

    public static HttpURLConnection NewHttpUrlCon(String url, String secretId, String secretKey) {
        // Get the current GMT time
        Calendar cd = Calendar.getInstance();
        SimpleDateFormat sdf = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss 'GMT'", Locale.US);
        sdf.setTimeZone(TimeZone.getTimeZone("GMT"));
        String timeStr = sdf.format(cd.getTime());
        HttpURLConnection httpUrlCon = null;
        try {
            String urlNameString = url;
            URL realUrl = new URL(urlNameString);
            // Open the connection to the URL
            URLConnection connection = realUrl.openConnection();
            httpUrlCon = (HttpURLConnection)connection;
            // Set general request attributes
            httpUrlCon.setRequestProperty("Host", url);
            httpUrlCon.setRequestProperty("Accept", "text/html, */*; q=0.01");
            httpUrlCon.setRequestProperty("Source","source");
            httpUrlCon.setRequestProperty("Date",timeStr);
            String sig = sign(secretKey,timeStr);
            String authen = "hmac id=\""+secretId+"\", algorithm=\"hmac-sha1\", headers=\"date source\", signature=\""+sig+"\"";
            System.out.println("authen --->" + authen);
            httpUrlCon.setRequestProperty("Authorization",authen);
            httpUrlCon.setRequestProperty("X-Requested-With","XMLHttpRequest");
            httpUrlCon.setRequestProperty("Accept-Encoding","gzip, deflate, sdch");

            // If it is a microservice API, you need to add two fields in the header: 'X-NameSpace-Code' and 'X-MicroService-Name'. They are not needed for general APIs.
            httpUrlCon.setRequestProperty("X-NameSpace-Code","testmic");
            httpUrlCon.setRequestProperty("X-MicroService-Name","provider-demo");
        } catch (Exception e) {
            System.out.println("An exception occurred while creating the connection." + e);
            e.printStackTrace();
        }
        return httpUrlCon;
    }

    public static String sendGet(String url, String secretId, String secretKey) {
        String result = "";
        BufferedReader in = null;
        try {
            // Create a connection
            HttpURLConnection httpUrlCon = NewHttpUrlCon(url, secretId, secretKey);

            // Establish the actual connection
            httpUrlCon.connect();

            // Get all response header fields
            Map<String, List<String>> map = httpUrlCon.getHeaderFields();

            // Traverse all response header fields
            for (String key : map.keySet()) {
                System.out.println(key + "--->" + map.get(key));
            }

            // Define the `BufferedReader` input stream to read the URL response
            in = new BufferedReader(new InputStreamReader(
                    httpUrlCon.getInputStream()));
            String line;
            while ((line = in.readLine()) != null) {
                result += line;
            }
        } catch (Exception e) {
            System.out.println("An exception occurred while sending the GET request." + e);
            e.printStackTrace();
        }

        // Close the input stream by using the `finally` block
        finally {
            try {
                if (in != null) {
                    in.close();
                }
            } catch (Exception e2) {
                e2.printStackTrace();
            }
        }
        return result;
    }

    public static String sendPost(String url, String secretId, String secretKey) {
        String result = "";
        BufferedReader in = null;
        try {

            // Create a connection
            HttpURLConnection httpUrlCon = NewHttpUrlCon(url, secretId, secretKey);

            // Configure the `POST` request
            httpUrlCon.setRequestMethod("POST");
            httpUrlCon.setUseCaches(false);  // A `POST` cannot use the cache
            httpUrlCon.setDoOutput(true);
            httpUrlCon.setDoInput(true);

            // Put the request data in the body
            OutputStreamWriter out = new OutputStreamWriter(httpUrlCon.getOutputStream());
            String jsonStr = "{\"caller\":\"apigw\", \"data\":\"test post\"}";
            out.write(jsonStr);
            out.flush();
            out.close();

            // Establish the actual connection
            httpUrlCon.connect();

            // Get all response header fields
            Map<String, List<String>> map = httpUrlCon.getHeaderFields();

            // Traverse all response header fields
            for (String key : map.keySet()) {
                System.out.println(key + "--->" + map.get(key));
            }

            // Define the `BufferedReader` input stream to read the URL response
            in = new BufferedReader(new InputStreamReader(
                    httpUrlCon.getInputStream()));
            String line;
            while ((line = in.readLine()) != null) {
                result += line;
            }
        } catch (Exception e) {
            System.out.println("An exception occurred while sending the POST request." + e);
            e.printStackTrace();
        }

        // Close the input stream by using the `finally` block
        finally {
            try {
                if (in != null) {
                    in.close();
                }
            } catch (Exception e2) {
                e2.printStackTrace();
            }
        }
        return result;
    }
}
```

#### Demo.java

```Java
package apigatewayDemo;
public class Demo {
    public static void main(String[] args) {
        String secretId = "your secretId"; // `SecretId` in key pair
        String secretKey = "your secretKey"; // `SecretKey` in key pair
        SignAndSend signAndSendInstance = new SignAndSend();

        // `GET` request
        String getUrl = "http://service-xxxxxxxx-1234567890.gz.apigw.tencentcs.com:80/get"; // API access path
        String getResult = SignAndSend.sendGet(getUrl, secretId, secretKey);
        System.out.println(getResult);

        // `POST` request
        String postUrl = "http://service-xxxxxxxx-1234567890.gz.apigw.tencentcs.com:80/post"; // API access path
        String postResult = SignAndSend.sendPost(postUrl, secretId, secretKey);
        System.out.println(postResult);
    }
}
```
