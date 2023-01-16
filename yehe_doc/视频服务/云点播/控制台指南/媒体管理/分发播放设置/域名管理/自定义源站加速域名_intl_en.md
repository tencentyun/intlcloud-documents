## Operation scene

The Video-on-Demand open CDN hosting capability helps users distribute media resources from their own origin sites, and supports the origin-pull capabilities of their own  origin sites and third-party object storage sites. By creating a custom domain name and configuring the origin site type, origin-pull request protocol, and origin site address, the user can realize the custom origin site feature (only custom domain names are supported to configure the custom origin-pull capability).

## Configuration Guide
1.  Log in to the [VOD console](https://console.tencentcloud.com/vod/overview), click **Application Management** on the left navigation bar to enter the application list page.
2.  Find the application that needs to be set, and click the application name to enter the application management page.
3.  By default, go to **Media Asset Management**>**Audio and Video Management**, "Uploaded" page.
4.  Select **Distribution Playback Settings** > [Domain Management](https://console.tencentcloud.com/vod/distribute-play/domain) in the left navigation bar to enter the domain management page.
5. Click the top **custom** **origin server** **domains** for accelerated source site to enter the "custom origin server domains " list page.
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_733809_BQj68x44F_6Suq8h_1673602703?w=1480&h=480)
6.  Click **Add Domain** to complete domain name configuration and origin server configuration according to your actual needs:
 - Domain configuration
Fill in the domain name and select the domain name acceleration area. For related information, see [Adding a Domain Name](https://www.tencentcloud.com/document/product/266/35572).
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_637821_VGb4iPXqW3eJXnUP_1673602856?w=1363&h=204)
 - Origin configuration
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_50088_65AcmuvO-erFQP_H_1673602907?w=882&h=409)
**Origin type**
Video-on-Demand provides three origin-pull types: self-owned origin site and third-party object storage, and users can choose configurations according to actual needs.
<table>
   <tr>
      <td >Self-owned server</td>
      <td >Already have a stable running business server (that is, the source site), fill in the corresponding IP address list, or a domain name as the origin site address.
</td>
   </tr>
   <tr>
      <td>Third-party object storage</td>
      <td>Third-party object storage other than Tencent Cloud, the currently supported third parties are: Qiniu Cloud, Baidu Cloud, Alibaba Cloud and AWS.
</td>
   </tr>
</table>

  **Origin-pull protocol**
The protocol used when the VOD acceleration node returns to the user's origin site, HTTP or HTTPS.
<table>
   <tr>
      <td >HTTP origin-pull</td>
      <td>HTTP origin-pull is used when the access is HTTP or HTTPS.</td>
   </tr>
   <tr>
      <td>HTTPS origin-pull</td>
      <td>HTTPS origin-pull is used when the access is HTTP or HTTPS.</td>
   </tr>
	    <tr>
      <td>Protocol follows</td>
      <td>HTTP requests use HTTP origin-pull, and HTTPS requests use HTTPS origin-pull.</td>
   </tr>
</table>

>? In the case of HTTPS origin-pull, please ensure that the origin site supports HTTPS access, otherwise the origin-pull will fail.

  **source address**
<table>
   <tr>
      <td>Self-owned server</td>
      <td>Support to populate multiple IP origin sites or a domain name origin site (separated by commas).</td>
   </tr>
   <tr>
      <td>Third-party object storage</td>
      <td><li>If the resource has been stored in a third-party object storage, please enter a valid storage bucket access address as the source site (it cannot contain http:// or http:// protocol header). The currently supported third parties are: Qiniuyun Kodo, Baidu Cloud BOS, Alibaba Cloud OSS and AWS S3.</li><br><li>TO origin-pull to a third-party private storage bucket, you need to fill in a valid key and enable the origin authentication, that is, enable access to the private storage bucket.
</li> </td>
   </tr>
</table>

>? The origin site can specify the origin-pull HOST, and the origin-pull HOST is used to specify the specific site of the domain name/ip of the site that the CDN node visits at the origin when origin-pull. If no origin-pull HOST is specified, the currently created acceleration domain name is used by default.
4. Domain name resolution. For the added custom acceleration domain name, you need to configure a CNAME on the DNS service provider specified by the domain name so that users can access your video media through the domain name. For details, see [VOD Acceleration Domain Name - Domain Name Resolution](https://www.tencentcloud.com/document/product/266/42076).


## Modify origin-pull configuration
For the added custom domain name, it can be adjusted and modified according to the actual needs of users. The modification method is as follows:
1.  On the [Domain Management](https://console.tencentcloud.com/vod/distribute-play/domain) > **custom origin server domains** page, select the custom domain name to be modified, click Settings, and enter the details page.
2. Click **Modify** to modify the original configuration information. It takes 5 minutes for the modified results to take effect.
![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_862633_9Ssc4zeoNwq57qB1_1673604340?w=1301&h=268)

>?
>- When the user-defined origin site is switched to the Video-on-Demand origin site, the domain name of the custom origin site needs to be deactivated and deleted first, and then the corresponding domain name should be added to the VOD‘s acceleration domain name.
>- When a user needs to use a custom origin site to return to the origin, he must first disable and delete the domain name configured in the on-demand acceleration domain name, and then go to the custom origin site acceleration domain name to add it.