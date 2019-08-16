## Overview
Tencent Cloud COS supports multi-region storage, and the default access domain name varies by region. The region selected when a bucket is created cannot be modified. You are advised to select a local region for storage based on your own business needs for faster object upload and download.

>- After a bucket is created, the corresponding default domain name will be generated, which can be viewed in **Domain Name Management** of the bucket in the [COS Console](https://console.cloud.tencent.com/cos5).
>- BucketName is the custom name you enter when you create a bucket. For more information, see [Bucket Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83).
>- APPID is the account you get after you successfully register a Tencent Cloud account. It is automatically assigned by the system as a unique permanent ID, which can be viewed in **Account Information** in the [Tencent Cloud Console](https://console.cloud.tencent.com).
>- The Shenzhen Finance and Shanghai Finance regions cannot interconnect with other public cloud regions.

### Mainland China

<table>
   <tr>
	 <th colspan=3><center>Region</center></th>
      <th>Region Abbreviation</th>
      <th>Default Domain Name (Upload/Download/Management)</th>
   </tr>
   <tr>
      <td rowspan=8>Mainland China</td>
      <td rowspan=6 nowrap="nowrap">Public cloud regions</td>
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
      <td>Shanghai (East China)</td>
      <td>ap-shanghai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com</td>
   </tr>
   <tr>
      <td>Guangzhou (South China)</td>
      <td>ap-guangzhou</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com</td>
   </tr>
   <tr>
      <td>Chengdu (Southwest China)</td>
      <td>ap-chengdu</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com</td>
   </tr>
   <tr>
      <td>Chongqing</td>
      <td>ap-chongqing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=2 nowrap="nowrap">Finance cloud regions</td>
      <td>Shenzhen Finance</td>
      <td nowrap="nowrap">ap-shenzhen-fsi</td>
      <td nowrap="nowrap">&lt;BucketName-APPID&gt;.cos.ap-shenzhen-fsi.myqcloud.com</td>
   </tr>
   <tr>
      <td>Shanghai Finance</td>
      <td nowrap="nowrap">ap-shanghai-fsi</td>
      <td nowrap="nowrap">&lt;BucketName-APPID&gt;.cos.ap-shanghai-fsi.myqcloud.com</td>
   </tr>
</table>


### Outside Mainland China

<table>
   <tr>
	 <th colspan=3><center>Region</center></th>
      <th>Region Abbreviation</th>
      <th>Default Domain Name (Upload/Download/Management)</th>
   </tr>
   <tr>
      <td rowspan=6>Asia Pacific</td>
      <td rowspan=11 nowrap="nowrap">Public cloud regions</td>
      <td>Hong Kong, China</td>
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
      <td>Silicon Valley</td>
      <td>na-siliconvalley</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-siliconvalley.myqcloud.com</td>
   </tr>
   <tr>
      <td>Virginia</td>
      <td>na-ashburn</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-ashburn.myqcloud.com</td>
   </tr>
   <tr>
      <td>Toronto</td>
      <td>na-toronto</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=2>Europe</td>
      <td>Frankfurt</td>
      <td>eu-frankfurt</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-frankfurt.myqcloud.com</td>
   </tr>
   <tr>
      <td>Moscow</td>
      <td>eu-moscow</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-moscow.myqcloud.com</td>
   </tr>
</table>

> Example:
> If you create a bucket named examplebucket in the **Guangzhou** region and your APPID is 1250000000, then the default domain name of the bucket is:
```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

## Private Network and Public Network Access
The access domain names of COS use intelligent domain name resolution, so that you requests to COS can be routed through the optimal link in case of cross-ISP access.

If you deploy a service in Tencent Cloud to access COS, intra-region access requests will be automatically directed to a private network address. Cross-region requests do not support private network access for the time being and will be resolved to a public network address by default.

For more information on private network and public network access, see [Overview of Request Creation](https://intl.cloud.tencent.com/document/product/436/30613).

