### How should I configure firewall iptables on a Linux OS?
> **Notes:**
> iptables varies greatly for versions earlier and later than CentOS 7.
> - In versions earlier than CentOS 7, the iptables service is used as the firewall by default. By running the `service iptables stop` command, the iptables service will first clear rules and then unload the iptables module. When the iptables service restarts, it loads rules from the configuration file. You can stop the iptables service to test whether the firewall restrictions are applied.
>[](https://main.qcloudimg.com/raw/4a404e0187b0ee677034c0df82468e4a.png)
> - In versions later than CentOS 7, the firewall service is used as the firewall by default, and the iptables_filter module is loaded to ensure compatibility. You can use the iptables command to add rules. However, the iptables service is disabled by default. After you confirm that the iptable_filter module is loaded, the rules take effect.

To determine the firewall, run `iptables -nvL` to view rules. 
The following examples describe how to configure the iptables firewall software program. 
#### Scenario 1
In an Ubuntu 14 OS, the security group and listening port are enabled, but the Telnet connection fails.
Security group inbound rules:
![](https://main.qcloudimg.com/raw/ef640902a0e0c78af6c07eb7102bb0d7.png)
Security group outbound rules:
![](https://main.qcloudimg.com/raw/03a960f82b6e88fdca9aff8f10d76f4c.png)
Telnet connection failure:
![](https://main.qcloudimg.com/raw/74c521a97d4b9dab64b85ce62ab2cf86.png)
#### Troubleshooting
1. Capture packets on the CVM to check whether packets are sent to the CVM.
 - If no, the packets may be blocked by the security group, upper TGW, or ISP.
 - If yes but the CVM does not respond, this issue may be caused by the iptables policy of the CVM. As shown in the following figure, the CVM does not return TCP packets to 64.11 after the Telnet connection is established.
![](https://main.qcloudimg.com/raw/1052893022c8786a9b7b0166a57ce16d.png)  

2. After identifying that the issue is caused by the iptables policy, run `iptables –nvL` to check whether the policy opens port 8081. In this example, port 8081 is closed. 
![](https://main.qcloudimg.com/raw/bccfca60e3d707ae61c5ba236bf088f8.png) 
3. Run the following command to open port 8081:
```
iptables -I INPUT 5 -p tcp  --dport 8081 -j ACCEPT
```
4. Check whether port 8081 is opened. If yes, the issue has been solved.  


#### Scenario 2
Based on the iptables configuration, the policy has been enabled, but the destination server still cannot be pinged through.
![](https://main.qcloudimg.com/raw/46fdf4e20187c5b366c7773d73eb1cee.png)
#### Troubleshooting
If the information shown below appears,
![](https://main.qcloudimg.com/raw/d1b01f74223ed34c78a789dc43d53bc8.png)
run the following command to delete the first output rule:
```
iptabels –D OUTPUT 1
```
Verify that the issue has been solved.

### How can I remove a firewall?
#### Windows instances:
1. After logging in to the instance, choose **Start** > **Control Panel** > **Firewall Settings** to go to the "Firewall Settings" page.

2. Check whether the firewall and other security software, such as safedog, have been enabled. If yes, disable them.

#### Linux instances:
1. Run the following command to check whether the firewall policy is enabled. If no, skip step 2 and go to step 3.
```
iptables -vnL
```

2. If the firewall policy is enabled, run the following command to back up the firewall policy:
```
iptables-save
```

3. Run the following command to clear the firewall policy:
```
iptables -F
```

### Will the firewall intercept a non-Tencent Cloud CDN CVM?
No. If you worry that the firewall may disrupt your business, disable the firewall.