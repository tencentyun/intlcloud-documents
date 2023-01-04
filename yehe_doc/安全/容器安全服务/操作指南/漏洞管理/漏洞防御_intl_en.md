Exploit prevention is a virtual patch-based system developed by the Tencent Cloud security team to defend against frequent 0-day and N-day vulnerabilities. It integrates Tencent's vulnerability mining and real-time high-risk vulnerability alerting technologies to capture and analyze vulnerabilities, generate virtual patches based on Tencent's expertise, and automatically make the patches effective in CVM instances. This helps effectively block hacker attacks and gain more time for vulnerability fix.

### Enabling exploit prevention
Enable the exploit prevention feature to block vulnerability exploitation in real time and protect your business from attacks.
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and select **Vulnerability Detection** on the left sidebar.
1. On the **Vulnerability Detection** page, toggle on the **Enable now** switch ![](https://qcloudimg.tencent-cloud.cn/raw/a35c368f36c94c26e23e636639ef99bb.png). The drawer on the right will display the configuration page for exploit prevention.
![](https://qcloudimg.tencent-cloud.cn/raw/316ffb6e9d29f12801bd7d39aae0de09.png)
2. On the **Vulnerability Detection** page, click **Vulnerability detection** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/3fdfe3439f63d5005ccfe66bb53661c1.png)
3. On the **Vulnerability detection** page, click the number of prevented vulnerabilities to view the details.
![](https://qcloudimg.tencent-cloud.cn/raw/b93ca544962ea477c7410e768a5684c7.png)
4. On the **Vulnerability detection** page, select **Protected nodes**, click **Implement now** at the bottom of the drawer, and wait for the policy to be distributed. Then, the selected nodes are protected against container vulnerability exploitation.
>? If you select **All servers** for **Protected nodes**, exploit prevention will be automatically enabled for newly added servers.

![](https://qcloudimg.tencent-cloud.cn/raw/38ff2e785d8cc085f7964fbd348598b7.png)
5. On the **Vulnerability Detection** page, click **Protection settings** to view or adjust the status of the exploit prevention switch, adjust the scope of protected nodes, and view the status of the prevention plugin on the node.
![](https://qcloudimg.tencent-cloud.cn/raw/e5b8986cc3ebb4fe90d40cde60c9481d.png)

### Viewing prevented vulnerabilities
1. After exploit prevention is enabled, you can filter vulnerabilities in the **Defending** status on the emergency vulnerabilities, system vulnerabilities, and application vulnerabilities pages to view the details.
![](https://qcloudimg.tencent-cloud.cn/raw/6e9803faf139d615667219ce51e5a755.png)
2. Hover over the **Defending** icon to quickly view the numbers of protected nodes and defended attacks. In addition, you can click **Protection settings** to enter the prevention settings drawer and click **Prevented attacks** to enter the vulnerability attack event page.
>? If exploit prevention is not enabled, you can filter vulnerabilities in the **Undefended** status on the emergency vulnerabilities, system vulnerabilities, and application vulnerabilities pages to view the details.

![](https://qcloudimg.tencent-cloud.cn/raw/83ba0f051ecdb61f704e1e6bb2076cc5.png)

### Vulnerability attack event
1. On the **Vulnerability Detection** page, click **Vulnerability attack event** to view attacks that have been successfully defended against.
![](https://qcloudimg.tencent-cloud.cn/raw/6c90d1857068a37203ed9ed277aad515.png)
2. Click **View details** to view the attack IP, attack packet, and prevention plugin information. You can also click **Image details** to view the vulnerability details. We recommend you block attack IPs and fix vulnerabilities in business images.
![](https://qcloudimg.tencent-cloud.cn/raw/6ef7288236a3fe57b88f4ee3e33b29e8.png)
