# Overview

You can create logsets and log topics in different regions when using CLS. Regions are independent geographical areas where IDCs are located. Tencent Cloud regions are completely isolated. Select the nearest region according to your business needs and the location of your targeted users to reduce log access latency and improve user experience. 

#### Available regions and their abbreviations

| Region     | Abbreviation         | Private Domain Name                            | Public Domain Name                           |
| :------- | :--------------- | :---------------------------------- | :--------------------------------- |
| Beijing     | ap-beijing       | ap-beijing.cls.tencentyun.com       | ap-beijing.cls.tencentcs.com       |
| Guangzhou     | ap-guangzhou     | ap-guangzhou.cls.tencentyun.com     | ap-guangzhou.cls.tencentcs.com     |
| Shanghai     | ap-shanghai      | ap-shanghai.cls.tencentyun.com      | ap-shanghai.cls.tencentcs.com      |
| Chengdu     | ap-chengdu       | ap-chengdu.cls.tencentyun.com       | ap-chengdu.cls.tencentcs.com       |
| Nanjing     | ap-nanjing       | ap-nanjing.cls.tencentyun.com       | ap-nanjing.cls.tencentcs.com       |
| Chongqing     | ap-chongqing     | ap-chongqing.cls.tencentyun.com     | ap-chongqing.cls.tencentcs.com     |
| Hong Kong (China) | ap-hongkong      | ap-hongkong.cls.tencentyun.com      | ap-hongkong.cls.tencentcs.com      |
| Silicon Valley     | na-siliconvalley | na-siliconvalley.cls.tencentyun.com | na-siliconvalley.cls.tencentcs.com |
| Virginia | na-ashburn       | na-ashburn.cls.tencentyun.com       | na-ashburn.cls.tencentcs.com |
| Singapore   | ap-singapore     | ap-singapore.cls.tencentyun.com     | ap-singapore.cls.tencentcs.com     |
| Thailand  | ap-bangkok   | ap-bangkok.cls.tencentyun.com  | ap-bangkok.cls.tencentcs.com  |
| Mumbai     | ap-mumbai        | ap-mumbai.cls.tencentyun.com        | ap-mumbai.cls.tencentcs.com        |
| Frankfurt | eu-frankfurt     | eu-frankfurt.cls.tencentyun.com     | eu-frankfurt.cls.tencentcs.com   |
| Tokyo     | ap-tokyo         | ap-tokyo.cls.tencentyun.com         | ap-tokyo.cls.tencentcs.com         |
| Seoul     | ap-seoul         | ap-seoul.cls.tencentyun.com         | ap-seoul.cls.tencentcs.com         |
| Moscow  | eu-moscow   |  eu-moscow.cls.tencentyun.com  |  eu-moscow.cls.tencentcs.com  |


## Notes:

1. If another Tencent Cloud product is integrated with CLS, try to select a logset in the same region as the product. Tencent Cloud products in the same region can access each other over the private network, which effectively reduces latency and improves access speed.
2. The classic network cannot access CLS over private network.
3. CLS request domain names divide into private domain names and public domain names:
	- A private domain name is in the format of `${region}.cls.tencentyun.com`, which is only valid for access requests from the same region, that is, CVM or Tencent Cloud services access the CLS service in the same region through the private domain name.
	- A public domain name is in the format of `${region}.cls.tencentcs.com`. After the access source is connected to the internet, the public domain name of CLS can be accessed under normal circumstances.
