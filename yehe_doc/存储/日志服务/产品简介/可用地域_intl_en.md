# Overview

You can create logsets and log topics in different regions when using CLS. Regions refer to the geographical areas of physical IDCs. Networks are completely isolated between regions. You can select the nearest region based on your business scenario and target users’ geographical location to reduce log access latency and improve access speed.



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

1. If another Tencent Cloud service is integrated into CLS, try to select a logset in the same region as the service. The services in the same region communicate with each other over a private network, which effectively reduces latency and improves access speed.
2. The classic network cannot access CLS over the private network.
