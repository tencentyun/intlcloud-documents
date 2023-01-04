### What are the destination address and ports for the cloud connection over Direct Connect?
Allow the destination address and ports in the firewall as shown below.
>? The address and ports will not change.

![](https://qcloudimg.tencent-cloud.cn/raw/2ee0b4ea8948caf819e0e95b5dc95df2.png)

### Can the TCSS agent be installed for IDCs outside the Chinese mainland?
Yes. The TCSS agent can be installed as long as the network is connected and the system meets the requirements.

### When will the non-Tencent Cloud instance be displayed in the console after the agent is installed?
Within seconds.

### Do I need to purchase the console if I use a non-Tencent Cloud instance?
No. The management and billing take place in the public cloud console.

### What are the destination IP and ports for IDC access to the cloud network?
The destination IP is included in the installation command, and the ports are 5574, 80, 8080, and 9080.

### Can I use TCSS if the private network instance cannot access the public network or there is no Direct Connect?
No.

### Does the hybrid cloud agent conflict with Zabbix processes?
There is no special processing for Zabbix or injection. Check for other agent installation drivers on the instance.