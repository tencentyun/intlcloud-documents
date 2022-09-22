## Service URL

TPNS currently provides four service access points in Guangzhou, Shanghai, Hong Kong (China), and Singapore (Southeast Asia). The data between different service access points is completely isolated. Based on the service access point you selected when creating a product, a service URL is obtained.
![](https://main.qcloudimg.com/raw/1292eb91a47983e2c51a4f61f6cb9fae.png)

The table below lists the service URLs currently available:

| Service Access Point     | Service URL                         |
| ------------------ | --------------------------------- |
| Service access point in Guangzhou, China     |  https://api.tpns.tencent.com/     |
| Service access point in Shanghai, China     | https://api.tpns.sh.tencent.com/     |
| Service access point in Hong Kong, China | https://api.tpns.hk.tencent.com/  |
| Service access point in Singapore   | https://api.tpns.sgp.tencent.com/ |


## Communication Protocol

All TencentCloud APIs communicate over HTTPS, which provides high security.

## Request Method

The supported HTTP request methods are as follows:
- POST

POST requests support the following content types:

1. application/json.
2. multipart/form-data (only supported by certain APIs).

## Character Encoding

Only `UTF-8` encoding is used.
