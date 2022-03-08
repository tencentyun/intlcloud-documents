## Overview

You can create logsets and log topics in different regions when using CLS. Regions are independent geographical areas where IDCs are located. Tencent Cloud regions are completely isolated. Select the nearest region according to your business needs and the location of your targeted users to reduce log access latency and improve user experience. 

## Available Regions

| Region     | Alias             |
| :------- | :--------------- |
| Beijing     | ap-beijing       |
| Guangzhou     | ap-guangzhou     |
| Shanghai     | ap-shanghai      |
| Chengdu     | ap-chengdu       |
| Nanjing     | ap-nanjing       |
| Chongqing     | ap-chongqing     |
| Hong Kong (China)  | ap-hongkong      |
| Taipei (China) | ap-taipei        |
| Silicon Valley | na-siliconvalley |
| Virginia | na-ashburn |
| Singapore | ap-singapore |
| Bangkok | ap-bangkok |
| Mumbai | ap-mumbai |
| Frankfurt | eu-frankfurt |
| Tokyo     | ap-tokyo         |
| Seoul | ap-seoul |
| Moscow | eu-moscow |
| Jakarta   | ap-jakarta       |
| Toronto | na-toronto |


>? 
> - If other cloud products are integrated into CLS, try to select a logset in the same region as the other cloud products. Cloud products in the same region access each other over a private network, which effectively reduces latency and improves access speed.
> 

## Domain Names

The domain names used by different CLS modules differ as follows:

<dx-tabs>
::: LogListener [](id:LogListener)

 LogListener is a log collection client provided by CLS and can report local logs to CLS. It uses the following domain names:
<table>
<thead>
<tr>
<th>Region</th>
<th>Alias</th>
<th>Private Network Domain Name</th>
<th>Public Network Domain Name</th>
</tr>
</thead>
<tbody><tr>
<td>Beijing</td>
<td>ap-beijing</td>
<td>ap-beijing.cls.tencentyun.com</td>
<td>ap-beijing.cls.tencentcs.com</td>
</tr>
<tr>
<td>Guangzhou</td>
<td>ap-guangzhou</td>
<td>ap-guangzhou.cls.tencentyun.com</td>
<td>ap-guangzhou.cls.tencentcs.com</td>
</tr>
<tr>
<td>Shanghai</td>
<td>ap-shanghai</td>
<td>ap-shanghai.cls.tencentyun.com</td>
<td>ap-shanghai.cls.tencentcs.com</td>
</tr>
<tr>
<td>Chengdu</td>
<td>ap-chengdu</td>
<td>ap-chengdu.cls.tencentyun.com</td>
<td>ap-chengdu.cls.tencentcs.com</td>
</tr>
<tr>
<td>Nanjing</td>
<td>ap-nanjing</td>
<td>ap-nanjing.cls.tencentyun.com</td>
<td>ap-nanjing.cls.tencentcs.com</td>
</tr>
<tr>
<td>Chongqing</td>
<td>ap-chongqing</td>
<td>ap-chongqing.cls.tencentyun.com</td>
<td>ap-chongqing.cls.tencentcs.com</td>
</tr>
<tr>
<td>Hong Kong (China)</td>
<td>ap-hongkong</td>
<td>ap-hongkong.cls.tencentyun.com</td>
<td>ap-hongkong.cls.tencentcs.com</td>
</tr>
<tr>
<td>Taipei (China)</td>
<td>ap-taipei</td>
<td>ap-taipei.cls.tencentyun.com</td>
<td>ap-taipei.cls.tencentcs.com</td>
</tr>
<tr>
<td>Silicon Valley</td>
<td>na-siliconvalley</td>
<td>na-siliconvalley.cls.tencentyun.com</td>
<td>na-siliconvalley.cls.tencentcs.com</td>
</tr>
<tr>
<td>Virginia</td>
<td>na-ashburn</td>
<td>na-ashburn.cls.tencentyun.com</td>
<td>na-ashburn.cls.tencentcs.com</td>
</tr>
<tr>
<td>Singapore</td>
<td>ap-singapore</td>
<td>ap-singapore.cls.tencentyun.com</td>
<td>ap-singapore.cls.tencentcs.com</td>
</tr>
<tr>
<td>Bangkok</td>
<td>ap-bangkok</td>
<td>ap-bangkok.cls.tencentyun.com</td>
<td>ap-bangkok.cls.tencentcs.com</td>
</tr>
<tr>
<td>Mumbai</td>
<td>ap-mumbai</td>
<td>ap-mumbai.cls.tencentyun.com</td>
<td>ap-mumbai.cls.tencentcs.com</td>
</tr>
<tr>
<td>Frankfurt</td>
<td>eu-frankfurt</td>
<td>eu-frankfurt.cls.tencentyun.com</td>
<td>eu-frankfurt.cls.tencentcs.com</td>
</tr>
<tr>
<td>Tokyo</td>
<td>ap-tokyo</td>
<td>ap-tokyo.cls.tencentyun.com</td>
<td>ap-tokyo.cls.tencentcs.com</td>
</tr>
<tr>
<td>Seoul</td>
<td>ap-seoul</td>
<td>ap-seoul.cls.tencentyun.com</td>
<td>ap-seoul.cls.tencentcs.com</td>
</tr>
<tr>
<td>Moscow</td>
<td>eu-moscow</td>
<td>eu-moscow.cls.tencentyun.com</td>
<td>eu-moscow.cls.tencentcs.com</td>
</tr>
<tr>
<td>Jakarta</td>
<td>ap-jakarta</td>
<td>ap-jakarta.cls.tencentyun.com</td>
<td>ap-jakarta.cls.tencentcs.com</td>
</tr>
<tr>
<td>Toronto</td>
<td>na-toronto</td>
<td>na-toronto.cls.tencentyun.com</td>
<td>na-toronto.cls.tencentcs.com</td>
</tr>
<tr>
</tbody></table>
:::
::: CLS/sAPI/s3.0 [](id:API3)

