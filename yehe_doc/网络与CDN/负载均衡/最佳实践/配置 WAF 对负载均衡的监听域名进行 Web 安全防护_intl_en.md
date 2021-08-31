By binding domain names with CLB listeners, [CLB Web Application Firewall (WAF)](https://intl.cloud.tencent.com/document/product/627/17470) can detect and block the HTTP or HTTPS traffic passing through CLB listeners. This document introduces how to use CLB WAF to apply Web security protection for the domain names added to CLB.

## Prerequisites
- CLB WAF is currently in beta, if you want to try it out, please Submit an Application.
- You have successfully created an HTTP or HTTPS listener, and the domain name can be accessed. For more information, please see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975).
- You have successfully purchased the CLB WAF service. For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/627/11730).

## Limits
Currently, only IPv4 CLB instances support CLB WAF protection, this feature is not available for IPv6 and NAT64.

## Directions
<span id ="step1"></span>
### Step 1: Confirm the CLB domain name configuration
This document takes the domain name `www.example.com` as an example.
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb), click **CLB Instance List** on the left sidebar to enter the **Instance Management** page.
2. Select the instance region and then click **Configure Listener** on the right of the target instance.
3. Select the **Listener Management** tab, in the **HTTP/HTTPS Listener** section, click the **+** icon on the left of the target listener to see the domain name details.
![](https://main.qcloudimg.com/raw/1d546d69bc1d88faf15ef7acc9270468.png)
4. Check the CLB domain name configuration to match the following: CLB instance ID: `lb-f8lm****`; listener name: `http-test`; domain name: `www.example.com`; domain name protection status: **Not Enabled** (the ID, name, and domain name are subject to actual cases).

### Step 2: Add a domain name in the WAF console and bind it to a CLB instance
To apply protection to a domain name with the CLB WAF service, you need to add a CLB-listening domain name in WAF and bind it with a CLB listener.
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/config), and select **Web Application Firewall** -> **Defense Settings** on the left sidebar.
2. Select the **CLB** tab.
3. Click **Add Domains**.
![](https://main.qcloudimg.com/raw/5dc4d9c0363a2fe2713f157606efce19.png)
4. Enter the domain name, and click **Next**.
![](https://main.qcloudimg.com/raw/fadb7336503e5ee808fe8a02d9b12005.png)
5. Select your CLB region, then the domain name in the <a href="#step1">"Step 1: Confirm the CLB domain name configuration"</a>, and click **Select a Listener**.
![](https://main.qcloudimg.com/raw/4b632c6769bbbe105027e8bdf0b3ba1a.png)
6. In the pop-up window, select the CLB listener in the <a href="#step1">"Step 1: Confirm the CLB domain name configuration"</a>, and then click **OK**.
![](https://main.qcloudimg.com/raw/2793320edb9a79b0c46e4ea4e92e38f6.png)
7. Click **Finish** in the **Select a Listener** step to finish binding a domain name with CLB listener in WAF.
8. Back to the **Domain List** page, check the domain name, region, bound CLB instance ID, listener, and other information.

### Step 3: Verify the result
1. Follow the directions in <a href="#step1">"Step 1: Confirm the CLB domain name configuration"</a> to check the domain name. The domain name protection is enabled if the domain name protection is **Enabled** and the traffic mode is **Mirror**.
 -  If you have not configured DNS resolution for your domain name, please see [Step 2. Perform Local Testing](https://intl.cloud.tencent.com/document/product/627/35652) to verify if the WAF protection is enabled.
 - If you have configured DNS resolution for your domain name, please follow the directions below to verify if the WAF protection is enabled.
1. Visit `http://www.example.com/?test=alert(123)` via a browser.
2. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/waf/config), and then select **Log Services** -> **Attack Log** on the left sidebar.
3. Select the **Log Search** tab, select the added protection domain name `www.example.com`, and then click **Search**. WAF protection for the domain name configured in CLB is effective if there are **XSS Attack** logs in the log list.

