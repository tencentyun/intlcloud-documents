Select **Feature Template** > **Watermark Configuration** in the left sidebar in the LVB Console and click "+".
![](https://main.qcloudimg.com/raw/573023a1d1d6fd921209799edbfa96e8.png)
Set basic information of the watermark.
![](https://main.qcloudimg.com/raw/f68fdfc704d8a706ccfef73a8d2a23be.png)
The display position of the watermark can be customized by adjusting the directions of the x axis and y axis (the watermark in the figure below is located in the top-left corner).
![](https://main.qcloudimg.com/raw/2fa0ba9edb3bbaec3615efc0ea063e59.png)

>For optimal visual effects, the watermark should be a transparent image in .png format of less than 2 MB in size.

## Binding a Domain Name
In **Domain Name Management**, select a push address and click **Manage**.
![](https://main.qcloudimg.com/raw/1986257b72420a985186648cbf96795a.png)
Select **Template Configuration** and then select the configured watermarking template in **Watermark Configuration** to specify it for the domain name.
![](https://main.qcloudimg.com/raw/637ec4e2692c9b1fdd06ccf336e439d8.png)


>- If you want to unbind the watermark configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>[](https://main.qcloudimg.com/raw/bcd339ff01bd8f5108638a30d5a5f0c1.png)
>- The watermarking templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated a specified stream through the watermark management API and want to disassociate it, you need to call the [watermark deletion API](https://intl.cloud.tencent.com/document/product/267/30824) to do so.

