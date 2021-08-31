## 1. Service Address

The API supports access from either a nearby region (at cvm.tencentcloudapi.com) or a specified region (at cvm.ap-guangzhou.tencentcloudapi.com for Guangzhou, for example).

You are recommended to use the domain name for accessing the nearest server. When you call an API, the domain name will be automatically resolved to a server in a region **nearest** to the client where the API is initiated. For example, when you initiate an API request in Guangzhou, the domain name will be automatically resolved to a Guangzhou server, with the result same as that of using "cvm.ap-guangzhou.tencentcloudapi.com".

**Note: for latency-sensitive businesses, you are recommended to specify a domain name with region.**

Currently supported regions are as listed below:

| Access Region | Domain Name |
|----------|------|
| Nearby access region (recommended, only for non-finance AZs) | cvm.tencentcloudapi.com|
| South China (Guangzhou) | cvm.ap-guangzhou.tencentcloudapi.com|
| East China (Shanghai) | cvm.ap-shanghai.tencentcloudapi.com|
| North China (Beijing) | cvm.ap-beijing.tencentcloudapi.com|
| Southwest China (Chengdu) | cvm.ap-chengdu.tencentcloudapi.com|
| Southwest China (Chongqing) | cvm.ap-chongqing.tencentcloudapi.com|
| Hong Kong, China/Macao, China/Taiwan, China (Hong Kong, China) | cvm.ap-hongkong.tencentcloudapi.com |
| Southeast Asia Pacific (Singapore) | cvm.ap-singapore.tencentcloudapi.com|
| Southeast Asia Pacific (Bangkok) | cvm.ap-bangkok.tencentcloudapi.com |
| South Asia Pacific (Mumbai) | cvm.ap-mumbai.tencentcloudapi.com|
| Northeast Asia Pacific (Seoul) | cvm.ap-seoul.tencentcloudapi.com|
| Northeast Asia Pacific (Tokyo) | cvm.ap-tokyo.tencentcloudapi.com |
| East US (Virginia) | cvm.na-ashburn.tencentcloudapi.com|
| West US (Silicon Valley) | cvm.na-siliconvalley.tencentcloudapi.com|
| North America (Toronto) | cvm.na-toronto.tencentcloudapi.com |
| Europe (Frankfurt) | cvm.eu-frankfurt.tencentcloudapi.com |
| Europe (Moscow) | cvm.eu-moscow.tencentcloudapi.com |

**Note: as finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (as specified in the common parameter `Region`), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in `Region`.**

| Access region for finance AZ | Domain name for finance AZ |
|----------|------|
| East China (Shanghai Finance) | cvm.ap-shanghai-fsi.tencentcloudapi.com|
| South China (Shenzhen Finance) | cvm.ap-shenzhen-fsi.tencentcloudapi.com|

## 2. Communications Protocol

All the TencentCloud APIs communicate over HTTPS, providing highly secure communications tunnels.

## 3. Request Method

Supported HTTP request methods:

* POST (recommended)
* GET

`Content-Type` types supported by POST request:

* application/json (recommended). The signature algorithm v3 (TC3-HMAC-SHA256) must be used.
* application/x-www-form-urlencoded. The signature algorithm v1 (HmacSHA1 or HmacSHA256) must be used.
* multipart/form-data (only supported by certain APIs). The signature algorithm v3 (TC3-HMAC-SHA256) must be used.

The size of a GET request packet cannot exceed 32 KB. The size of a POST request cannot exceed 1 MB for the signature algorithm v1 (HmacSHA1 or HmacSHA256) or 10 MB for the signature algorithm v3 (TC3-HMAC-SHA256).

## 4. Character Encoding

UTF-8 encoding is always used.
