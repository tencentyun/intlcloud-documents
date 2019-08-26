Select **Function Template** > **Screencap & Porn Detection Configuration** in the left sidebar in the LVB Console.
![](https://main.qcloudimg.com/raw/aad94fc28cf8767fb61023c14c7b5754.png)
The screencapturing interval is 10 seconds by default. It can be customized ranging from 5 to 300 seconds. When customizing the interval, remember that the value must be a multiple of 5.
![](https://main.qcloudimg.com/raw/6df1b1fc9864a26b29cac6ae66547934.png)
>!
>1. The screencapturing feature can be enabled alone, but the porn detection feature can be enabled only when screencapturing is enabled.
>2. Both screencapturing and porn detection are paid services. Screencapturing is priced at 0.1 CNY per thousand screenshots, and porn detection at 1.3 CNY per thousand screenshots. For more information, see [Pricing Details](https://cloud.tencent.com/document/product/267/2818#3.2-.E7.9B.B4.E6.92.AD.E6.88.AA.E5.9B.BE.E8.B4.B9.E7.94.A8).  

**Associate the template with a domain name:** After creating a screencapturing and porn detection template, you need to select the corresponding push domain name in **Manage Domain** and go to **Configure Template** to specify the screencapturing and porn detection template for the domain name.
![](https://main.qcloudimg.com/raw/838286bbfe34a44169e6fc1eccbb291c.png)

>?
>- If you want to unbind the screencapturing and porn detection configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
>![](https://main.qcloudimg.com/raw/22d95e62a0750b419b83dc4d49c1cd83.png)
>- The screencapturing and porn detection templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the configuration with a specified stream through the APIs related to screencapturing and porn detection and want to disassociate them, you need to call the [screencapturing template deletion API](https://cloud.tencent.com/document/product/267/32622).
