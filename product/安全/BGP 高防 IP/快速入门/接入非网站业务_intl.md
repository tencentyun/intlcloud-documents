[//]: # (chinagitpath:XXXXX)

This document shows you how to connect non-website applications to Anti-DDoS Advanced instances and verify protection configuration.

## Prerequisites

- To add a forwarding rule, you need to **purchase an Anti-DDoS Advanced instance**.
- To modify the DNS information of your business domain name, you need to purchase the **domain name resolution product**.

## Process 

![](https://main.qcloudimg.com/raw/26be97a1509c1947df6837ca6dce7597.png)

## Steps
<span id="step1"></span> 
### Configuring the forwarding rule

   1. Log in to the [Anti-DDoS Advanced console](https://console.cloud.tencent.com/dayu/bgpip), find the target instance and click the instance ID to enter the configuration page.
   2. In the **Forwarding Rules** configuration bar, click **New** to create a forwarding rule.

   ![](https://main.qcloudimg.com/raw/2e1749adb177c75205dbad1535582175.png)
    
  3. Configure the following parameters as needed and then click **OK**.

 - Forwarding protocol: TCP and UDP are supported.
 - Forwarding port: For access to the anti-DDoS Advanced IP.  We recommended you select the same forwarding port as that of the real server. Anti-DDoS Advanced does not support using 843, 1433, 1434, 3306, 3389, 36000 and 56000 ports as the forwarding port.
 - Real server port: The real port of the customer website.
 - Real server IP: Enter the IP address of the real server. If there are multiple real server IPs, you can enter all of them and separate them by pressing Enter. You are allowed to set up to  20 IP addresses. Your anti-DDoS Advanced IP utilizes round-robin load balancing to forward the business traffic.
 
 ![](https://main.qcloudimg.com/raw/7aee6b44bcbb34e262f17ff7bedda5cf.png)

<span id="step2"></span> 
### Open the intermediate IP range

To prevent the service unavailability that occurs when the real server blocks Anti-DDoS Advanced's intermediate IP, we suggest you to configure whitelist policies for the real server infrastructure,  including firewall, Web Application Firewall, intrusion protection system (IPS) and traffic management, and disable the protection feature of the host firewall and other security software (such as Safedog) or set whitelist policies, so that the intermediate IP will not be affected by the security policies of the real server.
For details about the intermediate IP segment of Anti-DDoS Advanced, contact Tencent Cloud support team.

<span id="step3"></span> 
### Local verification configuration

After the forwarding configuration is completed, the Anti-DDoS Advanced IP will forward the messages from the relevant port to the corresponding real server port by following the forwarding rules.
To ensure the stability of your business, a local test is recommended. The verification methods are as follows:

- **For applications accessed via IPs**
  For applications accessed via IPs (such as games), run `telnet` to check whether the Anti-DDoS Advanced IP port is accessible. You can also set the  Anti-DDoS Advanced IP as the server IP in your local client (if available) to check whether the connection is successful.
  For example, the protective IP is 10.1.1.1 with port 1234. And the real server IP is 10.2.2.2 with port 1234. Run `telnet` on your local to connect to 10.1.1.1:1234. If the address can be accessed, it means that the forwarding is successful.
- **For applications accessed via domain names**
  For applications accessed via domain names, please try the followings:
 1. Modify your local *hosts* file so that the requests that have been sent to the protected sites can be forwarded to the Anti-DDoS Advanced IP.
   Example: For  Windows users:
   1. Open the *hosts* file (C:\Windows\System32\drivers\etc), and add the following content at the end of the text:
   `<Protective IP address> <Domain name of the protected website>`
   For example, if the protected IP is 10.1.1.1 and the domain name is [www.qq.com](www.qq.com), add:
   `10.1.1.1       www.qq.com`
   2. Save the hosts file.
 2. Run the `ping` command on the protected domain name on the local computer.
   If the resolved IP address is the same as Anti-DDoS Advanced IP address in the *hosts* file, the forwarding is successful.
 > ? If the resolved IP address is still the real server IP address, try running the `ipconfig/flushdns` command in the Command Prompt to clear the local DNS cache.

  3. Confirm that IP binding is working, and check whether the domain name is accessible.  The configuration is successful if the domain name is accessible.
> ? If the domain name is not accessible, log in to the [Anti-DDoS Advanced console](https://console.cloud.tencent.com/dayu/bgpip) to check whether the configuration is correct and fix errors if possible. If the issue still exists, please contact Tencent Cloud support team.

<span id="step4"></span>
### Modify the DNS resolution of the business domain name

  After binding the forwarding rules to the Anti-DDoS Advanced IP, you can verify if the connection from the Anti-DDoS Advanced forwarding port to the real server port is successful, and point business IP to the  Anti-DDoS Advanced. Now the configuration is completed.
  
  If your uses the DNS resolution, you can modify the domain name resolution in DNS service provider and change the original business IP address to Anti-DDoS Advanced IP address.
  
  Modify DNS resolution so that user traffic will go through the Anti-DDoS Advanced IP before returning back to the real server. You can think of routing the requests to your Anti-DDoS Advanced IP.
