## Overview

A **region** is an area where a Tencent Cloud managed data center is deployed. COS data is stored in buckets in these regions. You can use COS to store your data in multiple regions. In general, you are advised to create buckets in the region closest to the location where your business is conducted. In this way, latency and costs can be reduced and compliance requirements can be met.

For example, if your business is distributed in South China, creating buckets in the Guangzhou region can accelerate the object upload and download speeds.

**Default endpoint** refers to the COS bucket’s default domain, which is automatically generated when the bucket is created. Buckets residing in different regions have different default domains. To view the default domain, you can go to the [COS console](https://console.cloud.tencent.com/cos5), click the name of the desired bucket, click **Overview**, and find the **Domain Information** area.



### Chinese mainland

<table>
   <tr>
	 <th colspan=3><center>Region</center></th>
      <th>Region Abbreviation</th>
      <th>Default Endpoint (Upload/Download/Management)</th>
   </tr>
   <tr>
      <td rowspan=10>Chinese mainland</td>
      <td rowspan=7 nowrap="nowrap">Public cloud regions</td>
      <td nowrap="nowrap">Beijing Zone 1 (sold out)</td>
      <td>ap-beijing-1</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-beijing-1.myqcloud.com</td>
   </tr>
   <tr>
      <td>Beijing</td>
      <td>ap-beijing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com</td>
   </tr>
   <tr>
      <td>Nanjing</td>
      <td>ap-nanjing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-nanjing.myqcloud.com</td>
   </tr>
   <tr>
      <td>Shanghai</td>
      <td>ap-shanghai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com</td>
   </tr>
   <tr>
      <td>Guangzhou</td>
      <td>ap-guangzhou</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com</td>
   </tr>
   <tr>
      <td>Chengdu</td>
      <td>ap-chengdu</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com</td>
   </tr>
   <tr>
      <td>Chongqing</td>
      <td>ap-chongqing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com</td>
   </tr>
</table>




### Outside Chinese mainland

<table>
   <tr>
	 <th colspan=3><center>Region</center></th>
      <th>Region Abbreviation</th>
      <th>Default Endpoint (Upload/Download/Management)</th>
   </tr>
   <tr>
      <td rowspan=7>Asia Pacific</td>
      <td rowspan=13 nowrap="nowrap">Public cloud regions</td>
      <td>Hong Kong (China)</td>
      <td>ap-hongkong</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-hongkong.myqcloud.com</td>
   </tr>
   <tr>
      <td>Singapore</td>
      <td>ap-singapore</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-singapore.myqcloud.com</td>
   </tr>
   <tr>
      <td>Mumbai</td>
      <td>ap-mumbai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-mumbai.myqcloud.com</td>
   </tr>
   <tr>
      <td  nowrap="nowrap">Jakarta</td>
      <td>ap-jakarta</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-jakarta.myqcloud.com</td>
   </tr>
   <tr>
      <td>Seoul</td>
      <td>ap-seoul</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-seoul.myqcloud.com</td>
   </tr>
   <tr>
      <td>Bangkok</td>
      <td>ap-bangkok</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-bangkok.myqcloud.com</td>
   </tr>
   <tr>
      <td>Tokyo</td>
      <td>ap-tokyo</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-tokyo.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=3>North America</td>
      <td nowrap="nowrap">Silicon Valley (US West)</td>
      <td>na-siliconvalley</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-siliconvalley.myqcloud.com</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Virginia (US East)</td>
      <td>na-ashburn</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-ashburn.myqcloud.com</td>
   </tr>
   <tr>
      <td>Toronto</td>
      <td>na-toronto</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=1>South America</td>
      <td>São Paulo</td>
      <td>sa-saopaulo</td>
      <td>&lt;BucketName-APPID&gt;.cos.sa-saopaulo.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=2>Europe</td>
      <td>Frankfurt</td>
      <td>eu-frankfurt</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-frankfurt.myqcloud.com</td>
   </tr>
</table>



### Global acceleration endpoint

A global acceleration endpoint is formatted as &lt;BucketName-APPID&gt;.`cos.accelerate.myqcloud.com`. For more information about global acceleration endpoints and the use cases, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).


### Example

Assume that you have logged in to the COS console as the root account (`APPID` is `1250000000`) and created a bucket named **examplebucket** in the **Guangzhou** region, the default endpoint of the bucket will be:

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

>?
>
>- examplebucket-1250000000: indicates that the bucket is owned by the user whose `APPID` is `1250000000`. `APPID` is a fixed and unique ID assigned by the system when you successfully applied for the Tencent Cloud account. You can view it at [Account Information](https://console.cloud.tencent.com/developer).
>- cos: Cloud Object Storage (COS)
>- ap-guangzhou: abbreviation of the bucket region
>- myqcloud.com: indicates Tencent Cloud domain (fixed)

If you store an image (picture.jpg) to the created bucket, the access URL of the image will be:

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/picture.jpg
```

>?If you have set the access permission of your image to **public read and private write**, you can copy the image access URL and paste it in the browser to view the image details.
>



## Private Network and Public Network Access

If an intra-region Cloud Virtual Machine (CVM) instance accesses COS using the default domain, data will be transferred over a private network by default. In this case, data uploads and downloads will generate private network traffic, but this traffic will not be billed. However, note that you will still be charged for the number of requests.

Tencent Cloud COS adopts intelligent resolution for COS endpoints. In this way, the optimal linkage can be provided for you to access COS with different ISPs.

If you deploy a service in Tencent Cloud to access COS, intra-region access requests will be automatically directed to a private network address. Currently, cross-region requests do not support private network access and will be resolved to a public network address by default. If you have requests for cross-region private network access, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

For more information about private network and public network access, see [Request Creation Overview](https://intl.cloud.tencent.com/document/product/436/30613).

