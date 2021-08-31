### How should I configure the firewall software iptables on a Linux OS?
> **Notes:**
> iptables varies greatly between versions earlier and later than CentOS 7.
> - In versions earlier than CentOS 7, the iptables service is used as the firewall by default. After running the `service iptables stop` command, the iptables service will first clear rules and then unload the iptables module. When the iptables service restarts, it will load rules from the configuration file. You can stop the iptables service to test whether the firewall restrictions were applied.
>[](https://main.qcloudimg.com/raw/4a404e0187b0ee677034c0df82468e4a.png)
> - In versions later than CentOS 7, the firewall service is used as the firewall by default, and the iptables_filter module is loaded to ensure compatibility. You can use the iptables command to add rules. However, the iptables service is disabled by default. After you confirm that the iptable_filter module is loaded, the rules will take effect.

To determine the firewall, run `iptables -nvL` to view the rules. 
The following two scenarios describe how to configure the iptables firewall software program. 
#### Scenario 1
In an Ubuntu 14 OS, the security group and listening port are enabled, but the Telnet connection fails.
Security group inbound rules:
![](https://main.qcloudimg.com/raw/4a6a1c7eca94a76ddbce457dbe28affa.png)
Security group outbound rules:
![](https://main.qcloudimg.com/raw/90914e729ba27a6a9253e719bf4a9703.png)
Telnet connection failure:
![](https://main.qcloudimg.com/raw/74c521a97d4b9dab64b85ce62ab2cf86.png)
#### Solution
1. Capture the packets on the CVM to check whether the packets were sent to the CVM.
 - If no, the packets may be blocked by the security group, the upper TGW, or the ISP.
 - If yes but the CVM does not respond, this issue may be caused by the iptables policy of the CVM. As shown in the following figure, the CVM does not return TCP packets to 64.11 after the Telnet connection is established.
![](https://main.qcloudimg.com/raw/1052893022c8786a9b7b0166a57ce16d.png)  

2. After confirming that the issue is caused by the iptables policy, run `iptables –nvL` to check whether the policy opened port 8081. In this example, port 8081 is closed. 
![](https://main.qcloudimg.com/raw/f214d470f1d40ed7061ea155de756bca.jpg) 
3. Run the following command to open port 8081:
```
iptables -I INPUT 5 -p tcp  --dport 8081 -j ACCEPT
```
4. Check whether port 8081 is open. If yes, the issue has been solved.  


#### Scenario 2
Based on the iptables configuration, the policy has been enabled, but the destination server still cannot be pinged through.
![](https://main.qcloudimg.com/raw/46fdf4e20187c5b366c7773d73eb1cee.png)
#### Solution
If the information shown below appears,
![](https://main.qcloudimg.com/raw/babfa7fcfe9dd7536ba011c3fbaab7bc.jpg)
run the following command to delete the first output rule:
```
iptabels –D OUTPUT 1
```
Test to verify that the issue has been solved.

### How can I remove a firewall?
#### Windows instances:
1. After logging in to the instance, choose **Start** > **Control Panel** > **Firewall Settings** to access the "Firewall Settings" page.

2. Check whether the firewall and other security software, such as safedog, have been enabled. If yes, disable them.

#### Linux instances:
1. Run the following command to check whether the firewall policy has been enabled. If no, skip step 2 and go to step 3.
```
iptables -vnL
```

2. If the firewall policy has been enabled, run the following command to back up the firewall policy:
```
iptables-save
```

3. Run the following command to clear the firewall policy:
```
iptables -F
```

### Will the firewall intercept a non-Tencent Cloud CDN CVM?
No. If you are worried that the firewall may disrupt your business, you can disable the firewall.
