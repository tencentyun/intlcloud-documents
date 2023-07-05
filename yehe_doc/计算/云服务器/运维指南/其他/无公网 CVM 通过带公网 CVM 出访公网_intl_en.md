## Overview
If you select a bandwidth with an upper limit of 0 Mbps when purchasing a CVM, the CVM will be unable to access the public network. This document uses CentOS 7.5 as an example to describe how a CVM without a public IP address can access the public network by connecting to a CVM with a public IP address through a PPTP VPN.


## Prerequisites
- Two CVMs in the same VPC instance have been created. One **CVM does not have a public IP address** and the other **CVM has a public IP address**.
- The private IP address of the CVM with a public IP address has been obtained.

## Directions
### Configuring PPTP on the CVM with a public IP address

1. Log in to the CVM with a public IP address.
2. Run the following command to install PPTP:
```
yum install -y pptpd
```
3. Run the following command to open the `pptpd.conf` configuration file:
```
vim /etc/pptpd.conf
```
4. Press **i** to switch to the editing mode and add the following code at the bottom of the file.
```
localip 192.168.0.1
remoteip 192.168.0.234-238,192.168.0.245
```
5. Press **Esc**, enter **:wq**, and save and close the file.
6. Run the following command to open the `/etc/ppp/chap-secrets` configuration file:
```
vim /etc/ppp/chap-secrets
```
7. <span id="step7">Press **i** to switch to the editing mode and add the username and password for connecting to PPTP in the following format at the bottom of the file.</span>
```
<Username>    pptpd    <Password>    *
```
For example, if the username and password for connecting to PPTP are root and 123456 respectively, add the following code:
```
root    pptpd    123456    *
```
8. Press **Esc**, enter **:wq**, and save and close the file.
9. Run the following command to start the PPTP service:
```
systemctl start pptpd
```
10. Run the following commands sequentially to enable forwarding:
```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.0/24 -j MASQUERADE
```

### Configuring PPTP on the CVM without a public IP address

1. Log in to the CVM without a public IP address.
2. Run the following command to install a PPTP client:
```
yum install -y pptp pptp-setup
``` 
3. Run the following command to create a configuration file:
```
pptpsetup --create <Configuration file name> --server <Private IP address of the CVM with a public IP address> --username <Username for connecting to PPTP> --password <Password for connecting to PPTP> --encrypt
```
For example, if you have obtained the private IP address 10.100.100.1 of the CVM with a public IP address, run the following command to create a test configuration file:
```
pptpsetup --create test --server 10.100.100.1 --username root --password 123456 --encrypt
```
4. Run the following command to connect to PPTP:
```
pppd call test (the configuration file name created in step 3)
```
5. Run the following commands to set routes:
```
route add -net 10.0.0.0/8 dev eth0
route add -net 172.16.0.0/12 dev eth0
route add -net 192.168.0.0/16 dev eth0
route add -net 169.254.0.0/16 dev eth0
route add -net 9.0.0.0/8 dev eth0
route add -net 100.64.0.0/10 dev eth0
route add -net 0.0.0.0 dev ppp0
```

### Checking whether the configuration was successful
Run the following command on the CVM without a public IP address to ping any external network address and check whether it can be pinged through:
```
ping -c 4 <External network address>
```
If a result similar to the following is returned, the configuration was successful:
![](https://main.qcloudimg.com/raw/c841782ce0976982d1f289d3437ec0ed.png)



