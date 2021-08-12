## Overview

This document describes how to authenticate and manage your APIs through application-enabled authentication in Java.

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "application-enabled authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in Java by referring to the [Sample Code](#示例代码).

## Environment Dependencies

API Gateway provides code samples for JSON request mode and form request mode. Please select an appropriate mode according to your business needs.

## Notes

- For more information on operations such as application lifecycle management, API authorization for application, and application-API binding, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, please see [Application-Enabled Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

## Sample Code[](id:示例代码)

### Sample code for JSON request method

```java
import javax.crypto.Mac;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.math.BigInteger;
import java.net.URI;
import java.net.URL;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.text.SimpleDateFormat;
import java.time.Duration;
import java.util.*;



public class AppAuthJavaDemo {
			private static final String MAC_NAME = "HmacSHA1";
			private static final String ENCODING = "UTF-8";



			private static final HttpClient httpClient = HttpClient.newBuilder()
							.version(HttpClient.Version.HTTP_2)
							.connectTimeout(Duration.ofSeconds(10))
							.build();



			private static String getGMTTime(){
					Calendar cd = Calendar.getInstance();
					SimpleDateFormat sdf = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss 'GMT'", Locale.US);
					sdf.setTimeZone(TimeZone.getTimeZone("GMT"));
					String GMTTime = sdf.format(cd.getTime());
					return GMTTime;
			}



			private static String sortQueryParams(String queryParam){
					// parameters should be in alphabetical order
					if (queryParam == null || queryParam == ""){
					return "";
					}



					String[] queryParams = queryParam.split("&");
					Map<String, String> queryPairs = new TreeMap<>();
					for(String query: queryParams){
							String[] kv = query.split("=");
							queryPairs.put(kv[0], kv[1]);
					}



					StringBuilder sortedParamsBuilder = new StringBuilder();
					Iterator iter = queryPairs.entrySet().iterator();
					while(iter.hasNext()){
					Map.Entry entry = (Map.Entry) iter.next();
							sortedParamsBuilder.append(entry.getKey());
							sortedParamsBuilder.append("=");
							sortedParamsBuilder.append(entry.getValue());
							sortedParamsBuilder.append("&");
					}
					String sortedParams = sortedParamsBuilder.toString();
					sortedParams = sortedParams.substring(0, sortedParams.length() - 1);



					return sortedParams;
			}



			private static byte[] HmacSHA1Encrypt(String encryptText, String encryptKey) throws Exception {
					byte[] data = encryptKey.getBytes(ENCODING);
					SecretKey secretKey = new SecretKeySpec(data, MAC_NAME);
					Mac mac = Mac.getInstance(MAC_NAME);
					mac.init(secretKey);



					byte[] text = encryptText.getBytes(ENCODING);
					return mac.doFinal(text);
			}



			private static String base64Encode(byte[] key) {
					final Base64.Encoder encoder = Base64.getEncoder();
					return encoder.encodeToString(key);
			}



			private static String getMD5(String str) throws NoSuchAlgorithmException {
					MessageDigest md = MessageDigest.getInstance("MD5");
					md.update(str.getBytes());
					return new BigInteger(1, md.digest()).toString(16);
			}



			public static void main(String[] args) throws Exception {
					String url = "http://service-xxxxx-xxxxx.bj.apigw.tencentcs.com/appauth?a=1&b=2";
					String host = "http://service-xxxxx-xxxxx.bj.apigw.tencentcs.com";
					String apiAppKey = "<Your AppKey>";
					String apiAppSecret = "<Your AppSecret>";
					String httpMethod = "POST";
					String acceptHeader = "application/json";



					// ContentType and contentMd5 should be empty if request body is not present
					String reqBody = "{\"name\":\"apple\", \"type\":\"fruit\"}";
					String contentType = "application/json";
					String contentMD5 = base64Encode(getMD5(reqBody).getBytes());



					// Parse URL and assemble string to sign
					URL parsedUrl = new URL(url);
					String pathAndParams = parsedUrl.getPath();
					if (parsedUrl.getQuery() != null) {
							pathAndParams = pathAndParams + "?" + sortQueryParams(parsedUrl.getQuery());
					}
					String xDate = getGMTTime();
					String stringToSign = String.format("x-date: %s\n%s\n%s\n%s\n%s\n%s", xDate, httpMethod, acceptHeader, contentType, contentMD5, pathAndParams);



					// Encode string with HMAC and base64
					byte[] hmacStr = HmacSHA1Encrypt(stringToSign, apiAppSecret);
					String signature = base64Encode(hmacStr);
					String authHeader = String.format("hmac id=\"%s\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\"%s\"", apiAppKey, signature);



					// Generate request
					HttpRequest request = HttpRequest.newBuilder()
									.POST(HttpRequest.BodyPublishers.ofString(reqBody))
									.uri(URI.create(url))
									.setHeader("Host", host)
									.setHeader("Accept", acceptHeader)
									.setHeader("x-date", xDate)
									.setHeader("Content-Type", contentType)
									.setHeader("Content-MD5", contentMD5)
									.setHeader("Authorization", authHeader)
									.build();



					// Send request
					HttpResponse<String> response = httpClient.send(request, HttpResponse.BodyHandlers.ofString());



					// Receive response
					System.out.println(response.statusCode());
					System.out.println(response.body());
			}


}
```

### Sample code for form request method

``` java
import javax.crypto.Mac;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.math.BigInteger;
import java.net.URI;
import java.net.URL;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.text.SimpleDateFormat;
import java.time.Duration;
import java.util.*;



public class AppAuthJavaFormDemo {
			private static final String MAC_NAME = "HmacSHA1";
			private static final String ENCODING = "UTF-8";



			private static final HttpClient httpClient = HttpClient.newBuilder()
					.version(HttpClient.Version.HTTP_2)
					.connectTimeout(Duration.ofSeconds(10))
					.build();



			private static String getGMTTime(){
					Calendar cd = Calendar.getInstance();
					SimpleDateFormat sdf = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss 'GMT'", Locale.US);
					sdf.setTimeZone(TimeZone.getTimeZone("GMT"));
					String GMTTime = sdf.format(cd.getTime());
					return GMTTime;
			}



			private static String sortQueryParams(String queryParam){
					// parameters should be in alphabetical order
					if (queryParam == null || queryParam == ""){
						return "";
			}



					String[] queryParams = queryParam.split("&");
					Map<String, String> queryPairs = new TreeMap<>();
					for(String query: queryParams){
						String[] kv = query.split("=");
						queryPairs.put(kv[0], kv[1]);
					}



					StringBuilder sortedParamsBuilder = new StringBuilder();
					Iterator iter = queryPairs.entrySet().iterator();
					while(iter.hasNext()){
						Map.Entry entry = (Map.Entry) iter.next();
						sortedParamsBuilder.append(entry.getKey());
						sortedParamsBuilder.append("=");
						sortedParamsBuilder.append(entry.getValue());
						sortedParamsBuilder.append("&");
					}
					String sortedParams = sortedParamsBuilder.toString();
					sortedParams = sortedParams.substring(0, sortedParams.length() - 1);



					return sortedParams;
			}



			private static byte[] HmacSHA1Encrypt(String encryptText, String encryptKey) throws Exception {
				byte[] data = encryptKey.getBytes(ENCODING);
				SecretKey secretKey = new SecretKeySpec(data, MAC_NAME);
				Mac mac = Mac.getInstance(MAC_NAME);
				mac.init(secretKey);



				byte[] text = encryptText.getBytes(ENCODING);
				return mac.doFinal(text);
			}



			private static String base64Encode(byte[] key) {
				final Base64.Encoder encoder = Base64.getEncoder();
				return encoder.encodeToString(key);
			}



			private static String getMD5(String str) throws NoSuchAlgorithmException {
				MessageDigest md = MessageDigest.getInstance("MD5");
				md.update(str.getBytes());
				return new BigInteger(1, md.digest()).toString(16);
			}



			public static void main(String[] args) throws Exception {
				String url = "http://service-xxxxxx-xxxxxx.bj.apigw.tencentcs.com/appauth?a=1&b=2";
				String host = "http://service-xxxxxx-xxxxxx.bj.apigw.tencentcs.com";
				String apiAppKey = "<Your App Key>";
				String apiAppSecret = "<Your App Secret>";
				String httpMethod = "POST";
				String acceptHeader = "application/json";



				// Parse form data and assemble request body
				Map<String, String> reqBodyMap = new TreeMap<>();
				reqBodyMap.put("type", "fruit");
				reqBodyMap.put("name", "apple");



				StringBuffer reqBodyBuffer = new StringBuffer();
				for (Map.Entry<String, String> e : reqBodyMap.entrySet()) {
					reqBodyBuffer.append(e.getKey());
					reqBodyBuffer.append("=");
					reqBodyBuffer.append(e.getValue());
					reqBodyBuffer.append("&");
				}
				String reqBody = reqBodyBuffer.toString();
				reqBody = reqBody.substring(0, reqBody.length() - 1);



				String contentType = "application/x-www-form-urlencoded";
				String contentMD5 = "";



				// Parse URL and assemble string to sign
				URL parsedUrl = new URL(url);
				String pathAndParams = parsedUrl.getPath();
				if (parsedUrl.getQuery() != null) {
					pathAndParams = pathAndParams + "?" + sortQueryParams(parsedUrl.getQuery());
				}
				if (reqBody != "" && reqBody.length() > 0){
					pathAndParams = pathAndParams + "&" + reqBody;
				}



				String xDate = getGMTTime();
				String stringToSign = String.format("x-date: %s\n%s\n%s\n%s\n%s\n%s", xDate, httpMethod, acceptHeader, contentType, contentMD5, pathAndParams);



				// Encode string with HMAC and base64
				byte[] hmacStr = HmacSHA1Encrypt(stringToSign, apiAppSecret);
				String signature = base64Encode(hmacStr);
				String authHeader = String.format("hmac id=\"%s\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\"%s\"", apiAppKey, signature);



				// Generate request
				HttpRequest request = HttpRequest.newBuilder()
						.POST(HttpRequest.BodyPublishers.ofString(reqBody))
						.uri(URI.create(url))
						.setHeader("Host", host)
						.setHeader("Accept", acceptHeader)
						.setHeader("x-date", xDate)
						.setHeader("Content-Type", contentType)
						.setHeader("Content-MD5", contentMD5)
						.setHeader("Authorization", authHeader)
						.build();



				// Send request
				HttpResponse<String> response = httpClient.send(request, HttpResponse.BodyHandlers.ofString());



				// Receive response
				System.out.println(response.statusCode());
				System.out.println(response.body());
			}
}
```
