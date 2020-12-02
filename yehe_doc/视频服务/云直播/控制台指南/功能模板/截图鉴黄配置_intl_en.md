This document describes how to create a [screencapturing and porn detection configuration](https://intl.cloud.tencent.com/document/product/267/31063) in the [LVB Console](https://console.cloud.tencent.com/live). After the configuration is successfully created, you need to associate it with the corresponding push domain name. The association will take effect in about 5–10 minutes. You can also create screencapturing templates for live channels through APIs. 


## Creating Screencapturing Template
Log in to the LVB Console, select **Feature Template** > **[Screencapture and porn detection configuration](https://console.cloud.tencent.com/live/config/jtjh)** on the left sidebar, click **+**, enter the configuration information, and click **Save**.
The screencapturing interval is generally 10 seconds by default, and its value range is between 5 and 300 seconds. When customizing the interval, remember that the value must be a multiple of 5.

![](https://main.qcloudimg.com/raw/30b549740abdf77f002fba3069737e52.png)

>
>1. The screencapturing feature can be enabled separately, but the porn detection feature can be used only after screencapturing is enabled.
>2. Both screencapturing and porn detection are paid services. Once enabled, screencapturing is charged at 0.0176 USD per thousand screenshots, and porn detection is charged at 0.2294 USD per thousand screenshots. 
>3. The generated screenshots are stored in your COS bucket and will incur COS storage fee. For more information, please see [COS Pricing](https://intl.cloud.tencent.com/document/product/436/6239).
>4. To enable the screencapturing feature, you must first grant LVB the permission to write to your COS bucket. 

## Associating a Domain Name
After creating a screencapturing and porn detection template, you need to select the corresponding push domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** or click **Manage** on the right to enter the domain name details page. Then, select **Template Configuration** to specify the screencapturing and porn detection template for the domain name.
![](https://main.qcloudimg.com/raw/680a7ca00df99cb79de9dd937554aa5c.png)
>
>- If you want to unbind the screencapturing and porn detection configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>- The screencapturing and porn detection templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated a specified stream through the APIs related to screencapturing and porn detection and want to disassociate it, you need to call the [screencapturing template deletion API](https://intl.cloud.tencent.com/document/product/267/30832) to do so.






