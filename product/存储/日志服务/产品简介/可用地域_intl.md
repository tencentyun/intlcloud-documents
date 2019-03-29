## Overview

You can create logsets and log topics in different regions when using CLS. Regions refer to the geographical areas of physical IDCs and networks are completely isolated between regions. You can select the nearest region based on your business scenario and target user's geographical location to reduce log data access latency and improve access speed. 


### Notes about Shenzhen/Shanghai Finance Zone

Compliance zone customized according to regulatory requirements for finance industry features high level of security and isolation. CLS is supported in Shenzhen and Shanghai Finance Zones now. Verified clients in finance industry can apply for the zone by submitting tickets. For more information, see the [introduction to finance zones](https://cloud.tencent.com/document/product/304/2766).


## Available Regions and Abbreviations

| Region | Abbreviation | Request Domain Name |
| -------- | --------------- | -------------------------------- |
| Beijing | ap-beijing | ap-beijing.cls.myqcloud.com |
| Shanghai | ap-shanghai | ap-shanghai.cls.myqcloud.com |
| Guangzhou | ap-guangzhou | ap-guangzhou.cls.myqcloud.com |
| Chengdu | ap-chengdu | ap-chengdu.cls.myqcloud.com |
| Shenzhen Finance | ap-shenzhen-fsi | ap-shenzhen-fsi.cls.myqcloud.com |
| Shanghai Finance | ap-shanghai-fsi | ap-shanghai-fsi.cls.myqcloud.com |
| Toronto | na-toronto | na-toronto.cls.myqcloud.com |



## Note

If other cloud products are integrated to CLS, try to select a logset in the same region as other cloud products. Cloud products in the same region read/write data over a private network, which can effectively reduce latency and improve access speed.

