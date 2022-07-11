## Overview

This document describes how to manage access to your APIs through application authentication in Java.

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as **App authentication**. To learn more about the authentication types, find the documentation for different types of backends in [Creating API - Overview](https://intl.cloud.tencent.com/document/product/628/11795).
2. Release the service where the API resides to an environment. See [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in Java by referring to the [Sample Code](#sample code).

## Environmental Dependencies

- API Gateway provides sample codes with the request body in JSON format and form-data format. Select as needed.
- Application authentication in the Java demo needs to introduce the following external dependency:

```xml
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.5.13</version>
</dependency>
<dependency>
    <groupId>commons-codec</groupId>
    <artifactId>commons-codec</artifactId>
    <version>1.11</version>
</dependency>
```

## Notes

- For more information on operations such as application lifecycle management, authorizing an app to access the API, and binding an app to an API, see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, see [Application Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

## Sample Code[](id:Sample-Code)
<dx-accordion>
::: Sample code with the request body in JSON format
<dx-codeblock>
:::  java
import org.apache.commons.codec.digest.DigestUtils;
import org.apache.http.HttpEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import javax.crypto.Mac;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.net.URL;
import java.text.SimpleDateFormat;
import java.util.*;

public class AppAuthJavaDemo {
    private static final String MAC_NAME = "HmacSHA1";
    private static final String ENCODING = "UTF-8";
    private static final String HTTP_METHOD_GET = "GET";
    private static final String HTTP_METHOD_POST = "POST";

    private static String getGMTTime(){
        Calendar cd = Calendar.getInstance();
        SimpleDateFormat sdf = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss 'GMT'", Locale.US);
        sdf.setTimeZone(TimeZone.getTimeZone("GMT"));
        String GMTTime = sdf.format(cd.getTime());
        return GMTTime;
    }

    private static String sortQueryParams(String queryParam){
        // Parameters should be in alphabetical order
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

    private static String getMD5(String str) {
        String md5Hex = DigestUtils.md5Hex(str);
        return md5Hex;
    }

    public static void main(String[] args) throws Exception {
        String environment = "";
        String url = "http://service-xxxxxxx-xxxxxxxxxx.cq.apigw.tencentcs.com/appParam?name=clare&password=333";
        String host = "service-xxxxxxx-xxxxxxxxxx.cq.apigw.tencentcs.com";
        String apiAppKey = "APIDoMSRiefxxxxxxxxxxxxGz6AEEaFB";
        String apiAppSecret = "I0IDUmr6xxxxxxxxxxxxxx3C5GUsN2Rjvp";
        String httpMethod = "POST";
        String acceptHeader = "application/json";

        String contentType = "application/json";
        String reqBody = "{\"current\":1,\"size\":10,\"businessType\":\"4\"}";
        String contentMD5 = base64Encode(getMD5(reqBody).getBytes());

        if (httpMethod.toUpperCase() == HTTP_METHOD_GET) {
            reqBody = "";
        }
        // ContentType and contentMd5 should be empty if request body is not present
        if (reqBody.length() == 0) {
            contentType = "";
            contentMD5 = "";
            reqBody = "";
        }

        // Parse URL and assemble string to sign
        URL parsedUrl = new URL(url);
        String pathAndParams = parsedUrl.getPath();
        if (environment != ""){
            pathAndParams = pathAndParams.substring(pathAndParams.indexOf(environment) + environment.length());
        }

        if (parsedUrl.getQuery() != null) {
            pathAndParams = pathAndParams + "?" + sortQueryParams(parsedUrl.getQuery());
        }

        System.out.println("pathAndParams:"+ pathAndParams);

        String xDate = getGMTTime();
        String stringToSign = String.format("x-date: %s\n%s\n%s\n%s\n%s\n%s", xDate, httpMethod, acceptHeader, contentType, contentMD5, pathAndParams);
        // Encode string with HMAC and base64
        byte[] hmacStr = HmacSHA1Encrypt(stringToSign, apiAppSecret);
        String signature = base64Encode(hmacStr);
        String authHeader = String.format("hmac id=\"%s\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\"%s\"", apiAppKey, signature);

        System.out.println(stringToSign);
        // Generate request
        CloseableHttpClient httpClient = HttpClients.createDefault();
        CloseableHttpResponse response = null;
        // Send request
        if (httpMethod.toUpperCase() == HTTP_METHOD_GET){
            HttpGet httpGet = new HttpGet(url);
            httpGet.setHeader("Accept", acceptHeader);
            httpGet.setHeader("Host", host);
            httpGet.setHeader("x-date", xDate);
            httpGet.setHeader("Authorization", authHeader);
            response = httpClient.execute(httpGet);
        }

        if (httpMethod.toUpperCase() == HTTP_METHOD_POST) {
            HttpPost httpPost = new HttpPost(url);
            httpPost.setHeader("Accept", acceptHeader);
            httpPost.setHeader("Host", host);
            httpPost.setHeader("x-date", xDate);
            httpPost.setHeader("Content-Type", contentType);
            httpPost.setHeader("Content-MD5", contentMD5);
            httpPost.setHeader("Authorization", authHeader);
            StringEntity stringEntity = new StringEntity(reqBody, ENCODING);
            httpPost.setEntity(stringEntity);
            response = httpClient.execute(httpPost);
        }

        // Receive response
        HttpEntity responseEntity = response.getEntity();
        if (responseEntity != null) {
            System.out.println("Response status code: " + response.getStatusLine());
            System.out.println("Response body: " + EntityUtils.toString(responseEntity));
        }
    }
}
:::
</dx-codeblock>
:::
::: Sample code with the request body in form-data format
<dx-codeblock>
:::  java
import org.apache.commons.codec.digest.DigestUtils;
import org.apache.http.HttpEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import javax.crypto.Mac;
import javax.crypto.SecretKey;
import javax.crypto.spec.SecretKeySpec;
import java.net.URL;
import java.text.SimpleDateFormat;
import java.util.*;

public class AppAuthJavaFormDemo {
    private static final String MAC_NAME = "HmacSHA1";
    private static final String ENCODING = "UTF-8";
    private static final String HTTP_METHOD_GET = "GET";
    private static final String HTTP_METHOD_POST = "POST";

    private static String getGMTTime(){
        Calendar cd = Calendar.getInstance();
        SimpleDateFormat sdf = new SimpleDateFormat("EEE, dd MMM yyyy HH:mm:ss 'GMT'", Locale.US);
        sdf.setTimeZone(TimeZone.getTimeZone("GMT"));
        String GMTTime = sdf.format(cd.getTime());
        return GMTTime;
    }

    private static String sortQueryParams(String queryParam){
        // Parameters should be in alphabetical order
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


    public static void main(String[] args) throws Exception {
        String environment = "";
        String url = "http://service-xxxxxxx-xxxxxxxxxx.cq.apigw.tencentcs.com/appParam?name=clare&password=333";
        String host = "service-xxxxxxx-xxxxxxxxxx.cq.apigw.tencentcs.com";
        String apiAppKey = "APIDoMSRiefxxxxxxxxxxxxGz6AEEaFB";
        String apiAppSecret = "I0IDUmr6xxxxxxxxxxxxxx3C5GUsN2Rjvp";
        String httpMethod = "POST";
        String acceptHeader = "application/json";

        String reqBody = "";
        String contentType = "application/x-www-form-urlencoded";
        String contentMD5 = "";

        if (httpMethod.toUpperCase() == HTTP_METHOD_POST) {
            // Parse form data and assemble request body
            Map<String, String> reqBodyMap = new TreeMap<>();
            reqBodyMap.put("type", "fruit");
            reqBodyMap.put("fruitname", "apple");

            StringBuffer reqBodyBuffer = new StringBuffer();
            for (Map.Entry<String, String> e : reqBodyMap.entrySet()) {
                reqBodyBuffer.append(e.getKey());
                reqBodyBuffer.append("=");
                reqBodyBuffer.append(e.getValue());
                reqBodyBuffer.append("&");
            }
            reqBody = reqBodyBuffer.toString();
            reqBody = reqBody.substring(0, reqBody.length() - 1);
        }

        // ContentType should be empty if request body is not present
        if (reqBody.length() == 0) {
            contentType = "";
            reqBody = "";
        }      

        // Parse URL and assemble string to sign
        URL parsedUrl = new URL(url);
        String pathAndParams = parsedUrl.getPath();
        if (environment != ""){
            pathAndParams = pathAndParams.substring(pathAndParams.indexOf(environment) + environment.length());
        }

        String queryParams = "";
        if (parsedUrl.getQuery() != null) {
            queryParams = parsedUrl.getQuery();
        }
        if (reqBody != "" && reqBody.length() > 0){
            if(queryParams.length() > 0){
                queryParams = queryParams + "&" + reqBody;
            } else {
                queryParams = reqBody;
            }
        }
        if (queryParams != ""){
            pathAndParams = pathAndParams + "?" + sortQueryParams(queryParams);
        }

        String xDate = getGMTTime();
        String stringToSign = String.format("x-date: %s\n%s\n%s\n%s\n%s\n%s", xDate, httpMethod, acceptHeader, contentType, contentMD5, pathAndParams);
        System.out.println("stringToSign:" + stringToSign);

        // Encode string with HMAC and base64
        byte[] hmacStr = HmacSHA1Encrypt(stringToSign, apiAppSecret);
        String signature = base64Encode(hmacStr);
        String authHeader = String.format("hmac id=\"%s\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\"%s\"", apiAppKey, signature);

        // Generate request
        CloseableHttpClient httpClient = HttpClients.createDefault();
        CloseableHttpResponse response = null;

        // Send request
        if (httpMethod.toUpperCase() == HTTP_METHOD_GET) {
            HttpGet httpGet = new HttpGet(url);
            httpGet.setHeader("Accept", acceptHeader);
            httpGet.setHeader("Host", host);
            httpGet.setHeader("x-date", xDate);
            httpGet.setHeader("Authorization", authHeader);
            response = httpClient.execute(httpGet);
        }

        if (httpMethod.toUpperCase() == HTTP_METHOD_POST) {
            HttpPost httpPost = new HttpPost(url);
            httpPost.setHeader("Accept", acceptHeader);
            httpPost.setHeader("Host", host);
            httpPost.setHeader("x-date", xDate);
            httpPost.setHeader("Content-Type", contentType);
            httpPost.setHeader("Content-MD5", contentMD5);
            httpPost.setHeader("Authorization", authHeader);
            StringEntity stringEntity = new StringEntity(reqBody, ENCODING);
            httpPost.setEntity(stringEntity);
            response = httpClient.execute(httpPost);
        }

        // Receive response
        HttpEntity responseEntity = response.getEntity();

        if (responseEntity != null) {
            System.out.println("Response status code: " + response.getStatusLine());
            System.out.println("Response body: " + EntityUtils.toString(responseEntity));
        }
    }
}
:::
</dx-codeblock>
:::
</dx-accordion>

