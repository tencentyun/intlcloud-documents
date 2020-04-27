## Scenario
When you choose 0Mbps bandwidth for a CVM, this CVM will not be able to access the public network. This document uses CentOS7.5 as an example to describe how a CVM without a public IP can access a public network by connecting to a CVM with a public IP through a PPTP VPN. 


## Prerequisites
- Create two CVMs in the same VPC (One **CVM without a public IP** and the other **CVM with a public IP**).
- Get the private IP of the CVM with a public IP.

## Directions
### Configuring PPTP on the CVM with a public IP

1. Log in to the CVM with a public IP.
2. Execute the following command to install PPTP.
```
yum install -y pptpd
```
3. Execute the following command to open the `pptpd.conf` configuration file.
```
vim /etc/pptpd.conf
```
3. Press “**i**” to switch to editing mode and add the following content to the bottom of the file.
```
localip 192.168.0.1
remoteip 192.168.0.234-238,192.168.0.245
```
4. Press **Esc**, enter **:wq**, save the file and return.
5. Execute the following command to open the `/etc/ppp/chap-secrets` configuration file.
```
vim /etc/ppp/chap-secrets
```
6. <span id="step7">Press “**i**” to switch to editing mode and on the bottom of the file add the user name and password to connect to PPTP in the following format.</span>
```
User Name    pptpd    Password    *
```
For example, if the username to connect to PPTP is root and the password is 123456, the information needs to be added as follows:
```
root    pptpd    123456    *
```
7. Press **Esc**, enter **:wq**, and save the file and return.
8. Execute the following command to launch the PPTP service.
```
systemctl start pptpd
```
9. Execute the following commands one-by-one to launch forwarding ability.
```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.0/24 -j MASQUERADE
```

### Configuring PPTP on the CVM without a public IP

1. Log in to the CVM without a public IP.
2. Execute the following command to install a PPTP client.
```
yum install -y pptp pptp-setup
``` 
3. Execute the following command to create the configuration file.
```
pptpsetup --create name of the configuration file --server private IP of the CVM with a public IP --username username to connect PPTP --password password to connect PPTP --encrypt
```
For example, if the private IP of the CVM with a public IP is 10.100.100.1, you can execute the following command to create a test configuration file:
```
pptpsetup --create test --server 10.100.100.1 --username root --password 123456 --encrypt
```
4. Execute the following command to connect to PPTP.
```
pppd call test（the file name created for step 3）
```
5. Execute the following commands one-by-one to set the route.
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
Execute the following command on the CVM without a public IP to ping any external network address and check whether it can be pinged.
```
ping -c 4 external network address
```
If a result similar to the following is returned, the configuration is successful:
![](https://main.qcloudimg.com/raw/c841782ce0976982d1f289d3437ec0ed.png)



