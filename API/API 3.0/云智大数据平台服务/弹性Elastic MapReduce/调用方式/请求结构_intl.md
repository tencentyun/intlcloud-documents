## 1. Service Address

The API supports access from either a nearby region (at cvm.tencentcloudapi.com) or a specified region (at cvm.ap-guangzhou.tencentcloudapi.com for Guangzhou, for example).

It is recommended to use the domain name for accessing the nearest server. When you call an API, this domain name is automatically resolved to a server in the region **nearest** to the client where the API is initiated. For example, when you initiate an API request in Guangzhou, this domain name is automatically resolved to a Guangzhou server, with the result same as that of using "cvm.ap-guangzhou.tencentcloudapi.com".

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
| Southeast Asia (Hong Kong, China) | cvm.ap-hongkong.tencentcloudapi.com |
| Southeast Asia (Singapore) | cvm.ap-singapore.tencentcloudapi.com|
| Asia Pacific (Bangkok) | cvm.ap-bangkok.tencentcloudapi.com |
| Asia Pacific (Mumbai) | cvm.ap-mumbai.tencentcloudapi.com|
| Asia Pacific (Seoul) | cvm.ap-seoul.tencentcloudapi.com|
| Asia Pacific (Tokyo) | cvm.ap-tokyo.tencentcloudapi.com |
| Eastern US (Virginia) | cvm.na-ashburn.tencentcloudapi.com|
| Western US (Silicon Valley) | cvm.na-siliconvalley.tencentcloudapi.com|
| North America (Toronto) | cvm.na-toronto.tencentcloudapi.com |
| Europe (Frankfurt) | cvm.eu-frankfurt.tencentcloudapi.com |
| Europe (Moscow) | cvm.eu-moscow.tencentcloudapi.com |

**Note: As [financial availability zones](https://cloud.tencent.com/document/product/304/2766) and non-financial availability zones are isolated, when accessing the services in a financial availability zone (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the financial availability zone, preferably in the same region as specified in Region.**

| Access region for financial availability zone | Domain name for financial availability zone |
|----------|------|
| East China (Shanghai Finance) | cvm.ap-shanghai-fsi.tencentcloudapi.com|
| South China (Shenzhen Finance) | cvm.ap-shenzhen-fsi.tencentcloudapi.com|

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

The size of a GET request packet is up to 32 KB. The size of a POST request is up to 1 MB when the HmacSHA1 or HmacSHA256 signature method is used, and up to 10 MB when TC3-HMAC-SHA256 is used.

## 4. Character Encoding

Only UTF-8 encoding is used.
