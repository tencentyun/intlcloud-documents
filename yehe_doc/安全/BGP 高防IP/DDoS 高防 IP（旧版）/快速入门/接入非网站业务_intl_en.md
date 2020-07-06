
This document describes how to connect non-website applications to Anti-DDoS Advanced instances and verify the forwarding configuration.

## Prerequisites
- To add a forwarding rule, you need to [purchase an Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/15483) first.
- To modify the DNS information of your business domain name, you need to purchase a domain name resolution product first.

## Process
![](https://main.qcloudimg.com/raw/2e1749adb177c75205dbad1535582175.png)

## Directions
<span id="step1"></span> 
### Configuring forwarding rules
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgpip_v2) and select **Anti-DDoS Advanced** > **Access Configuration**.
2. On the **Non-website Scenarios** tab, find and select the target Anti-DDoS Advanced instance and add a forwarding rule.
• Add one single forwarding rule:
	1. Click **Create**.
	![](https://main.qcloudimg.com/raw/d5d3c6bd1b0f1023879135e066776f78.png)
	1. On the **Add forwarding rule** page, configure the following parameters as needed and click **OK**.
![](https://main.qcloudimg.com/raw/849f37ac06a8c3bf9cc53f7e6bb1e154.png)

 - Forwarding Protocol: TCP and UDP are supported currently.
 - Forwarding Port: this is the Anti-DDoS Advanced port used for access. You are recommended to choose the same port as that of the real server.
 > Anti-DDoS Advanced does not support ports 1433, 1434, 3306, 3389, 36000, and 56000. Port 843 is supported in the Guangzhou and Beijing regions.
 - Real Server Port: the real port of your business site.
 - Forwarding Method: **Forwarding via IP** and **Forwarding via domain name** are supported.
 - Load Balancing Method: only weighted round-robin is supported currently.
 - Real Server IP + Weight or Real Server Domain Name: enter the real server IP + weight or real server domain name based on the **forwarding method**. Up to 20 pairs of IP + weight or domain names are supported.
    - If you check **Forwarding via IP**, enter the real server IP address + weight such as 1.1.1.1 50. If a domain name corresponds to multiple pairs of real server IP + weight, you can enter all of them and separate them with carriage return. Up to 20 entries are supported.
     >The weight ranges from 1 to 100.
    - If you check **Forwarding via domain name**, enter the real server domain name. If one domain name corresponds to multiple real server domain names, you can enter all of them and separate them with carriage return. Up to 20 entries are supported.
	
 • Add forwarding rules in batches:
	1. Click **Batch Import**.
![](https://main.qcloudimg.com/raw/066af7814e650a22a64efb7a18307c17.png)
	1. In the rule input box on the batch import page, paste the rules to be imported.
![](https://main.qcloudimg.com/raw/cfd833447e6b64460df1f078545f62f3.png)
>
>- From left to right, paste the forwarding protocol, forwarding port, real server port, real server IP, and weight and separate them with space. Only one forwarding rule can be entered per line.
>- The number of forwarding rule entries added in batches cannot exceed the current quota. Within the quota limit, up to 30 entries can be imported at a time.


<span id="step2"></span> 
### Opening the intermediate IP range

To prevent service unavailability that occurs if the real server blocks Anti-DDoS Advanced's intermediate IP, you are recommended to configure whitelist policies for the real server infrastructure (such as firewall, web application firewall, intrusion protection system (IPS), and traffic management system) and disable the protection features of the host firewall and other security software tools (such as Safedog) or set whitelist policies for them, so that the intermediate IP will not be affected by the security policies of the real server.
You can log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgpip_v2), select **Anti-DDoS Advanced** > **Resource List** on the left sidebar, find the row of the target Anti-DDoS Advanced instance, and click its **ID/Name** to view its detailed intermediate IP range on the **Basic Information** page that pops up.
<span id="step3"></span> 
### Verifying the configuration locally

After the forwarding configuration is completed, the Anti-DDoS Advanced instance will forward messages from the relevant port to the corresponding real server port according to the forwarding rule.
To ensure the stability of your business, a local test is recommended. The verification method is as follows:

- **For applications accessed through IPs**
  For applications accessed through IPs (such as games), run `telnet` to check whether the Anti-DDoS Advanced port is accessible. You can also enter the Anti-DDoS Advanced IP as the server IP in your local client (if possible) to check whether the local client can access it.
  For example, if your Anti-DDoS Advanced IP is 10.1.1.1 with forwarding port 1234, and your real server IP is 10.2.2.2 with port 1234, when you run `telnet` locally to access 10.1.1.1:1234, if the address can be accessed, the forwarding is successful.
- **For applications accessed through domain names**
  For applications accessed through domain names, follow the steps below for verification:
 1. Modify your local `hosts` file to direct local requests to the protected site to your Anti-DDoS Advanced instance.
   Take Windows OS as an example:
   1. Open the `hosts` file (C:\Windows\System32\drivers\etc) and add the following content at the end of file:
   `<Anti-DDoS Advanced IP address> <Domain name of the protected site>`
   For example, if the Anti-DDoS Advanced IP is 10.1.1.1 and the domain name is [www.qq.com](www.qq.com), then add:
   `10.1.1.1       www.qq.com`
   2. Save the `hosts` file.
 2. Run the `ping` command on the protected domain name on your local computer.
   If the resolved IP address is the Anti-DDoS Advanced IP address bound in the `hosts` file, the forwarding is successful.
 >If the resolved IP address is still the real server IP address, try running the `ipconfig/flushdns` command in the Windows Command Prompt to clear the local DNS cache.

  3. After successfully configuring the `hosts`, check whether the domain name can be accessed.
   If yes, the configuration has taken effect.

>If the verification still fails with the correct method, please log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgpip_v2) and check whether the configuration is correct. If the problem persists after you fix any incorrect configuration items, please contact [Tencent Cloud technical support](https://intl.cloud.tencent.com/support).

<span id="step4"></span>
### Modifying the DNS resolution of the business domain name

Before using Anti-DDoS Advanced, you need to configure the A record of your business domain name's DNS with an Anti-DDoS Advanced IP, so that all user access requests to your site will pass through Anti-DDoS Advanced first before arriving at the real server (that is, all traffic will be first directed to Anti-DDoS Advanced before getting to the real server).
