## Overview

This document describes how to authenticate and manage your APIs through application-enabled authentication in PHP.

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "Application-Enabled Authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in PHP by referring to the [Sample Code](#示例代码).

## Environment Dependencies

This code sample is for PHP 7, and you may need to make changes for other PHP versions as appropriate.

## Notes

- For more information on operations such as application lifecycle management, API authorization for application, and application-API binding, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, please see [Application-Enabled Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

## Sample Code[](id:示例代码)

<dx-codeblock>
:::  PHP
<?php

/**

- Sort the given query string in alphabetical order

- @param string $queryStr

- @return string sorted query string
  */
  function sortQueryParameters($queryStr) {
  if (is_null($queryStr) || empty($queryStr)) {
      return "";
  }

  parse_str($queryStr, $arr);
  if (empty($arr)) {
      return "";
  }
  ksort($arr);

  $sortedQueryArr = array();
  foreach($arr as $k => $v) {
      $tmp = $k;
      if (!empty($v)) {
          $tmp .= ("=" . $v);
      }
      array_push($sortedQueryArr, $tmp);
  }

  return join('&', $sortedQueryArr);
  }

// ==========================================================
// Note: Update the customized variables based on your API
// ==========================================================
$apiAppKey = '<your_apiAppKey>';
$apiAppSecret = '<your_apiAppSecret>';
$httpMethod = "POST";
$acceptHeader = "application/json"; // accept header for your request
$url = 'https://service-xxxx-xxxx.gz.apigw.tencentcs.com/testmock?b=1&a=2';

// ContentType and contentMd5 should be empty if request body is not present
$reqBody = "{\"code\":1, \"msg\":\"ok\"}";
$contentType = "application/json";
$contentMD5 = base64_encode(md5($reqBody));

// ==========================================================
// customized parameter ends here
// ==========================================================

$parsedUrl = parse_url($url);
$xDateHeader = gmstrftime('%a, %d %b %Y %T %Z', time());

// Note:
// 1. parameters should be in alphabetical order
// 2. form parameter should also append to $pathAndParam
$pathAndParam = $parsedUrl['path'];
if ($parsedUrl['query']) {
    $pathAndParam = $pathAndParam . '?' . sortQueryParameters($parsedUrl['query']);
}

// Generate the string to sign
$strToSign = sprintf("x-date: %s\n%s\n%s\n%s\n%s\n%s",
    $xDateHeader, $httpMethod, $acceptHeader, $contentType, $contentMD5, $pathAndParam);
// echo "strToSign: $strToSign\n";

// Encode the string with HMAC and base64
$sign = base64_encode(hash_hmac('sha1', $strToSign, $apiAppSecret, TRUE));
$authHeader = sprintf('hmac id="%s", algorithm="hmac-sha1", headers="x-date", signature="%s"',
    $apiAppKey, $sign);

// Generate the request headers
$headers = array(
    'Host:' . $parsedUrl['host'],
    'Accept:' . $acceptHeader,
    'X-Date:' . $xDateHeader,
    'Content-Type:' . $contentType,  // only required if request body is present
    'Content-MD5:' . $contentMD5,    // only required if request body is present
    'Authorization:' . $authHeader,
);
// var_dump($headers);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_TIMEOUT, 60);
curl_setopt($ch, CURLOPT_POSTFIELDS, $reqBody); // only required if request body is present
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, $httpMethod);
$data = curl_exec($ch);

if (curl_errno($ch)) {
    print "Error: " . curl_error($ch);
} else {
    var_dump($data);
    curl_close($ch);
}
:::
</dx-codeblock>
