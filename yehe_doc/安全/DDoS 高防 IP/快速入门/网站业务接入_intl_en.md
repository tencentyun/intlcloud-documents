This document describes how to connect a website business to an Anti-DDoS Advanced instance and verify the forwarding configuration.
>Currently, only website businesses in Beijing, Shanghai, and Guangzhou regions can be connected. Businesses outside Mainland China are not supported.

## Prerequisites
- To add a forwarding rule, you need to [purchase an Anti-DDoS Advanced instance in Mainland China](https://buy.cloud.tencent.com/antiddos#/advanced) or [outside Mainland China](https://buy.cloud.tencent.com/antiddos#/advanced-intl).
- To modify the DNS information of your business domain name, you need to purchase the domain name resolution product.

## Process
![](https://main.qcloudimg.com/raw/2e1749adb177c75205dbad1535582175.png)

## Directions


### Configuring forwarding rule
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview) and click **Business Connection** on the left sidebar.
2. On the "Business Connection" page, select the **Domain Name Connection** tab and click **Add Domain Name**.
![](https://main.qcloudimg.com/raw/cfbfe8e83df682516d665ad5bfeab834.png)
3. On the forwarding rule adding page, configure the following parameters as needed:
![](https://main.qcloudimg.com/raw/b881a15850a364dc08393ccd1738468f.png)
Parameter description:
 - Domain Name: enter the website domain name to be protected.
 - Protocol: HTTP and HTTPS are supported. Please select an option as needed:
<table>
<tr>
<th>Business Scenario</th>
<th>Relevant Operation</th>
</tr>
<tr>
<td>Websites supporting only HTTP</td>
<td>Select **HTTP**.</td>
</tr>
<tr>
<td>Websites supporting only HTTPS</td>
<td><ul><li>Select **HTTPS**.</li>
        <li>Certificate source: Tencent Cloud-hosted certificate is selected by default.</li>
        <li>Certificate: select the name of the corresponding SSL certificate.</li></td>
</tr>
</table>
  - Forwarding Method: **forwarding via IP** and **forwarding via domain name** are supported.
    - If you select **Forwarding via IP**, enter the IP (or IP + port) of the real server. If one website domain name corresponds to multiple real server IPs (or IP + port pairs), you can enter all of them and separate them with carriage return. Up to 16 IPs (or IP + port pairs) are supported.
    - If you select **Forwarding via domain name**, enter the real server domain name (CNAME) or domain name (CNAME) + port. If one website domain name corresponds to multiple real server domain names (CNAMEs) or pairs of domain name (CNAME) + port, you can enter all of them and separate them with carriage returns. Up to 16 entries are supported.



### Opening forwarding IP range
To prevent business interruption that occurs if the real server blocks the Anti-DDoS Advanced forwarding IP, you are recommended to configure allowlist policies for the real server infrastructure (such as firewall, web application firewall, intrusion protection system (IPS), and traffic management system) and disable the protection features of the server firewall and other security software tools (such as Safedog) or set allowlist policies for them, so that the forwarding IP will not be affected by the security policies of the real server.

You can log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview) and click **Instance List** on the left sidebar to find the target instance ID.
![](https://main.qcloudimg.com/raw/ff2ae3b5f116c04589779023e20171c6.png)
Click the instance ID to enter the basic information page and view the Anti-DDoS Advanced forwarding IP range.
![](https://main.qcloudimg.com/raw/4f959d6a68bf3cedf5c7815411717079.png)

### Verifying configuration locally
After the forwarding configuration is completed, the Anti-DDoS Advanced IP will forward the packets from the relevant port to the corresponding real server port according to the forwarding rule.
To ensure the stability of your business, a local test is recommended. The verification method is as follows:
1. Modify the local `hosts` file to direct local requests to the protected site to your Anti-DDoS Advanced instance. The following uses Windows as an example to describe how to configure the local `hosts` file:
    Open the `hosts` file in `C:\Windows\System32\drivers\etc` and add the following content at the end of the file:
    ```
    <Anti-DDoS Advanced IP address> <Domain name of the protected website>
    ```
    For example, if the Anti-DDoS Advanced IP is `10.1.1.1` and the domain name is `www.qq.com`, then add:
    ```
    10.1.1.1       www.qqq.com
    ```
    Save the `hosts` file and run the `ping` command on the local computer to ping the protected domain name. If the resolved IP address is the Anti-DDoS Advanced IP address bound in the `hosts` file, the local `hosts` configuration has taken effect.
    >If the resolved IP address is still the real server IP address, try running the `ipconfig /flushdns` command in Windows Command Prompt to clear the local DNS cache.

3. After successfully configuring the `hosts`, check whether the domain name can be accessed. If it can be accessed properly, the configuration has taken effect.
>If the verification still fails with the correct method, please log in to the Anti-DDoS Advanced Console and check whether the configuration is correct. If the problem persists after you fix any incorrect configuration items, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
