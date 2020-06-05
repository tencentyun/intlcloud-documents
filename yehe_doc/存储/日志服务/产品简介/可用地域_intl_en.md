## Overview

You can create logsets and log topics in different regions when using CLS. Regions are independent geographical areas where IDCs are located. Tencent Cloud regions are completely isolated. Select the nearest region according to your business needs and the location of your targeted users to reduce log access latency and improve user experience. 



#### Notes about Shenzhen and Shanghai Finance Zones

A finance zone is a tailor-made AZ for compliance with regulatory requirements in the finance industry and features high security and high isolation. Currently, CLS supports the Shenzhen and Shanghai Finance Zones. Verified finance customers can submit a ticket to use these AZs.



#### Available regions and their abbreviations

| Region     | Abbreviation         | Private Domain Name                            | Public Domain Name                           |
| -------- | ---------------- | ----------------------------------- | ---------------------------------- |
| Beijing     | ap-beijing       | ap-beijing.cls.tencentyun.com       | ap-beijing.cls.tencentcs.com       |
| Guangzhou     | ap-guangzhou     | ap-guangzhou.cls.tencentyun.com     | ap-guangzhou.cls.tencentcs.com     |
| Shanghai     | ap-shanghai      | ap-shanghai.cls.tencentyun.com      | ap-shanghai.cls.tencentcs.com      |
| Chengdu     | ap-chengdu       | ap-chengdu.cls.tencentyun.com       | ap-chengdu.cls.tencentcs.com       |
| Nanjing     | ap-nanjing       | ap-nanjing.cls.tencentyun.com       | ap-nanjing.cls.tencentcs.com       |
| Chongqing     | ap-chongqing     | ap-chongqing.cls.tencentyun.com     | ap-chongqing.cls.tencentcs.com     |
| Shenzhen Finance | ap-shenzhen-fsi  | ap-shenzhen-fsi.cls.tencentyun.com  | ap-shenzhen-fsi.cls.tencentcs.com  |
| Shanghai Finance | ap-shanghai-fsi  | ap-shanghai-fsi.cls.tencentyun.com  | ap-shanghai-fsi.cls.tencentcs.com  |
| Hong Kong (China) | ap-hongkong      | ap-hongkong.cls.tencentyun.com      | ap-hongkong.cls.tencentcs.com      |
| Silicon Valley     | na-siliconvalley | na-siliconvalley.cls.tencentyun.com | na-siliconvalley.cls.tencentcs.com |
| Singapore   | ap-singapore     | ap-singapore.cls.tencentyun.com     | ap-singapore.cls.tencentcs.com     |
| Mumbai     | ap-mumbai        | ap-mumbai.cls.tencentyun.com        | ap-mumbai.cls.tencentcs.com        |



## Notes

If another Tencent Cloud product is integrated with CLS, try to select a logset in the same region as the product. Tencent Cloud products in the same region can access each other over the private network, which effectively reduces latency and improves access speed.
2. The classic network cannot access CLS over private network.
