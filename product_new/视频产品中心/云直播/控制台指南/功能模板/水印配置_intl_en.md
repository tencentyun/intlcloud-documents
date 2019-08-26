Select **Function Template** > **Watermark Configuration** in the left sidebar in the LVB Console and click "+".
![](https://main.qcloudimg.com/raw/c039e7361af62dcdb5d9d8383c37dc7d.png)
Set basic information of the watermark.
![](https://main.qcloudimg.com/raw/74c50b5f485ea035c4ef813670aead2a.png)
The position of the watermark can be customized by adjusting the directions of the x axis and y axis (the watermark in the figure below is located in the top-left corner).
![](https://main.qcloudimg.com/raw/a913d44121b4ef79e9e21386b19d663a.png)
>! For optimal visual effects, the watermark should be a transparent image in .png format of less than 2 MB in size.

## Associating the Template with a Domain Name
In **Manage Domain**, select a push address and click **Manage**.
![](https://main.qcloudimg.com/raw/d64d2bd0e3db81e1287d1117bb037739.png)
Select **Configure Template** and then select the configured watermarking template in **Watermark Configuration** to specify it for the domain name.
![](https://main.qcloudimg.com/raw/2bf70042782fd2386a1cfc13bf8a9c6c.png)
>?
>- If you want to unbind the watermark configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
>![](https://main.qcloudimg.com/raw/22d95e62a0750b419b83dc4d49c1cd83.png)
>- The watermarking templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the configuration with a specified stream through the watermark management API and want to disassociate them, you need to call the [watermark deletion API](https://cloud.tencent.com/document/product/267/30153).
