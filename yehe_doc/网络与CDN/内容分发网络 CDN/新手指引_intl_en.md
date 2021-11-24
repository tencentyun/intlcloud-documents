



## Concepts

To cope with the complicated network environment and fix various network problems in internet businesses, Tencent Cloud deploys high-performance cache nodes globally based on the existing network structure to create a new virtual network architecture, so you can store your business content on the edge servers closer to your users according to your cache policies, shortening the distance between users and content, reducing the access latency, and improving the availability.

To better distinguish between the acceleration services, Tencent Cloud provides different products for different acceleration types:

- **CDN** for static resources: the content stays the **same** in the responses to multiple requests for the same resource.
Examples include html, css and js files, images, videos, software installation packages, APK files, and compressed files.
Recommended scenarios: website static resource acceleration, file download acceleration, and audio/video acceleration.
- **ECDN** for dynamic resources: the content **varies** in the responses to multiple requests for the same resource.
Examples include APIs and .jsp, .asp, .php, .perl, and .cgi files.
Recommended scenarios: dynamic acceleration and dynamic/static acceleration.

  

<table>
  <tr>
    <td>Comparison Item</td>
    <td align='middle'><b>CDN</b></td>
    <td align='middle'><b>ECDN</b></td>
  </tr>
  <tr>
    <td>Use case</td>
    <td>Static website resource acceleration, file download acceleration, and audio/video on demand website</td>
    <td>Ecommerce, in-game payment, financial website, and online education</td>
  </tr>
  <tr>
    <td>Coverage</td>
    <td colspan="2" align="middle">Chinese mainland<br>Outside the Chinese mainland<br>Global</td>
  </tr>
  <tr>
    <td>Billing Mode</td>
    <td align="middle">Billed by traffic hourly<br>Traffic packages available for users in the Chinese mainland. <br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/228/2949">Billing Overview</a> of CDN</td>
    <td align="middle">Billed by number of requests and excessive traffic<br>For more information, see <a href="https://intl.cloud.tencent.com/document/product/570/37505">Billing Overview</a> of ECDN</td>
  </tr>
  <tr>
    <td>Acceleration method</td>
    <td align="middle">Static content is accelerated, and dynamic content is pulled from the origin server</td>
    <td align="middle">Dynamic acceleration and dynamic/static acceleration are supported<br></td>
  </tr>
  <tr>
    <td>Resource reserve</td>
    <td colspan='2' align='middle'>More than 2,800 nodes in over 70 countries/regions, with a total reserved bandwidth of over 150 Tbps</td>
  </tr>
</table>



