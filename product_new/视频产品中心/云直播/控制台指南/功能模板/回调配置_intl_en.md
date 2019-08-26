Select **Function Template** > **Callback Configuration** in the left sidebar in the LVB Console and click "+" to create a callback template.
![](https://main.qcloudimg.com/raw/f750e5a36976d0e2b0995ea1c681e471.png)
Enter the callback information in the callback settings pop-up window and click **Save**.
![](https://main.qcloudimg.com/raw/d31e9dcabf17fd394b56207c0d9d557a.png)
>? The **Callback key** is a user-defined string of up to 32 characters consisting of uppercase and lowercase letters and numbers. For more information on how to use the callback key, see [Instructions on Parameters in Event Notification](https://cloud.tencent.com/document/product/267/32744#.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF.E9.80.9A.E7.9F.A5.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E).

**Associate the template with a domain name**
After creating a callback template, you need to select the corresponding push domain name in **Manage Domain** and go to **Configure Template** to specify the callback template for the domain name.
![](https://main.qcloudimg.com/raw/bf61f5ac138d45ceb837ad9bf4e7e591.png)

>?
>- If you want to unbind the callback configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
>![](https://main.qcloudimg.com/raw/e853c0aa663e95d62cf9515f814fb8db.png)
>- The callback templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated the callback configuration with a specified stream through the APIs related to callback and want to disassociate them, you need to call the [callback template deletion API](https://cloud.tencent.com/document/product/267/32635).
