[//]: # (chinagitpath:XXXXX)

This document describes how users can connect non-website businesses to Anti-DDoS Advanced instances and verify protection configuration.

## Prerequisites

- To add a forwarding rule, you need to **purchase an Anti-DDoS Advanced instance**.
- To modify the DNS information of your business domain name, you need to purchase the **domain name resolution product**.

## Procedure

![](https://main.qcloudimg.com/raw/26be97a1509c1947df6837ca6dce7597.png)

## Steps
<span id="step1"></span> 
### Configuring the forwarding rule

   1. Log in to the [Anti-DDoS Advanced console](https://console.cloud.tencent.com/dayu/bgpip), find the target instance and click the instance ID to enter the configuration page.
   2. In the **Forwarding Rules** configuration bar, click **New** to create a forwarding rule.

   ![](https://main.qcloudimg.com/raw/80dda47083ae23cd814bf45788aa8617.png)
    
  3. Configure the following parameters as needed and then click **OK**.

 - Forwarding protocol: TCP and UDP are supported.
 - Forwarding port: A protective IP port for access. It is recommended to select the same port as that of the real server. Anti-DDoS Advanced does not support using 843, 1433, 1434, 3306, 3389, 36000 and 56000 ports as the forwarding port.
 - Real server port: The real port of customer website.
 - Real server IP: Enter the IP address of the real server. If there are multiple real server IPs, you can enter all of them and separate them by pressing Enter. A maximum of 20 IPs are supported. The protective IP uses the polling-based load balancing algorithm to forward business traffic.
 
 ![](https://main.qcloudimg.com/raw/7aee6b44bcbb34e262f17ff7bedda5cf.png)

<span id="step2"></span> 
### Open the intermediate IP range

To avoid business interruption caused by Anti-DDoS Advanced's intermediate IP being blocked by the real server, it is suggested to set whitelist policies on the hardware devices of the real server including firewall, Web Application Firewall, intrusion protection system (IPS) and traffic management, and disable the protection feature of the host firewall and any other security software (such as Safedog) or set whitelist policies, so that the intermediate IP will not be affected by the security policies of the real server.
For details about the intermediate IP range of Anti-DDoS Advanced, contact Tencent Cloud support team.

<span id="step3"></span> 
### Local verification configuration

After forwarding configuration is completed, the protective IP of the Anti-DDoS Advanced instance will forward the messages of relevant port to the corresponding port of the real server according to the forwarding rule.
To ensure the stability of your business, a local test is recommended. The verification methods are as follows:

- **For applications accessed via IPs**
  For applications accessed via IPs (such as games), run `telnet` to check whether the protective IP port is accessible. You can also enter the protective IP as the server IP in your local client (if available) to check whether the local client can access the protective IP.
  For example, the protective IP is 10.1.1.1 with port 1234. And the real server IP is 10.2.2.2 with port 1234. Run `telnet` on your local to connect to 10.1.1.1:1234. If the address can be accessed, it means that the forwarding is successful.
- **For applications accessed via domain names**
  For applications accessed via domain names, please try the followings:
 1. Modify your local hosts file to direct local requests to the protected website to the protective IP.
   Take Windows operating system as an example:
   1. Open the hosts file (C:\Windows\System32\drivers\etc), and add the following content at the end of the text:
   `<Protective IP address> <Domain name of the protected website>`
   For example, if the protective IP is 10.1.1.1 and the domain name is [www.qq.com](www.qq.com), add:
   `10.1.1.1       www.qq.com`
   2. Save the hosts file.
 2. Run the `ping` command on the protected domain name on the local computer.
   If the resolved IP address is the protective IP address bound in the hosts file, the forwarding is successful.
 > ? If the resolved IP address is still the real server IP address, try running the `ipconfig/flushdns` command in the Windows Command Prompt to clear the local DNS cache.

  3. After successful configuration of hosts, check whether the domain domain name can be accessed.
   If yes, the configuration has taken effect.

> ? If verification fails, log in to the [Anti-DDoS Advanced console](https://console.cloud.tencent.com/dayu/bgpip) to check the configuration. If the issue persists, contact Tencent Cloud support team.

<span id="step4"></span>
### Modify the DNS resolution of the business domain name

  After binding the forwarding rule group for Anti-DDoS Advanced, you can verify the connectivity from the forwarding port of Anti-DDoS Advanced to the real server port of the real server. Set the business IP to point to Anti-DDoS Advanced, and the access configuration is completed.
  
  If your business uses the DNS resolution service, you can modify the domain name resolution in DNS service provider and change the original business IP address to the bound protective IP address.
  
  Modify DNS resolution so that all users' access traffic passes through the protective IP before returning to the real server (equivalent to routing all traffic to the protective IP).

