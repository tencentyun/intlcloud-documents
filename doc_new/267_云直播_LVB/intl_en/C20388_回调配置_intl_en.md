Select **Feature Template** > **Callback Configuration** in the left sidebar in the LVB Console and click "+" to create a callback template.
![](https://main.qcloudimg.com/raw/231fc027c73d4629f5bc04fafdfb895f.png)
Enter the callback information in the callback settings pop-up window and click **Save**.
![](https://main.qcloudimg.com/raw/870c6dd664a4eb618bdc1a7fcdf922dc.png)

> The **Callback key** is a user-defined string of up to 32 uppercase and lowercase letters and numbers. For more information about how to use the callback key, see Event Message Notification Parameter Description.

**Associate a domain name**
After creating a callback template, you need to select the corresponding push domain name in **Domain Name Management** and go to **Template Configuration** to specify the callback template for the domain name.
![](https://main.qcloudimg.com/raw/738f2e274ee988b7237c627972826cef.png)


>- If you want to unbind the callback configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>[](https://main.qcloudimg.com/raw/3d65aea44b2711b80e1250a1b2bfc8cc.png)
>- The callback templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated a specified stream through the APIs related to callback and want to disassociate it, you need to call the [callback template deletion API](https://intl.cloud.tencent.com/document/product/267/30813) to do so.
