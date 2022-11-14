## What is a network honeypot?
A network honeypot is a network-attached system that simulates businesses. Network honeypots expose probes in your network. When an attacker probes a honeypot, the attacker's information and attack method are traced and recorded, which can help you counter the attack. In prioritized protection scenarios, honeypots buy you time to protect businesses.

The Cloud Firewall honeypot service is deployed in Tencent Cloud's honeynet, and does not occupy your network space. The honeypots are isolated from each other as they are deployed in different VPCs. Thus, attackers will not gain lateral movement. Honeypot probes are deployed in your network based on an IP or domain name. Traffic of the specified ports/paths will be forwarded to different honeypot services so as to **trap** attackers.

## Features and principles
The Cloud Firewall honeypot service has three main features as follows:
- Lures attackers with highly realistic simulations.
- Collects attacker information to help you counter attacks.
- Delays attackers and secures time to protect networks.

Increase your business security by setting more probes, which require little network resources. Using the highly realistic fake services in the honeynet, you can **deceive** attackers.


## Checking the overview
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw) and click **Network Honeypots** in the left navigation pane.
2. On the **Network honeypot** page, the overview will be displayed in the upper left corner, and you can quickly check the number of honeypot services, probes, hit honeypots, scanned probes, attacker IPs, and scanned IPs.
![](https://qcloudimg.tencent-cloud.cn/raw/ecb02c5163b625c91c19fc1bffc5b5c5.png)
3. In the overview, click **View alerts** to go to the **Honeypot events** page, or click **View logs** to go to the **Honeypots** page of the intrusion defense logs.
![](https://qcloudimg.tencent-cloud.cn/raw/e5f4837da134a9fde5f4f3fba99700f7.png)


## Viewing the honeypot policy map
The honeypot policy map includes a policy list and a policy view, which take the form of a table and a path chart, respectively. It shows the different paths, honeypot service types, and bait types corresponding to different probe addresses.
#### Policy list
The policy list shows the honeypot information corresponding to different probe addresses in detail.
![](https://qcloudimg.tencent-cloud.cn/raw/0fb117622946efe475decd028b4a3624.png)

#### Policy view
- The policy view intuitively displays the honeypot information corresponding to different probe addresses in different regions.
![](https://qcloudimg.tencent-cloud.cn/raw/247104e5989b0932519b88c8bdf1c037.png)
- You can query specific probe addresses in the view by honeypot filter conditions. For example, you can hover the mouse cursor over **①Probe address** and **②Honeypot service** to find the corresponding probe and bait of the honeypot. You can select the checkbox for any condition on this page to find the corresponding service and visualize the information.
![](https://qcloudimg.tencent-cloud.cn/raw/a1fd4fd9663eec310609ee86697af3da.png)
