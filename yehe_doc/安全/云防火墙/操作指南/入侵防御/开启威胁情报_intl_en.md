After threat intelligence is enabled, CFW feeds network perimeter traffic to the threat intelligence detection and analysis engine to identify unknown risks beyond access control rules. Prioritized protection packages are also available to enhance risk resistance capabilities in prioritized protection scenarios.

## Directions
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ips) and click **Intrusion Protection System** in the left navigation pane.
2. On the **Intrusion protection system** page, click ![](https://qcloudimg.tencent-cloud.cn/raw/0b2fd6e67aa8a17206b6f6cf25d9c75a.png) next to **Threat intelligence** to enable this feature.
>- Only when threat intelligence and [edge firewall](https://console.cloud.tencent.com/cfw/switch/internet) are both enabled for a public IP address, CFW monitors and analyzes the north-south traffic on this IP address based on the threat intelligence.

![](https://qcloudimg.tencent-cloud.cn/raw/6fc232e64a4d6f4f2476ac5ab0f9e100.png)
3. After threat intelligence is enabled, CFW feeds network perimeter traffic to the threat intelligence detection and analysis engine to identify unknown risks beyond access control rules:
	- Malicious incoming access: CFW detects malicious scanning, brute-force attacks, and remote control from malicious IP addresses to cloud assets, as well as mining Trojans, ransomware, and other threat samples.
	- Outgoing access: CFW detects outgoing access from cloud assets to external malicious IP addresses or domain names, and identifies potential server compromise risks through the comparative analysis of big data provided by threat intelligence.

## More Information
For questions about intrusion defense, please see [Intrusion Protection System](https://intl.cloud.tencent.com/document/product/1160/49835).