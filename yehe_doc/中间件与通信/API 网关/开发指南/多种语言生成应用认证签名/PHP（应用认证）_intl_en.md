## Overview

This document describes how to manage access to your APIs through application authentication in PHP.

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as **App authentication**. To learn more about the authentication types, find the documentation for different types of backends in [Creating API - Overview](https://intl.cloud.tencent.com/document/product/628/11795).
2. Release the service where the API resides to an environment. See [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in PHP by referring to the [Sample Code](#sample code).

## Environmental Dependencies

- This code sample is for PHP 7, and you may need to make changes for other PHP versions as appropriate.
- API Gateway provides sample codes with the request body in JSON format and form-data format. Select as needed.

## Notes

- For more information on operations such as application lifecycle management, authorizing an app to access the API, and binding an app to an API, see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, see [Application Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

## Sample Code[](id:Sample-Code)
<dx-accordion>
::: Basic code
<dx-codeblock>
:::  php
<?php

const FORM_URLENCODED = "application/x-www-form-urlencoded";

/**
 * Generate a sorted query parameter string from parameter array.
 * such as array('b' => 1, 'a' => 2) to "a=1&b=2"
 *
 * @param array $paramArr
 * @return string sorted query string
 */
function getSortedParameterStr($paramArr)
{
    ksort($paramArr);
    $tmpArr = array();
    foreach ($paramArr as $k => $v) {
        $tmp = $k;
        if (!empty($v)) {
            $tmp .= ("=" . $v);
        }
        array_push($tmpArr, $tmp);
    }

    return join('&', $tmpArr);
}

/**
 * Send a HTTP request with App Authorization
 *
 * @param $apiAppKey string API App Key
 * @param $apiAppSecret string API App Secret
 * @param $method string HTTP Method of API
 * @param $url string Request URL of API, note that environment path (/release) is not allowed
 * @param $contentType string Request Content-Type header, set empty if request body is not needed
 * @param $acceptHeader string Accept HTTP request header
 * @param $reqBody string Request Body, set null if request body is not needed
 * @param $formParam array form parameters array, set null if not form request
 * @param $algorithm string Encryption algorithm: sha1, sha256, sha384, sha512, SM3, default to sha1
 * @param $customHeaders array Custom HTTP Headers, such as `array('x-header-a' => 1)`
 */
function sendRequestWithAppAuth($apiAppKey, $apiAppSecret, $method, $url, $contentType, $acceptHeader,
                                $reqBody=null, $formParam=null, $algorithm=null, $customHeaders=null)
{
    $contentMD5 = "";
    $isForm = ($contentType == FORM_URLENCODED);
    // Note: ContentMd5 is empty for application/x-www-form-urlencoded request
    if ($isForm) {
        assert(!is_null($formParam), "formParam is required for form request");
        // generate request body from form parameters
        $reqBody = getSortedParameterStr($formParam);
    } elseif (!is_null($reqBody)) {
        // get content md5 for signing the request later
        $contentMD5 = base64_encode(md5($reqBody));
    }

    if (null === $algorithm) {
        $algorithm = "sha1";
    }

    // ===================================
    // STEP 1: Generate the string to sign
    // ===================================

    echo "1. URL:\n $url\n";

    // Note:
    // 1. parameters needs to be sorted in alphabetical order
    // 2. parameters include both query parameters and form parameters
    $paramArr = array();
    $parsedUrl = parse_url($url);
    if (!is_null($parsedUrl['query']) && !empty($parsedUrl['query'])) {
        parse_str($parsedUrl['query'], $paramArr);
    }
    if (!empty($formParam)) {
        $paramArr = array_merge($paramArr, $formParam);
    }

    $pathAndParam = $parsedUrl['path'];
    if (!empty($paramArr)){
        $pathAndParam = $pathAndParam . '?' . getSortedParameterStr($paramArr);
    }

    $xDateHeader = gmstrftime('%a, %d %b %Y %T %Z', time());
    $strToSign = sprintf("x-date: %s\n%s\n%s\n%s\n%s\n%s",
        $xDateHeader, $method, $acceptHeader, $contentType, $contentMD5, $pathAndParam);

    // Print stringToSign for debugging if authorization failed with 401
    $strToSignDebug = str_replace("\n", "#", $strToSign);
    echo "2. StringToSign:\n $strToSignDebug\n";

    // ===============================================================================
    // STEP 2: Generate the signature (Authorization header) based on the stringToSign
    // ===============================================================================

    // Encode the string with HMAC and base64.
    $sign = base64_encode(hash_hmac($algorithm, $strToSign, $apiAppSecret, TRUE));
    $authHeader = sprintf(
        'hmac id="%s", algorithm="hmac-%s", headers="x-date", signature="%s"',
        $apiAppKey, $algorithm, $sign
    );

    $headers = array(
        'Host:' . $parsedUrl['host'],
        'Accept:' . $acceptHeader,
        'X-Date:' . $xDateHeader,
        'Authorization:' . $authHeader,
    );
    if (!empty($contentType)) {
        array_push($headers, "Content-Type:" . $contentType);
    }
    if (!empty($contentMD5)) {
        array_push($headers, "Content-MD5:" . $contentMD5);
    }
    if (!is_null($customHeaders) && is_array($customHeaders)) {
        foreach ($customHeaders as $k => $v) {
            array_push($headers, $k . ":" . $v);
        }
    }

    echo "3. Request Headers:\n";
    var_dump($headers);

    // ============================
    // STEP 3: Send the API request
    // ============================

    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_TIMEOUT, 60);
    if (!empty($reqBody)) {
        curl_setopt($ch, CURLOPT_POSTFIELDS, $reqBody); // only required if request body is present
    }
    curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
    curl_setopt($ch, CURLOPT_CUSTOMREQUEST, $method);
    $data = curl_exec($ch);
    if (curl_errno($ch)) {
        print "Error: " . curl_error($ch);
    } else {
        echo "Response: \n";
        var_dump($data);
        curl_close($ch);
    }
}
:::
</dx-codeblock>
:::
::: GET sample request
<dx-codeblock>
:::  php
// ==========================================================
// Example 1: Send a GET request without a request body
// ==========================================================
$apiAppKey = '<your_app_key>';
$apiAppSecret = '<your_app_secret>';

$httpMethod = "GET";
$acceptHeader = "application/json";

// Note: environment path, such as `/release`, is not supported with App Authorization
$url = 'https://service-xxxx-xxxx.gz.apigw.tencentcs.com/testmock?b=1&a=2';
sendRequestWithAppAuth($apiAppKey, $apiAppSecret, $httpMethod, $url, "", $acceptHeader);
:::
</dx-codeblock>
:::
::: POST JSON sample request
<dx-codeblock>
:::  php
// ==========================================================
// Example 2: Send a POST request with JSON request body
// ==========================================================
$apiAppKey = '<your_app_key>';
$apiAppSecret = '<your_app_secret>';

$httpMethod = "POST";
$acceptHeader = "application/json";
$contentType = "application/json";

// Note: environment path, such as `/release`, is not supported with App Authorization
$url = 'https://service-xxxx-xxxx.gz.apigw.tencentcs.com/testmock?b=1&a=2';
$jsonBody = "{\"data\":1}";
sendRequestWithAppAuth($apiAppKey, $apiAppSecret, $httpMethod, $url,
    $contentType, $acceptHeader, $jsonBody);
:::
</dx-codeblock>
:::
::: POST form-urlencoded sample request
<dx-codeblock>
:::  php
$apiAppKey = '<your_app_key>';
$apiAppSecret = '<your_app_secret>';

$httpMethod = "POST";
$acceptHeader = "application/json";
$contentType = "application/x-www-form-urlencoded";

// Note: environment path, such as `/release`, is not supported with App Authorization
$url = 'https://service-xxxx-xxxx.gz.apigw.tencentcs.com/testmock?b=1&a=2';
$customHeaders = array("x-custom-header" => 1);
$formParam = array('id' => 1, 'name' => 'tencent');
sendRequestWithAppAuth($apiAppKey, $apiAppSecret, $httpMethod, $url,
    $contentType, $acceptHeader, null, $formParam, null, $customHeaders);
:::
</dx-codeblock>
:::
</dx-accordion>


