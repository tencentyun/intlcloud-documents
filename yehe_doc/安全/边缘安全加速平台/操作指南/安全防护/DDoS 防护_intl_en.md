This document describes the DDoS mitigation level, IP blocklist/allowlist, regional blocking, and protocol blocking features of DDoS mitigation as well as their configurations.
>?DDoS mitigation features and their configurations may be different depending on the EdgeOne plan you purchase.

## Prerequisites
You have [purchased](https://intl.cloud.tencent.com/document/product/1145/48705) the EdgeOne Enterprise plan and [connected your site](https://intl.cloud.tencent.com/document/product/1145/45966) to EdgeOne or [accessed the layer-4 proxy](https://intl.cloud.tencent.com/document/product/1145/46194).

## DDoS Mitigation Level
EdgeOne provides different DDoS mitigation levels in different scenarios. This document describes how to configure the DDoS mitigation level in the console.


### Use cases
EdgeOne allows you to adjust mitigation policies and provides three mitigation levels against DDoS attacks. The mitigation operations at each level are described below:

| Protection Level | Protection Action                                                     | Description                                                         |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Loose     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li> | <li>This cleansing policy is loose and only defends against explicit attack packets.</li><li>We recommend choosing this protection level when normal requests are blocked. Complex attack packets may pass through the security system.</li> |
| Medium     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li><li>Filters common UDP-based attack packets.</li><li>Actively verifies the source IPs of some access attempts.</li> | <li>This cleansing policy is suitable for most businesses and capable of defending against common attacks.</li><li>The level Medium is chosen by default.</li> |
| Strict     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Strictly checks and filters UDP data packets with explicit attack attributes and UDP-based attack packets.</li><li>Actively verifies the source IPs of some access attempts.</li><li>Filters ICMP attack packets.</li> | This cleansing policy provides strict traffic cleansing. We recommend choosing this level when attack packets pass through the security system in **Medium** mode.         |

>?
>- If you want to protect your business from massive attacks or use UDP for your business, [contact us](https://intl.cloud.tencent.com/contact-us) to customize a policy that can ensure business continuity in **Strict** mode.
>- By default, the purchased EdgeOne Enterprise plan uses the **Medium** mitigation level. You can adjust the level based on your actual business conditions.
>- By default, the purchased EdgeOne Standard plan uses the **Medium** mitigation level.


### Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **DDoS Mitigation** on the left sidebar.
2. On the left of the **DDoS mitigation** page, select a mitigation business object, such as a **DDoS mitigation Enterprise plan** or **DDoS mitigation Enterprise plan - L4 proxy** instance.
![](https://qcloudimg.tencent-cloud.cn/raw/c0a6eed4c3425ea285b3d296e5ee6a05.png)
3. In the **DDoS mitigation level** section, the **Medium** mitigation level is applied to your sites in EdgeOne by default when DDoS mitigation is enabled. You can adjust the level based on your actual business needs.
![](https://qcloudimg.tencent-cloud.cn/raw/fbe8f793333d8bd6264d1cfe9f382275.png)


## IP Blocklist/Allowlist
EdgeOne enables you to configure the IP blocklist and allowlist to control access to EdgeOne sites and block or allow access requests based on the client source IP.
>? The IP blocklist/allowlist rules take effect in 5 to 10 seconds after being saved.
>- The access requests from the IPs on the allowlist will not be filtered by any DDoS mitigation policy.
>- The access requests from the IPs on the blocklist will be discarded directly.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **DDoS Mitigation** on the left sidebar.
2. On the left of the **DDoS mitigation** page, select a mitigation business object, such as a **DDoS mitigation Enterprise plan** or **DDoS mitigation Enterprise plan - L4 proxy** instance.
![](https://qcloudimg.tencent-cloud.cn/raw/cb03113aaf23a11c95d58abd73fbb79f.png)
3. Click **Set** in the "IP blocklist/allowlist" section.
![](https://qcloudimg.tencent-cloud.cn/raw/e7529d2fea115fc61402a2e7a21e9c46.png)
4. On the **IP blocklist/allowlist** page, click **Create** to create a rule, enter the target IP, select **Blocklist** or **Allowlist** for the type, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/b2aeaffa7a3ba49d3c7e5cf9a564665c.png)
6. (Optional) After the rule is created, it is added to the rule list. To delete it, click **Delete** in the "Operation" column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/2fd20196deb21eb3b44de05c48d885db.png)


## Regional Blocking
EdgeOne enables you to prevent client IPs in specific regions from accessing your site. It can block traffic from multiple regions/countries.
>?After you configure the regional blocking setting, attack traffic targeting the region will still be recorded but will not be allowed to your real server.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **DDoS Mitigation** on the left sidebar.
2. On the left of the **DDoS mitigation** page, select a mitigation business object, such as a **DDoS mitigation Enterprise plan** or **DDoS mitigation Enterprise plan - L4 proxy** instance.
![](https://qcloudimg.tencent-cloud.cn/raw/4c1a18fce71a8c0e476a5f7a215603fb.png)
3. Click **Set** in the "Regional blocking" section.
![](https://qcloudimg.tencent-cloud.cn/raw/8cbec0bbc75da0a5917d75ded9257eca.png)
4. On the regional blocking page, click **Create**.
5. In the **Create regional blocking policy** pop-up window, select the target region and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/e92efeddba9852eddb4fabf4a5b70097.png)
6. (Optional) After the rule is created, it is added to the list. To modify the list of blocked regions, click **Configure** in the "Operation" column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/05a61a7dc3d0fe2225f5315e658fd3e9.png)

## Port Filtering

Port filtering is a more fine-grained way to restrict client access traffic to your sites in EdgeOne. After it is enabled, you can create a rule by setting the protocol type, source port range, destination port range, and action (**Discard** or **Continue protection**).

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **DDoS Mitigation** on the left sidebar.
2. On the left of the **DDoS mitigation** page, select a mitigation business object, such as a **DDoS mitigation Enterprise plan** or **DDoS mitigation Enterprise plan - L4 proxy** instance.
![](https://qcloudimg.tencent-cloud.cn/raw/075f32b046ef6b723e879176eedc40b9.png)
3. Click **Set** in the **Port filtering** section.
![](https://qcloudimg.tencent-cloud.cn/raw/60963e3373ddec51e672044b61b6bf1d.png)
4. On the page that appears, click **Create** to create a rule. Select an action, enter the required fields, and click **Save**.
>?
>- Multiple instances can be created at a time. For instances without protected resources, you cannot create rules.
>- For **Priority**, enter an integer between 1 and 1000. A rule with a lower number has higher priority and is listed higher. Default: 10.

![](https://qcloudimg.tencent-cloud.cn/raw/6d3e7f363891dca41da7ff2a89e86ae2.png)
6. (Optional) After the rule is created, it is added to the rule list. To modify it, click **Configure** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/e0021e07c52c56f45d2f1e2d35b1ced7.png)

## Feature Filtering
A feature filtering rule allows you to define a number of conditions based on IP, TCP, and UDP headers, payload, source port, destination port, and action (**Discard**, **Allow**, **Discard and block**, or **Continue protection**). After feature filtering is enabled, you can create mitigation rules targeting those specific features.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **DDoS Mitigation** on the left sidebar.
2. On the left of the **DDoS mitigation** page, select a mitigation business object, such as a **DDoS mitigation Enterprise plan** or **DDoS mitigation Enterprise plan - L4 proxy** instance.
![](https://qcloudimg.tencent-cloud.cn/raw/a53ab5c87e42aeb8f4c84d119f7c4a30.png)
3. Click **Set** in the "Feature filtering" section.
![](https://qcloudimg.tencent-cloud.cn/raw/71417e41054e15dc88ed797bd6ace249.png)
4. On the feature filtering page, click **Create**.
5. In the **Create feature filtering policy** pop-up window, select an action, enter the required fields, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/d6d1c0ebe6732904651b6ec615d4808e.png)
6. (Optional) After the rule is created, it is added to the list. To modify it, click **Configure** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/68fd8c9f7e28a575f0ddf897280fd131.png)

## Protocol Blocking
EdgeOne supports blocking inbound traffic based on its protocol type. You can enable **ICMP protocol blocking**, **TCP protocol blocking**, **UDP protocol blocking**, and blocking of other protocols to block their access requests directly. Note that UDP is a connectionless protocol that doesn't provide a three-way handshake process like TCP and thus has security vulnerabilities. We recommend you block UDP if it is not used for your business.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **DDoS Mitigation** on the left sidebar.
2. On the left of the **DDoS mitigation** page, select a mitigation business object, such as a **DDoS mitigation Enterprise plan** or **DDoS mitigation Enterprise plan - L4 proxy** instance.
![](https://qcloudimg.tencent-cloud.cn/raw/66e66d073a66a9332a03977a62e90694.png)
3. Click **Set** in the "Protocol blocking" section.
![](https://qcloudimg.tencent-cloud.cn/raw/edadfe2d6d2662e78e845d456e48b45d.png)
4. On the **Protocol blocking** page, toggle on the target protocol ![](https://qcloudimg.tencent-cloud.cn/raw/0e86da85c0afc62ad707cf59f1442d6b.png).
![](https://qcloudimg.tencent-cloud.cn/raw/1d8457083b163985f50e8e8929ec7cef.png)

## Connection Attack Protection
EdgeOne can provide protection against connection attacks. With **Maximum source IP exceptional connections** enabled, a source IP detected that frequently sends a high number of abnormal connection requests in a short time will be added to the blocklist and be blocked for 15 minutes.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and select **Security** > **DDoS Mitigation** on the left sidebar.
2. On the left of the **DDoS mitigation** page, select a mitigation business object, such as a **DDoS mitigation Enterprise plan** or **DDoS mitigation Enterprise plan - L4 proxy** instance.
![](https://qcloudimg.tencent-cloud.cn/raw/4396712ec21168045dbeda6bdcc0448c.png)
3. Click **Set** in the **Connection attack protection** section to enter the configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/bbdd0e66bfd561d3614c35f4a7b56cd3.png)
4. On the **Connection attack protection** page, click **Configure**.
5. In the **Configure connection attack protection** pop-up window, enable **Exceptional connection protection** and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/74112df3401d38a43ea5943d27a206c5.png)
6. (Optional) After the rule is created, it is added to the list. To modify the configuration, click **Configure** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/291584edc4d33b3ef7a9dbb4a0b4bf6d.png)
