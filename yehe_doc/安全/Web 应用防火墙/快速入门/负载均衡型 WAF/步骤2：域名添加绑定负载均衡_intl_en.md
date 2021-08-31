1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/config) and select **Web Application Firewall** > **Protection Settings** on the left sidebar to enter the protection settings page.
2. On the protection settings page, click **CLB WAF** to enter the CLB WAF protection settings page. In the domain name list, click **Add Domain Name** to enter the domain name adding page.
3. On the domain name adding page, enter the domain name to be protected; then, click **Next** to enter the listener selection page.
>!The entered domain name must be the same as that added in the CLB listener configuration.

4. On the listener selection page, select the CLB instance and listener configured in [Step 1. Confirm CLB Configuration]() to complete binding.
5. After the binding is completed, click **Complete** below to return to the domain name list, where you can view the protected domain name `wow.qcloudwaf.com` and the ID, name, VIP, and listener information of the CLB instance.
