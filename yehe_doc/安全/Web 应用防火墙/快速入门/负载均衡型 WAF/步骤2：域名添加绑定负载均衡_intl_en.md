This document describes how to bind a domain name to a CLB instance in the WAF console.
## Directions

1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) and select **Instance Management** -> **Instance List** -> **CLB WAF**on the left sidebar to enter the protection settings page.
2. On the protection settings page, select an instance for the domain name, and click **Domain Name Connection** to enter the domain name connection page.
![](https://main.qcloudimg.com/raw/bb237d6a08bb25c4b25c1cde17145598.png)
3. In the domain name list, click **Add Domain Name** to enter a domain name you want to protect; click **Next** to enter the listener selection page.
>!The entered domain name must be the same as that added in the CLB listener configuration.
>
![](https://main.qcloudimg.com/raw/868d3f6f9cdae3f08147cf88c7f2b0fa.png)
4. On the listener selection page, select the CLB instance and listener configured in [Step 1. Confirm CLB Configuration] to complete binding.
![](https://main.qcloudimg.com/raw/27b2fe447eee3f72f0fbd2ade23726ca.png)
5. After the binding is completed, click **Complete** below to return to the domain name list, where you can view the protected domain name `wow.qcloudwaf.com`, and the ID, name, VIP and listener information of the CLB instance.
![](https://main.qcloudimg.com/raw/a6d7c75770afc3e66667e2de7c7cb2c2.png)
## Subsequent Operations
After completing the binding , you can proceed to [Step 3. Verifying the Configuration](https://intl.cloud.tencent.com/document/product/627/34721).