When connecting a domain name to be accelerated to Tencent Cloud, you can select either of the two products in the [CDN console](https://console.cloud.tencent.com/cdn):


Note that the two acceleration types use different acceleration policies and billing standards. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949) of CDN and [Billing Overview](https://intl.cloud.tencent.com/document/product/570/37505) of ECDN respectively.





## CDN Connection Example

![](https://qcloudimg.tencent-cloud.cn/raw/af95ca14834f1fb163b4d98e17f721f6.png)

### User access configured with CDN acceleration

A user in Shenzhen accesses an origin server in Beijing whose address is `1.1.1.1` through `cdntest.com`.

1. The user enters the domain name `cdntest.com` for access, the local DNS resolves the configured CNAME record value `cdntest.com.cdn.dnsv1.com`, and the request is sent to Tencent's proprietary DNS scheduling system and assigned to the optimal CDN edge server close to the user whose IP is `2.2.2.2`.
2. The user requests the CDN edge server whose IP is `2.2.2.2`. If the content has been cached on it, the user's requested content will be returned, and the process ends.
3. If the requested content is not cached on the CDN edge server, it will request the origin server in Beijing whose address is `1.1.1.1`, and the requested content will be decided by the configured host header.
4. After the CDN edge server whose IP address is `2.2.2.2` gets the resource from the origin server, it will be cached on the edge server according to the custom cache policies and returned to the user. Then, the request will end.
5. When another user close to Shenzhen accesses `cdntest.com` again, the Tencent DNS scheduling system will preferentially schedule the request to the CDN edge server whose IP is `2.2.2.2`, as it already caches the corresponding content. In this way, the user can directly get the content from the edge server without requesting it from the origin server.

### Confusing concepts

- If end users access your business through `cdntest.com`, then `cdntest.com` is the acceleration domain name.
- After an acceleration domain name is connected, the system will automatically assign a CNAME domain name suffixed with `.cdn.dnsv1.com` or `.dsa.dnsv1.com`, such as `cdntest.com.cdn.dnsv1.com` and `cdntest.com.dsa.dnsv1.com`, which needs to be resolved in the DNSPod console.
- If the CDN node does not cache the content requested by the user, the node will request such content at `1.1.1.1`, which is the origin address.
- When the CDN node is requesting `1.1.1.1`, the actually requested address is `originhost.com`, that is, `originhost.com` is the host header. Generally, the acceleration domain name and the host header domain name should be the same, which can be adjusted based on your business needs.

| Configuration Item          | Description                                                     | Use Position          |
| ----------------- | ------------------------------------------------------------ | ----------------- |
| Acceleration domain name          | Domain name to be connected to CDN, which is the actual domain name accessed by end users            | Create a Domain Name > Domain Configuration |
| Origin address/origin domain name | IP address (domain name) of the origin server. If the requested content is not on the CDN node, this address (domain name) will be accessed to get the requested content.<br /><br />**Origin server**: server that provides a service, which can process and respond to user requests. End users access your business at the origin address. An origin address can be a domain name or IP address. **The origin address cannot be the same as the acceleration domain name.** | Create a Domain Name > Origin Configuration |
| Host header         | Server content actually requested during origin-pull of the CDN node.                            | Create a Domain Name > Origin Configuration |
| CNAME domain name        | After your acceleration domain name is connected, the system will automatically assign a CNAME domain name suffixed with `.cdn.dnsv1.com` or `.dsa.dnsv1.com`.<br />After your acceleration domain names are mapped to the CNAME domain name, Tencent Cloud will dynamically change the IP address pointed to by the CNAME record and update all your acceleration domain names, eliminating your need to manually change the IP addresses pointed to them. | Configure CNAME        |



## Why CDN?

#### User experience issues that may occur when end users directly access static content on the origin server

- The farther the end user to the server, the slower the access.
- The larger the number of end users, the higher the network bandwidth fees.
- The cross-border access experience is poor.

![](https://qcloudimg.tencent-cloud.cn/raw/cb1dd401c8cbb0e3835d9e410c37c31d.png)

>?The above data is for reference only. Data fluctuations in complicated network environments are normal.

#### How CDN improves your network experience

- After CDN caches the content, end users only need to access the nearby CDN nodes to get the static content.
- The bandwidth pressure on the origin server is relieved, and the network fees are reduced.
- The globally deployed nodes improve the cross-border access experience.

![](https://qcloudimg.tencent-cloud.cn/raw/7460b780994e836d97d549b79211f517.png)

>?The above data is for reference only. Data fluctuations in complicated network environments are normal.

#### Recommended use cases of CDN

- Static website resource acceleration: CDN is suitable for caching and accelerating **static content such as images, videos, and various HTML files on common websites** (portal, ecommerce, and UGC websites, etc.), so as to deliver a smoother access experience.
- File download acceleration: CDN is suitable for **accelerating downloads of various files**. By delivering files to edge servers, CDN not only relieves the bandwidth pressure during peak hours of download, but also improve the download experience.
- Audio/Video acceleration: CDN is suitable for various **audio/video on demand websites**. Based on Tencent's many years of online video operations experience, CDN effectively ensures that end users in all regions can smoothly listen to/watch audio/video streams even when there are high numbers of concurrent access requests to audio/video resources.

## Why ECDN?

### User experience issues that may occur when end users directly access dynamic content on the origin server

- The network, region, and bandwidth factors all affect the resource requests and cause problems such as high latency and high packet loss rate.
- The network linkage may have a poor quality or even be blocked during routing.
- The public network environment is complicated, compromising the normal service experience.

![](https://qcloudimg.tencent-cloud.cn/raw/3fcb611b6d5c37e63b692daab957350f.png)

>?The above data is for reference only. Data fluctuations in complicated network environments are normal.



### How ECDN improves your network experience

- End users access nearby ECDN nodes for operations such as resource access and origin-pull.
- The status of the entire network is monitored in real time to select the optimal linkage and avoid blocked and low-quality linkages.

![](https://qcloudimg.tencent-cloud.cn/raw/e8ef115ebb2a4f719454b23e33b2dd6b.png)

>?The above data is for reference only. Data fluctuations in complicated network environments are normal.



### Recommended use cases of ECDN

- Dynamic/Static acceleration: ECDN is applicable to scenarios with both **dynamic and static resources**. It can better sustain such scenarios by automatically recognizing dynamic resources, using different acceleration policies, and implementing one-stop acceleration for dynamic and static resources. As ECDN linkage is used, **the billing standards of ECDN shall prevail for both static and dynamic resources**.
- Dynamic acceleration: ECDN is suitable for scenarios with **many dynamic resource requests**, such as game battle, ecommerce transaction, financial payment, and online education. It can select the optimal linkage for origin-pull by using various technologies such as dynamic route detection and smart routing, greatly reducing the access latency.

  
### How to activate ECDN

1. If you are a new user and activate the service in the <a href="https://console.cloud.tencent.com/cdn">CDN console</a>, both CDN and ECDN will be activated, but the unused service will not incur fees. For more information, see <a href="https://intl.cloud.tencent.com/document/product/228/32978">Configuring CDN from Scratch</a>.
2. If CDN is activated but ECDN is not, when you add a domain name for dynamic/static acceleration or dynamic acceleration for the first time, the system will automatically activate ECDN for you as shown below:

3. If you already activated ECDN in the original ECDN console, you can submit a ticket for migrating your account. After successful migration, you can use ECDN in the CDN console.

>!
>- Dynamic/Static acceleration: it is applicable to business scenarios where dynamic and static data is integrated, such as various website homepages.
>- Dynamic acceleration: it is applicable to scenarios such as account login, order transaction, API call, and real-time query.
>
>Fees generated by an ECDN domain name will be billed according to the [billing overview](https://intl.cloud.tencent.com/document/product/570/37505) of ECDN.

 


​	
​	
​	

## When to Use SCDN

If your business has additional requirements for security, you can purchase an additional security service based on CDN, i.e., SCDN. For more information, see [Secure Content Delivery Network](https://intl.cloud.tencent.com/document/product/1032).



## How to Select Acceleration Region

| End User Location                 | Acceleration Effect                                             | Selected Acceleration Region |
| :--------------------------- | ---------------------------------------------------- | ------------ |
| Chinese mainland                     | Access requests from global users will be scheduled to the cache nodes in the Chinese mainland for service  | Chinese mainland     |
| Outside Chinese mainland (including Hong Kong, Macao and Taiwan (China))                     | Access requests from global users will be scheduled to cache nodes outside the Chinese mainland for service  | Outside Chinese mainland     |
| Global          | Access requests from global users will be scheduled to the nearest node for service           | Global         |

CDN and ECDN both have globally deployed edge servers to route end users to the nodes nearest to them in their respective regions based on your choice. Note that the billing standards vary by acceleration region. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949).

>?If you have purchased a traffic package, check whether the regions where it is available match your needed acceleration region.



## Configuring CDN/ECDN from Scratch

This tutorial describes how to quickly configure CDN/ECDN and the relevant parameters. Click [Configuring CDN from Scratch](https://intl.cloud.tencent.com/document/product/228/32978) to view it.