[CLS API 3.0](https://intl.cloud.tencent.com/document/product/614/11321) is CLS's latest API version and complies with the unified API specifications of Tencent Cloud. You can use the APIs to manage resources such as log topics and alarm policies. The APIs use the following domain names:

>? If you access CLS via the public network, you can also use unified domain name cls.tencentcloudapi.com. Your API request will be automatically resolved to a server that is **nearest** to the client. For latency-sensitive businesses, we recommend that you specify the region in the domain name.
>

| Region     | Alias             | Private Network Domain Name                            | Public Network Domain Name                           |
| :------- | :--------------- | -------------------------------- | ---------------------------------------- |
| Beijing     | ap-beijing       | cls.internal.tencentcloudapi.com | cls.ap-beijing.tencentcloudapi.com       |
| Guangzhou     | ap-guangzhou     | cls.internal.tencentcloudapi.com | cls.ap-guangzhou.tencentcloudapi.com     |
| Shanghai     | ap-shanghai      | cls.internal.tencentcloudapi.com | cls.ap-shanghai.tencentcloudapi.com      |
| Chengdu     | ap-chengdu       | cls.internal.tencentcloudapi.com | cls.ap-chengdu.tencentcloudapi.com       |
| Nanjing     | ap-nanjing       | cls.internal.tencentcloudapi.com | cls.ap-nanjing.tencentcloudapi.com       |
| Chongqing     | ap-chongqing     | cls.internal.tencentcloudapi.com | cls.ap-chongqing.tencentcloudapi.com     |
| Hong Kong (China) | ap-hongkong      | cls.internal.tencentcloudapi.com | cls.ap-hongkong.tencentcloudapi.com      |
| Taipei (China) | ap-taipei        | cls.internal.tencentcloudapi.com | cls.ap-taipei.tencentcloudapi.com        |
| Silicon Valley     | na-siliconvalley | cls.internal.tencentcloudapi.com | cls.na-siliconvalley.tencentcloudapi.com |
| Virginia | na-ashburn       | cls.internal.tencentcloudapi.com | cls.na-ashburn.tencentcloudapi.com       |
| Singapore   | ap-singapore     | cls.internal.tencentcloudapi.com | cls.ap-singapore.tencentcloudapi.com     |
| Bangkok     | ap-bangkok       | cls.internal.tencentcloudapi.com | cls.ap-bangkok.tencentcloudapi.com       |
| Mumbai     | ap-mumbai        | cls.internal.tencentcloudapi.com | cls.ap-mumbai.tencentcloudapi.com        |
| Frankfurt | eu-frankfurt     | cls.internal.tencentcloudapi.com | cls.eu-frankfurt.tencentcloudapi.com     |
| Tokyo     | ap-tokyo         | cls.internal.tencentcloudapi.com | cls.ap-tokyo.tencentcloudapi.com         |
| Seoul     | ap-seoul         | cls.internal.tencentcloudapi.com | cls.ap-seoul.tencentcloudapi.com         |
| Moscow   | eu-moscow        | cls.internal.tencentcloudapi.com | cls.eu-moscow.tencentcloudapi.com        |
| Jakarta   | ap-jakarta       | cls.internal.tencentcloudapi.com | cls.ap-jakarta.tencentcloudapi.com       |
| Toronto   | na-toronto       | cls.internal.tencentcloudapi.com | cls.na-toronto.tencentcloudapi.com       |

:::
::: CLS/sAPI/s2017 [](id:API2017)

[CLS API 2017](https://intl.cloud.tencent.com/document/product/614/16907) is CLS's earlier API version and is not recommended to be used alone. The APIs use the following domain names:

<table>
<thead>
<tr>
<th>Region</th>
<th>Alias</th>
<th>Private Network Domain Name</th>
<th>Public Network Domain Name</th>
</tr>
</thead>
<tbody><tr>
<td>Beijing</td>
<td>ap-beijing</td>
<td>ap-beijing.cls.tencentyun.com</td>
<td>ap-beijing.cls.tencentcs.com</td>
</tr>
<tr>
<td>Guangzhou</td>
<td>ap-guangzhou</td>
<td>ap-guangzhou.cls.tencentyun.com</td>
<td>ap-guangzhou.cls.tencentcs.com</td>
</tr>
<tr>
<td>Shanghai</td>
<td>ap-shanghai</td>
<td>ap-shanghai.cls.tencentyun.com</td>
<td>ap-shanghai.cls.tencentcs.com</td>
</tr>
<tr>
<td>Chengdu</td>
<td>ap-chengdu</td>
<td>ap-chengdu.cls.tencentyun.com</td>
<td>ap-chengdu.cls.tencentcs.com</td>
</tr>
<tr>
<td>Nanjing</td>
<td>ap-nanjing</td>
<td>ap-nanjing.cls.tencentyun.com</td>
<td>ap-nanjing.cls.tencentcs.com</td>
</tr>
<tr>
<td>Chongqing</td>
<td>ap-chongqing</td>
<td>ap-chongqing.cls.tencentyun.com</td>
<td>ap-chongqing.cls.tencentcs.com</td>
</tr>
<tr>
<td>Hong Kong (China)</td>
<td>ap-hongkong</td>
<td>ap-hongkong.cls.tencentyun.com</td>
<td>ap-hongkong.cls.tencentcs.com</td>
</tr>
<tr>
<td>Taipei (China)</td>
<td>ap-taipei</td>
<td>ap-taipei.cls.tencentyun.com</td>
<td>ap-taipei.cls.tencentcs.com</td>
</tr>
<tr>
<td>Silicon Valley</td>
<td>na-siliconvalley</td>
<td>na-siliconvalley.cls.tencentyun.com</td>
<td>na-siliconvalley.cls.tencentcs.com</td>
</tr>
<tr>
<td>Virginia</td>
<td>na-ashburn</td>
<td>na-ashburn.cls.tencentyun.com</td>
<td>na-ashburn.cls.tencentcs.com</td>
</tr>
<tr>
<td>Singapore</td>
<td>ap-singapore</td>
<td>ap-singapore.cls.tencentyun.com</td>
<td>ap-singapore.cls.tencentcs.com</td>
</tr>
<tr>
<td>Bangkok</td>
<td>ap-bangkok</td>
<td>ap-bangkok.cls.tencentyun.com</td>
<td>ap-bangkok.cls.tencentcs.com</td>
</tr>
<tr>
<td>Mumbai</td>
<td>ap-mumbai</td>
<td>ap-mumbai.cls.tencentyun.com</td>
<td>ap-mumbai.cls.tencentcs.com</td>
</tr>
<tr>
<td>Frankfurt</td>
<td>eu-frankfurt</td>
<td>eu-frankfurt.cls.tencentyun.com</td>
<td>eu-frankfurt.cls.tencentcs.com</td>
</tr>
<tr>
<td>Tokyo</td>
<td>ap-tokyo</td>
<td>ap-tokyo.cls.tencentyun.com</td>
<td>ap-tokyo.cls.tencentcs.com</td>
</tr>
<tr>
<td>Seoul</td>
<td>ap-seoul</td>
<td>ap-seoul.cls.tencentyun.com</td>
<td>ap-seoul.cls.tencentcs.com</td>
</tr>
<tr>
<td>Moscow</td>
<td>eu-moscow</td>
<td>eu-moscow.cls.tencentyun.com</td>
<td>eu-moscow.cls.tencentcs.com</td>
</tr>
<tr>
<td>Jakarta</td>
<td>ap-jakarta</td>
<td>ap-jakarta.cls.tencentyun.com</td>
<td>ap-jakarta.cls.tencentcs.com</td>
</tr>
<tr>
<td>Toronto</td>
<td>na-toronto</td>
<td>na-toronto.cls.tencentyun.com</td>
<td>na-toronto.cls.tencentcs.com</td>
</tr>
</tbody></table>
:::
::: Kafka/sUploading Logs [](id:Kafka)

With the feature of [uploading logs via Kafka](https://intl.cloud.tencent.com/document/product/614/43574), you can use Kafka Producer SDKs or other Kafka agents to upload logs to CLS. The feature uses the following domain names:

<table>
<thead>
<tr>
<th>Region</th>
<th>Alias</th>
<th>Private Network Domain Name</th>
<th>Public Network Domain Name</th>
</tr>
</thead>
<tbody><tr>
<td>Beijing</td>
<td>ap-beijing</td>
<td>bj-producer.cls.tencentyun.com</td>
<td>bj-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Guangzhou</td>
<td>ap-guangzhou</td>
<td>gz-producer.cls.tencentyun.com</td>
<td>gz-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Shanghai</td>
<td>ap-shanghai</td>
<td>sh-producer.cls.tencentyun.com</td>
<td>sh-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Chengdu</td>
<td>ap-chengdu</td>
<td>cd-producer.cls.tencentyun.com</td>
<td>cd-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Nanjing</td>
<td>ap-nanjing</td>
<td>nj-producer.cls.tencentyun.com</td>
<td>nj-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Chongqing</td>
<td>ap-chongqing</td>
<td>cq-producer.cls.tencentyun.com</td>
<td>cq-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Hong Kong (China)</td>
<td>ap-hongkong</td>
<td>hk-producer.cls.tencentyun.com</td>
<td>hk-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Taipei (China)</td>
<td>ap-taipei</td>
<td>tpe-producer.cls.tencentyun.com</td>
<td>tpe-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Silicon Valley</td>
<td>na-siliconvalley</td>
<td>usw-producer.cls.tencentyun.com</td>
<td>usw-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Virginia</td>
<td>na-ashburn</td>
<td>use-producer.cls.tencentyun.com</td>
<td>use-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Singapore</td>
<td>ap-singapore</td>
<td>sg-producer.cls.tencentyun.com</td>
<td>sg-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Bangkok</td>
<td>ap-bangkok</td>
<td>th-producer.cls.tencentyun.com</td>
<td>th-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Mumbai</td>
<td>ap-mumbai</td>
<td>in-producer.cls.tencentyun.com</td>
<td>in-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Frankfurt</td>
<td>eu-frankfurt</td>
<td>de-producer.cls.tencentyun.com</td>
<td>de-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Tokyo</td>
<td>ap-tokyo</td>
<td>jp-producer.cls.tencentyun.com</td>
<td>jp-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Seoul</td>
<td>ap-seoul</td>
<td>kr-producer.cls.tencentyun.com</td>
<td>kr-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Moscow</td>
<td>eu-moscow</td>
<td>ru-producer.cls.tencentyun.com</td>
<td>ru-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Jakarta</td>
<td>ap-jakarta</td>
<td>jkt-producer.cls.tencentyun.com</td>
<td>jkt-producer.cls.tencentcs.com</td>
</tr>
<tr>
<td>Toronto</td>
<td>na-toronto</td>
<td>ca-producer.cls.tencentyun.com</td>
<td>ca-producer.cls.tencentcs.com</td>
</tr>
</tbody></table>
:::
</dx-tabs>