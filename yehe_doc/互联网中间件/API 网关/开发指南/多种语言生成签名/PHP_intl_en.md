## Operation Scenarios

This document describes how to authenticate and manage your APIs through key pair authentication in PHP.

## Directions
1. In the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "key pair authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create a key pair on the key management page in the console.
4. Create a usage plan on the usage plan page in the console and bind it to the created key pair (for more information, please see [Sample Usage Plan](https://intl.cloud.tencent.com/document/product/628/11816)).
5. Bind the usage plan to the API or the service where the API resides.
6. Generate signing information in PHP by referring to the [Sample Code](#example).

## Notes
- The eventually delivered HTTP request contains at least two headers: `Date` or `X-Date` and `Authorization`. More optional headers can be added in the request. If `Date` is used, the server will not check the time; if `X-Date` is used, the server will check the time.
- The value of `Date` header is the construction time of the HTTP request in GMT format, such as Fri, 09 Oct 2015 00:00:00 GMT.
- The value of `X-Date` header is the construction time of the HTTP request in GMT format, such as Mon, 19 Mar 2018 12:08:40 GMT. It cannot deviate from the current time for more than 15 minutes.
- If it is a microservice API, you need to add two fields in the header: `X-NameSpace-Code` and `X-MicroService-Name`. They are not needed for general APIs and are included in the demo by default.

<span id="example"></span>
## Sample Code
```
<?php

$dateTime = gmdate("D, d M Y H:i:s T");
$SecretId = 'your SecretId'; # `SecretId` in key pair
$SecretKey = 'your SecretKey'; # `SecretKey` in key pair
$srcStr = "date: ".$dateTime."\n"."source: "."xxxxxx"; # Arbitrary signature watermark value
$Authen = 'hmac id="'.$SecretId.'", algorithm="hmac-sha1", headers="date source", signature="';
$signStr = base64_encode(hash_hmac('sha1', $srcStr, $SecretKey, true));
# echo $signStr;
$Authen = $Authen.$signStr."\"";
echo $Authen;
# echo '</br>';

$url = 'http://service-xxxxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com/release/yousa'; # API access path
$headers = array( 
	'Host:service-xxxxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com', # Service domain name of API
	'Accept:text/html, */*; q=0.01',
	'Source: xxxxxx',
	'Date: '.$dateTime,
	'Authorization: '.$Authen,
	'X-Requested-With: XMLHttpRequest',
	# 'Accept-Encoding: gzip, deflate, sdch',
	
	# If it is a microservice API, you need to add two fields in the header: 'X-NameSpace-Code' and 'X-MicroService-Name'. They are not needed for general APIs.
	'X-NameSpace-Code: testmic',
	'X-MicroService-Name: provider-demo'
);
$ch = curl_init(); 
curl_setopt($ch, CURLOPT_URL,$url); 
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
curl_setopt($ch, CURLOPT_TIMEOUT, 60); 
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers); 
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");

$data = curl_exec($ch); 

if (curl_errno($ch)) { 
	print "Error: " . curl_error($ch); 
} else { 
	# Show me the result 
	var_dump($data); 
	curl_close($ch); 
} 

?>
```
