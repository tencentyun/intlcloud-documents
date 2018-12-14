## 1. Service Address

In this product, your API requests are routed to the nearest server via the domain name cvm.tencentcloudapi.com. You can also access APIs using the domain name for specified region, such as cvm.ap-guangzhou.tencentcloudapi.com for Guangzhou region.

It is recommended to use the domain name for accessing the nearest server. When you call an API, this domain name is automatically resolved to a server in a region **nearest** to the client where the API is initiated. For example, when you initiate an API request in Guangzhou, this domain name is automatically resolved to a Guangzhou server, with the result same as that of using "cvm.ap-guangzhou.tencentcloudapi.com".

The supported domain names are listed as below:

| Region | Domain Name |
|----------|------|
| Accessing the nearest server (recommended, and is only for non-Finance regions) | cvm.tencentcloudapi.com |
| South China (Guangzhou) | cvm.ap-guangzhou.tencentcloudapi.com |
| East China (Shanghai) | cvm.ap-shanghai.tencentcloudapi.com |
| North China (Beijing) | cvm.ap-beijing.tencentcloudapi.com |
| Southwest China (Chengdu) | cvm.ap-chengdu.tencentcloudapi.com |
| Southwest (Chongqing) | cvm.ap-chongqing.tencentcloudapi.com |
| Southeast Asia (Seoul) | cvm.ap-seoul.tencentcloudapi.com |
| Southeast Asia (Singapore) | cvm.ap-singapore.tencentcloudapi.com |
| Asia Pacific (Mumbai) | cvm.ap-mumbai.tencentcloudapi.com |
| Western U.S. (Silicon Valley) | cvm.na-siliconvalley.tencentcloudapi.com |
| Eastern U.S. (Virginia) | cvm.na-ashburn.tencentcloudapi.com |

**Note: [Finance regions](https://cloud.tencent.com/document/product/304/2766) and non-Finance regions are isolated from each other. Therefore, when you access the services in a finance region (the common parameter Region is finance region), you need to specify a domain name containing the region specified in the Region field.**

| Finance Region | Domain Name |
|----------|------|
| East China (Shanghai Finance) | cvm.ap-shanghai-fsi.tencentcloudapi.com |
| South China (Shenzhen Finance) | cvm.ap-shenzhen-fsi.tencentcloudapi.com |

## 2. Communication Protocol

All Tencent Cloud APIs communicate over HTTPS to provide high-security connections.

## 3. Request Methods

Both POST and GET requests are supported. For POST requests, Content-Type can only be application/x-www-form-urlencoded.

## 4. Character Encoding

UTF-8 encoding is always used.

