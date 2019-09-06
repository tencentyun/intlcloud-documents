Select **Function Template** > **Callback Configuration** in the left sidebar in the LVB Console and click "+" to create a callback template.
![](https://main.qcloudimg.com/raw/231fc027c73d4629f5bc04fafdfb895f.png)
Enter the callback information in the callback settings pop-up window and click **Save**.
![](https://main.qcloudimg.com/raw/870c6dd664a4eb618bdc1a7fcdf922dc.png)
>The **Callback key** is a user-defined string of up to 32 characters consisting of uppercase and lowercase letters and numbers. 

**Associate the template with a domain name**
After creating a callback template, you need to select the corresponding push domain name in **Manage Domain** and go to **Configure Template** to specify the callback template for the domain name.
![](https://main.qcloudimg.com/raw/738f2e274ee988b7237c627972826cef.png)


>- If you want to unbind the callback configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
>![](https://main.qcloudimg.com/raw/3d65aea44b2711b80e1250a1b2bfc8cc.png)
>- The callback templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the callback configuration with a specified stream through the APIs related to callback and want to disassociate them, you need to call the [callback template deletion API](https://intl.cloud.tencent.com/document/product/267/30813).
