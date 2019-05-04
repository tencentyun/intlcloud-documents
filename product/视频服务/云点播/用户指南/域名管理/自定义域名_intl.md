## Operation Scenario
After activating Tencent Cloud VOD, the system will assign you a default domain name `xxx.vod2.myqcloud.com`, which will be used by default for all your VOD resources. You can also add and resolve a custom domain name via [VOD Console](https://console.cloud.tencent.com/video/cdnlog).
## Prerequisites
- You have successfully applied for the video service. To do this, see [Purchase Process](https://cloud.tencent.com/document/product/266/2839).
- The domain name to be added has successfully obtained an ICP filing. To do this, see [ICP Filing Application Process](https://cloud.tencent.com/document/product/243/18909).

## Adding a Domain Name
1. Log in to [VOD Console](https://console.cloud.tencent.com/video/cdnlog) and select **Distribution and Playback** > **Domain Name** in the left sidebar.
2. Click **Add Domain Name**.
 ![](https://main.qcloudimg.com/raw/04bf9340b103ab3f6e053e4f26f14374.png)
3. In the pop-up dialog box, enter the domain name that has successfully obtained an [ICP filing](https://cloud.tencent.com/document/product/243/18909) and click **OK**.
It takes a few minutes to add a domain name. Please wait patiently. After the domain name is added, you can view its status, CNAME, and domain type.
>?Up to 18 domain names can be added to a single Tencent Cloud account.
>
 ![](https://main.qcloudimg.com/raw/49fe1f6a8490375bceba65cdbf824613.png)
 
## Resolving a Domain Name
After adding a domain name, you need to configure the CNAME in the specific DNS service provider of the domain name, so that users can access your video information through the domain name.
>?This document uses Tencent Cloud DNS as the DNS service provider to illustrate how to add a CNAME record. The detailed steps vary by provider. For more information, see [CNAME Configuration](https://cloud.tencent.com/document/product/570/11134).

1. Log in to the [Domain Name Management Console](https://console.cloud.tencent.com/domain).
2. In the **My Domain Names** list, find the domain name for which to add a CNAME record, and click **Resolve** in the "Action" column.
 ![](https://main.qcloudimg.com/raw/66826f1e9105e359279b6290a3dcd5d4.png)
2. Go to the **Record Management** page of the domain name and click **Add Record**.
 ![](https://main.qcloudimg.com/raw/53b07e045bddf3d8b8a11ec8d8dced4b.png)
3. In the pop-up box, set **Record Type** to CNAME, **Host Record** to the domain name prefix (such as www), and **Record Value** to the CNAME domain name, and click **OK**.
 ![](https://mc.qcloudimg.com/static/img/1374c7877eca588d8a14779a60b13a1e/add_cname.png)
