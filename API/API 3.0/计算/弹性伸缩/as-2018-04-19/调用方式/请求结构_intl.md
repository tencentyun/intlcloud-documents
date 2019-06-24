## 1. Service Address

The API supports access from either a nearby region (at cvm.tencentcloudapi.com) or a specified region (at cvm.ap-guangzhou.tencentcloudapi.com for Guangzhou, for example).

It is recommended to use the domain name for nearby access. Based on the location of the client when calling the API, the request will be automatically resolved to the server in the **nearest** region. For example, if a request is initiated in Guangzhou, it will be automatically resolved to the server in Guangzhou, and the effect is the same as that when specifying cvm.ap-guangzhou.tencentcloudapi.com.

**Note: For latency-sensitive businesses, it is recommended to specify a domain name with region.**

Below lists the currently supported regions:

| Access region | Domain name |
|----------|------|
| Local access region (recommended, only for non-financial availability zones) | cvm.tencentcloudapi.com|
| South China (Guangzhou) | cvm.ap-guangzhou.tencentcloudapi.com|
| East China (Shanghai) | cvm.ap-shanghai.tencentcloudapi.com|
| North China (Beijing) | cvm.ap-beijing.tencentcloudapi.com|
| Southwest China (Chengdu) | cvm.ap-chengdu.tencentcloudapi.com|
| Southwest China (Chongqing) | cvm.ap-chongqing.tencentcloudapi.com|
| Southeast Asia (China Hong Kong) | cvm.ap-hongkong.tencentcloudapi.com |
| Southeast Asia (Singapore) | cvm.ap-singapore.tencentcloudapi.com|
| Asia Pacific (Bangkok) | cvm.ap-bangkok.tencentcloudapi.com |
| Asia Pacific (Mumbai) | cvm.ap-mumbai.tencentcloudapi.com|
| Asia Pacific (Seoul) | cvm.ap-seoul.tencentcloudapi.com|
| Asia Pacific (Tokyo) | cvm.ap-tokyo.tencentcloudapi.com |
| Eastern America (Virginia) | cvm.na-ashburn.tencentcloudapi.com|
| Western America (Silicon Valley) | cvm.na-siliconvalley.tencentcloudapi.com|
| North America (Toronto) | cvm.na-toronto.tencentcloudapi.com |
| Europe (Frankfurt) | cvm.eu-frankfurt.tencentcloudapi.com |
| Europe (Moscow) | cvm.eu-moscow.tencentcloudapi.com |

**Note: As [financial availability zones](https://cloud.tencent.com/document/product/304/2766) and non-financial availability zones are isolated, when accessing the services in a financial availability zone (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the financial availability zone, preferably in the same region as specified in Region.**

| Access region for financial availability zone | Domain name for financial availability zone |
|----------|------|
| East China (Shanghai Financial) | cvm.ap-shanghai-fsi.tencentcloudapi.com|
| South China (Shenzhen Financial) | cvm.ap-shenzhen-fsi.tencentcloudapi.com|

## 2. Communications Protocol

All the TencentCloud APIs communicate via HTTPS, providing highly secure communications tunnels.

## 3. Request Method

Supported HTTP request methods:

* POST (recommended)
* GET

The Content-Type types supported by POST request:

* application/json (recommended). The TC3-HMAC-SHA256 signature method must be used.
* application/x-www-form-urlencoded. The HmacSHA1 or HmacSHA256 signature method must be used.
* multipart/form-data (only supported by certain APIs). The TC3-HMAC-SHA256 signature method must be used.

The GET request cannot exceed 32 KB in length. A POST request cannot exceed 1 MB in length when the HmacSHA1 or HmacSHA256 signature method is used.

## 4. Character Encoding

Only UTF-8 encoding is used.
