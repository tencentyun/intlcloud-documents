## Operation Scenarios

This document describes how to authenticate and manage your APIs through key pair authentication in JavaScript.

## Directions
1. In the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "key pair authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create a key pair on the key management page in the console.
4. Create a usage plan on the usage plan page in the console and bind it to the created key pair (for more information, please see [Sample Usage Plan](https://intl.cloud.tencent.com/document/product/628/11816)).
5. Bind the usage plan to the API or the service where the API resides.
6. Generate signing information in JavaScript by referring to the [Sample Code](#example).

## Notes
- The eventually delivered HTTP request contains at least two headers: `Date` or `X-Date` and `Authorization`. More optional headers can be added in the request. If `Date` is used, the server will not check the time; if `X-Date` is used, the server will check the time.
- The value of `Date` header is the construction time of the HTTP request in GMT format, such as Fri, 09 Oct 2015 00:00:00 GMT.
- The value of `X-Date` header is the construction time of the HTTP request in GMT format, such as Mon, 19 Mar 2018 12:08:40 GMT. It cannot deviate from the current time for more than 15 minutes.
- If it is a microservice API, you need to add two fields in the header: `X-NameSpace-Code` and `X-MicroService-Name`. They are not needed for general APIs and are included in the demo by default.

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

var dateTime = nowDate.toUTCString();
//dateTime = "Mon, 19 Mar 2018 12:00:44 GMT"
var SecretId = 'your SecretId'; // `SecretId` in key pair
var SecretKey = 'your SecretKey'; // `SecretKey` in key pair
var source = 'xxxxxx'; // Arbitrary signature watermark value
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
