## 1. Service Address

The API supports access from either a nearby region (at cvm.tencentcloudapi.com) or a specified region (at cvm.ap-guangzhou.tencentcloudapi.com for Guangzhou, for example).

We recommend using the domain name to access the nearest server. When you call an API, the request is automatically resolved to a server in the region **nearest** to the location where the API is initiated. For example, when you initiate an API request in Guangzhou, this domain name is automatically resolved to a Guangzhou server, the result is the same as that of specifying the region in the domain like "cvm.ap-guangzhou.tencentcloudapi.com".

**Note: For latency-sensitive businesses, we recommend that you specify the region in the domain name. **

Tencent Cloud currently supports the following regions:

| Hosted region | Domain name |
|----------|------|
| Local access region (recommended, only for non-financial availability zones) | cvm.tencentcloudapi.com|
| South China (Guangzhou) | cvm.ap-guangzhou.tencentcloudapi.com |
| East China (Shanghai) | cvm.ap-shanghai.tencentcloudapi.com |
| North China (Beijing) | cvm.ap-beijing.tencentcloudapi.com |
| Southwest China (Chengdu) | cvm.ap-chengdu.tencentcloudapi.com |
| Southwest China (Chongqing) | cvm.ap-chongqing.tencentcloudapi.com |
| Hong Kong, Macao, Taiwan (Hong Kong, China) | cvm.ap-hongkong.tencentcloudapi.com |
| Southeast Asia (Singapore) | cvm.ap-singapore.tencentcloudapi.com|
| Southeast Asia (Bangkok) | cvm.ap-bangkok.tencentcloudapi.com |
| South Asia (Mumbai) | cvm.ap-mumbai.tencentcloudapi.com |
| Northeast Asia (Seoul) | cvm.ap-seoul.tencentcloudapi.com |
| Northeast Asia (Tokyo) | cvm.ap-tokyo.tencentcloudapi.com |
| U.S. East Coast (Virginia) | cvm.na-ashburn.tencentcloudapi.com |
| U.S. West Coast (Silicon Valley) | cvm.na-siliconvalley.tencentcloudapi.com |
| North America (Toronto) | cvm.na-toronto.tencentcloudapi.com |
| Europe (Frankfurt) | cvm.eu-frankfurt.tencentcloudapi.com |
| Europe (Moscow) | cvm.eu-moscow.tencentcloudapi.com |

**Note: As [financial availability zones](https://cloud.tencent.com/document/product/304/2766) and non-financial availability zones are isolated, when accessing the services in a financial availability zone (with the common parameter `Region` specifying a financial availability zone), it is necessary to specify a domain name of the financial availability zone, preferably in the same region as specified in `Region`.**

| Access region for financial availability zone | Domain name for financial availability zone |
|----------|------|
| East China (Shanghai Finance) | cvm.ap-shanghai-fsi.tencentcloudapi.com|
| South China (Shenzhen Finance) | cvm.ap-shenzhen-fsi.tencentcloudapi.com|

## 2. Communications Protocol

All the Tencent Cloud APIs communicate via HTTPS, providing highly secure communication tunnels.

## 3. Request Methods

Supported HTTP request methods:

* POST (recommended)
* GET

The Content-Type types supported by POST requests:

* application/json (recommended). The TC3-HMAC-SHA256 signature algorithm must be used.
* application/x-www-form-urlencoded. The HmacSHA1 or HmacSHA256 signature algorithm must be used.
* multipart/form-data (only supported by certain APIs). You must use TC3-HMAC-SHA256 to calculate the signature.

The size of a GET request packet is up to 32 KB. The size of a POST request is up to 1 MB when the HmacSHA1 or HmacSHA256 signature algorithm is used, and up to 10 MB when TC3-HMAC-SHA256 is used.

## 4. Character Encoding

Only UTF-8 encoding is used.
