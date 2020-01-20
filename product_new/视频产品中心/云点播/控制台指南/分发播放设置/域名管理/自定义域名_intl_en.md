### Operation Scenarios
After you activate VOD, the system will assign you a default domain name `xxx.vod2.myqcloud.com`, which will be used by default for all VOD resources. You can also add and resolve a custom domain name in the [VOD Console](https://console.cloud.tencent.com/vod/overview).
## Prerequisites
<!--doc - You have activated VOD. For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/266/2839).-->
- The domain name to be added has successfully obtained an ICP filing. For more information, please see [ICP Filing Application Process](https://intl.cloud.tencent.com/document/product/1022/31659).

## Adding a Domain Name
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Distribution and Playback** > **Domain Names** on the left sidebar.
2. Click **Add Domain Name**. In the pop-up dialog box, enter the domain name that has successfully obtained an [ICP filing](https://intl.cloud.tencent.com/document/product/1022/31659) and click **OK**.
![](https://main.qcloudimg.com/raw/37dab10b1d498194b8ac7fbf4f977525.png)
>
>- It takes several minutes to add the domain name. After the domain name is added, you can view its status, CNAME, and domain name type.
>- Up to 18 domain names can be added to a Tencent Cloud account.


## Resolving a Domain Name
After adding a domain name, you need to configure the CNAME in the specific DNS service provider of the domain name, so that users can access your video information through the domain name. 
 <!--
The steps are as follows:
>The following uses Tencent Cloud DNS as the DNS service provider to illustrate how to add a CNAME record. The detailed steps vary by provider. For more information, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/570/11134).

1. Log in to [Domain Name Management Console](https://console.cloud.tencent.com/domain). In **My Domain Names**, find the domain name for which to add a CNAME record, and click **Resolve** in the "Operation" column.
2. Go to the **Record Management** page of the domain name and click **Add Record**.
3. In the pop-up box, set **Record Type** to CNAME, **Host Record** to the domain name prefix (such as www), and **Record Value** to the CNAME domain name, and click **OK**.

> After you add a custom domain name, even if you do not add a video, a small amount of traffic will still be generated, which is normal as a small number of packets will be returned to the domain name.
-->
