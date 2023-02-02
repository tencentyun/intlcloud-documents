## Introduction

The custom origin-pull feature relies on the Video-on-demand CDN capability. By creating a custom domain name and configuring the origin-pull information, users can accelerate the distribution of media files stored in the third-party origin site with the help of Video- on-demand, providing users with cloud-based services in multi-cloud scenarios. Media distribution scheme. This article will introduce how to configure and use Video-on-demand custom origin-pull capabilities.

## Usage Scenarios

- **Origin site migration costs are high:** The user's media resource is stored on other third-party origin sites, and the content of the origin site is highly coupled with the third-party platform, so it is difficult to migrate the origin site. Based on the custom origin-pull feature, you can use it without migrating the origin site and accelerate content distribution by VOD‘s CDN.
- **High playback quality requirements**:  When the User’s content has high requirements for network delay and lag, it is difficult to meet user needs with other third-party platforms. The custom origin-pull feature can ensure smoother audio and video playback for customers, to ensure the quality of services.
- **Multi-cloud Coexistence Reduces Risk:** The user‘s content and business need multiple content acceleration channels to ensure business reliability and improve disaster recovery capabilities. You can choose Tencent Cloud Video-on-demand CDN for accelerated audio and video distribution.


## Prerequisite

1. [Register](https://www.tencentcloud.com/en/account/register?s_url=https%3A%2F%2Fconsole.tencentcloud.com%2Fvod%2Foverview) and [log in](https://www.tencentcloud.com/en/account/login?s_url=https%3A%2F%2Fconsole.tencentcloud.com%2Fvod%2Foverview) to the Tencent Cloud account, and complete the account real-name authentication.
2. The Tencent Cloud VOD service has been activated. If it is not activated, please go to activate the [Video-on-demand](https://console.tencentcloud.com/vod/overview) service.
3. Go to the [feature experience](https://console.tencentcloud.com/vod/overview) module under the console, and enable the custom origin-pull feature.


## Supported origin types

- **Own origin server**
- **Third party storage**

## Directions
### Step 1: Create a custom domain name and configure  origin-pull information

1. After the custom origin-pull is enabled, log in to the VOD console, and select **Distribution Playback Settings** > [Domain Management](https://console.tencentcloud.com/vod/distribute-play/domain) in the left navigation bar to enter the **Domain Management** page.
2. Click **Custom** **origin server** **domains** of the origin site acceleration at the top to enter the page of the **custom domain name** of the origin site acceleration.
![img](https://qcloudimg.tencent-cloud.cn/raw/e68e04641c3ad616450a70c72d5d3dcd.png)
3. Click Add Domain, fill in the registered domain name and select the acceleration region. For details, see [Customizing Domain Names](https://www.tencentcloud.com/document/product/266/35572).
![img](https://qcloudimg.tencent-cloud.cn/raw/0fbcc49821fd7eebffd9ad17a81072b1.png)
4. Fill in the origin station configuration according to the user's actual origin-pull requirements. Currently, **self-owned** **server** and **third-party storage** are supported. The specific configuration instructions are as follows:   
![img](https://qcloudimg.tencent-cloud.cn/raw/9ac80033d6fb055e299a2f355d0d1825.png) 
   **Own origin server**
If the user wants to use a business server running stably as the  origin site to accelerate the distribution of media files on it with the help of Video-on-Demand CDN, please configure the origin site as follows:
<table>
   <tr>
      <th width="0px" style="text-align:center">Configuration item</td>
      <th width="0px" style="text-align:center">Describe</td>
   </tr>
   <tr>
      <td>Origin type</td>
      <td>Choose<b>Self-owned server</b></td>
   </tr>
   <tr>
      <td>Origin-pull protocol</td>
      <td>According to the support of the origin site, select the origin-pull request protocol, which supports HTTP, HTTPS ,and protocol following</td>
   </tr>
	   <tr>
      <td>Origin-pull address</td>
      <td>Support filling in multiple IP origin sites (separated by commas) or a domain name origin site</td>
   </tr>
	 <tr>
      <td>Origin-pull HOST</td>
      <td>The own origin site can specify the origin-pull HOST, and the origin-pull HOST is used to specify the specific site of the domain name/IP of the site accessed by the CDN node when origin pulling.<br>If the origin-pull HOST is not specified, the current accelerated domain name is used by default</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">

- The orgin site address does not support the default domain name of VOD.
- Protocol following can realize HTTP access using HTTP origin-pull, and HTTPS access using HTTPS origin-pull (the origin site needs to support HTTPS access).
- It is supported to select a domain name as the origin-pull address, and this domain name cannot be the same as the business acceleration domain name.
</dx-alert>
<b>**Third-party object storage**</b><br>
If you want to accelerate the distribution of media files stored in third-party object storage with the help of Video-on-Demand CDN capabilities, please configure the origin site as follows:          
<table>
   <tr>
      <th width="0px" style="text-align:center">Configuration item</td>
      <th width="0px" style="text-align:center">Describe</td>
   </tr>
   <tr>
      <td>Origin type</td>
      <td>Choose<b>third-party object storage</b></td>
   </tr>
   <tr>
      <td>Third-party object storage</td>
      <td>Currently supported third-party object storage includes Alibaba Cloud OSS and AWS S3</td>
   </tr>
	   <tr>
	<td>Origin-pull protocol</td>
	  <td>Support HTTP, HTTPS</td>
   </tr>
	 <tr>
      <td>Origin-pull address</td>
      <td>Enter a valid bucket access address as the origin server (it cannot contain http:// or http:// protocol header)</td>
   </tr>
</table>

![img](https://qcloudimg.tencent-cloud.cn/raw/f5ca4759794c94ffba9f6a960b9a8641.png)<br>
If you choose a privately accessed third-party object storage bucket as the origin site, you need to fill in a valid access ID and key for origin-pull authentication. After the authentication is passed, the private storage bucket access will be enabled. For details, see [Access Key Obtaining Guidelines](https://www.tencentcloud.com/document/product/266/53277).<br>

![img](https://qcloudimg.tencent-cloud.cn/raw/66864ace26867520f76172f2901ad138.png)

#### **Step 2: Customize domain name resolution**

For the added custom accelerated domain name, you need to configure a CNAME on the DNS service provider specified by the domain name so that users can access your media files through the accelerated domain name. For details, see [VOD Accelerated Domain Name - Domain Name Resolution](https://www.tencentcloud.com/document/product/266/42076).

#### **Step 3: View and modify the configuration results of custom origin-pull**

1. Go to **domain management**, enter the **custom origin server domains**, select the created domain name and click **Settings**.
![img](https://qcloudimg.tencent-cloud.cn/raw/3522690fd01bd3c0f90eb1065dc87965.png)
2. Click **Basic Configuration** to view the origin-pull configuration information of the current custom domain name and modify it.
![img](https://qcloudimg.tencent-cloud.cn/raw/bb04aa08590e9f88680c29eb19a502b9.png)

Through the above steps, users can complete the origin-pull configuration based on their own origin site or third-party object storage, and can distribute media files on the custom origin site through the Video-on-demand CDN. The specific distribution process is described as follows:

1. If the user adds a custom domain name (for example: test.com) and completes the domain name resolution and configuration of origin-pull, when accessing the media files under the domain name through the browser (for example: http://www.test.com/test. mp4), it will first initiate a domain name resolution request to Local DNS;
2. When Local DNS resolves the domain name test.com, it finds that a CNAME has been configured: www.test.com.cdn.dnsv1.com, and will resolve the request to Tencent GSLB (Global Server Load Balance, which is the global load balancing system independently developed by Tencent. );
3. GSLB will return the best access node IP list, and Local DNS will obtain the corresponding resolution IP;
4. The user obtains the best access IP node;
5. The user initiates an access request to http://www.test.com/test.mp4 to the best access IP node;
6. If there is test.mp4 cached on the CDN node, the user will get the data and end the request. If the CDN node does not cache the resource, the node will initiate a request for test.mp4 to the business origin site you configured. After obtaining the resource, it will cache it in the current node by default and return the resource to the user. At this time to end the request.

>? When users use the custom origin-pull feature to accelerate distribution and play media files, downlink traffic fees and origin-pull traffic fees will be incurred. The downlink traffic fees are charged by Video-on-demand. For specific rules, please refer to [traffic billing](https://www.tencentcloud.com/document/product/266/14666#video-acceleration) and [traffic  packages](https://www.tencentcloud.com/document/product/266/52806#traffic-pack). The traffic fee of the origin site is charged by the origin site.