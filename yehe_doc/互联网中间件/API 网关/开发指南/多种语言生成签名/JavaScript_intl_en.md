## Operation Scenarios

This document describes how to authenticate and manage your APIs through key pair authentication in JavaScript.

## Directions
1. In the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "key pair authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create a key pair on the key management page in the console.
4. Create a usage plan on the usage plan page in the console and bind it to the created key pair (for more information, please see [Sample Usage Plan](https://intl.cloud.tencent.com/document/product/628/11816)).
5. Bind the usage plan to the API or the service where the API resides.
6. Generate signing information in JavaScript by referring to the [Sample Code](#example).

<span id="example"></span>
## Sample Code
```
/*
used...
<script src="js/vue.js"></script>
<script src="js/axios.js"></script>
<script src="js/qs.js"></script>
<script src="js/crypto-js/crypto-js.js"></script>
*/
var nowDate = new Date(); 

var dateTime = nowDate.toGMTString();
//dateTime = "Mon, 19 Mar 2018 12:00:44 GMT"
var SecretId = 'your SecretId'; // `SecretId` in key pair
var SecretKey = 'your SecretKey'; // `SecretKey` in key pair
var source = 'xxxxxx'; // Arbitrary signature watermark value
source = 'source';
var auth = "hmac id=\"" + SecretId + "\", algorithm=\"hmac-sha1\", headers=\"x-date source\", signature=\"";
var signStr = "x-date: " + dateTime + "\n" + "source: " + source;
console.log(signStr)
var sign = CryptoJS.HmacSHA1(signStr, SecretKey)
console.log(sign.toString())
sign = CryptoJS.enc.Base64.stringify(sign)
sign = auth + sign + "\""
console.log(sign)
console.log(dateTime)

var instance = axios.create({
    baseURL: 'http://service-xxxxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com/release/api/shoplist', // API access path
    timeout: 5000,
    headers: {
                "Source":source,
                "X-Date":dateTime,
                "Authorization":sign
                
                // If it is a microservice API, you need to add two fields in the header: 'X-NameSpace-Code' and 'X-MicroService-Name'. They are not needed for general APIs.
				"X-NameSpace-Code": "testmic",
				"X-MicroService-Name": "provider-demo",
    },
    withCredentials: true
});

instance.get()
.then(function (response) {
        console.log(response);
    })
    .catch(function (error) {
        console.log(error);
    });;
```
