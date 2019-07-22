Select **Feature Template** > **Screencapturing and Porn Detection Configuration** in the left sidebar in the LVB Console.
![](https://main.qcloudimg.com/raw/7f92dd18dfe7d82b2e1b6f8dfea61587.png)
The screencapturing interval is generally 10 seconds by default, and its value range is 5 to 300 seconds. When customizing the interval, remember that the value must be a multiple of 5.
![](https://main.qcloudimg.com/raw/6295d6b27b0bd5d04d68a8c6189488d6.png)


>1. The screencapturing feature can be enabled separately, but the porn detection feature can be used only after screencapturing is enabled.
>2. Both screencapturing and porn detection are paid services. Once enabled, screencapturing is charged 0.1 CNY per thousand screenshots, and porn detection is charged at 1.3 CNY per thousand screenshots. For more information, see [Pricing Details](https://intl.cloud.tencent.com/document/product/267/2818#3.2-.E7.9B.B4.E6.92.AD.E6.88.AA.E5.9B.BE.E8.B4.B9.E7.94.A8).  

**Associate a domain name:** After creating a screencapturing and porn detection template, you need to select the corresponding push domain name in **Domain Name Management** and go to **Template Configuration** to specify the screencapturing and porn detection template for the domain name.
![](https://main.qcloudimg.com/raw/db575f7fc574635d27ace6be492fc522.png)


>- If you want to unbind the screencapturing and porn detection configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>[](https://main.qcloudimg.com/raw/2a0f365568a13a050e115034e5570ddf.png)
>- The screencapturing and porn detection templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated a specified stream through the APIs related to screencapturing and porn detection and want to disassociate it, you need to call the [screencapturing template deletion API](https://intl.cloud.tencent.com/document/product/267/30832) to do so.
