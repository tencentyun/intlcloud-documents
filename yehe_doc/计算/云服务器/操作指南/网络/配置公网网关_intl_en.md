
<dx-alert infotype="alarm" title="">
**Using a single CVM instance as the public gateway has the risk of single point of failure. You are advised to use a [NAT gateway](https://intl.cloud.tencent.com/document/product/1015/30226) in the production environment.**
</dx-alert>
As of December 6, 2019, Tencent Cloud no longer supports configuring a CVM as the public gateway on the CVM purchase page. If you need to configure a gateway, follow the instructions below.




## Overview

You can access the internet by using a public gateway CVM with a public IP or EIP when some of your VPC-based CVMs lack the public IPs. The public gateway CVM translates the source IP for outbound traffic. When other CVMs access the internet through the public gateway CVM, the source IPs will be translated into public IP of the public gateway CVM. See the figure below.
![](https://main.qcloudimg.com/raw/4879fa2798946972e8496c13a1bfa3cc.png)

## Prerequisites
- You are logged in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
- The public gateway CVM and the CVMs that need to access the internet through the public gateway CVM must be in different subnets because the public gateway CVM can only forward requests from other subnets.
- The public gateway CVM must be a Linux CVM. Windows CVMs will not work.

## Directions
### Step 1: bind an EIP (optional)

<dx-alert infotype="explain" title="">
Skip this step if the public gateway CVM already has a public IP.
</dx-alert>

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index) and choose **EIP** on the left sidebar.
2. Locate the EIP to bind the instance, select **More** > **Bind** in the **Operation** column.
![](https://main.qcloudimg.com/raw/c9e46426e64fd6de3d4a2a9dccb91822.png)
3. In the pop-up window, select a CVM to be configured and bind it to the EIP.
![](https://main.qcloudimg.com/raw/1642880850b505fa57a598d10247edbc.png)

### Step 2: configure a route table for the gateway subnet

<dx-alert infotype="notice" title="">
The gateway subnet and other subnets cannot share the same route table. You need to create a separate route table for the gateway subnet.
</dx-alert>

1. [Create a custom route table](https://intl.cloud.tencent.com/document/product/215/35236).
2. Associate the route table with the subnet where the public gateway CVM resides.
![](https://main.qcloudimg.com/raw/4f804600a0d2120a959e722daf21fa59.png)

### Step 3: configure a route table for the other subnets
This route table directs all traffic from the CVMs without a public IP to the public gateway so these CVMs can access public networks as well.
Add the following routing policies to the route table:
- Destination: the public IP you want to access.
- Next hop type: CVM.
- Next hop: private IP of the CVM instance to which the EIP is bound in Step 1.
For more information, see [Manage Route table](https://intl.cloud.tencent.com/document/product/215/40080).
![](https://main.qcloudimg.com/raw/68e072841dc6d528fe2ff269e5a982a5.png)

### Step 4: configure the public gateway
1. Log in to the [public gateway CVM instance](https://intl.cloud.tencent.com/document/product/213/5436) and perform the following operations to enable the network forwarding and NAT proxy features:
 1. Run the following command to create the `vpcGateway.sh` script in `usr/local/sbin`.
```
vim /usr/local/sbin/vpcGateway.sh
```
 2. Press **i** to switch to the edit mode and add the following code to the script.
```
#!/bin/bash
echo "----------------------------------------------------"
echo " `date`"
echo "(1)ip_forward config......"
file="/etc/sysctl.conf"
grep -i "^net\.ipv4\.ip_forward.*" $file &>/dev/null && sed -i \
's/net\.ipv4\.ip_forward.*/net\.ipv4\.ip_forward = 1/' $file || \
echo "net.ipv4.ip_forward = 1" >> $file
echo 1 >/proc/sys/net/ipv4/ip_forward
[ `cat /proc/sys/net/ipv4/ip_forward` -eq 1 ] && echo "-->ip_forward:Success" || \
echo "-->ip_forward:Fail"
echo "(2)Iptables set......"
iptables -t nat -A POSTROUTING -j MASQUERADE && echo "-->nat:Success" || echo "-->nat:Fail"
iptables -t mangle -A POSTROUTING -p tcp -j TCPOPTSTRIP --strip-options timestamp && \
echo "-->mangle:Success" || echo "-->mangle:Fail"
echo "(3)nf_conntrack config......"
echo 262144 > /sys/module/nf_conntrack/parameters/hashsize
[ `cat /sys/module/nf_conntrack/parameters/hashsize` -eq 262144 ] && \
echo "-->hashsize:Success" || echo "-->hashsize:Fail"
echo 1048576 > /proc/sys/net/netfilter/nf_conntrack_max
[ `cat /proc/sys/net/netfilter/nf_conntrack_max` -eq 1048576 ] && \
echo "-->nf_conntrack_max:Success" || echo "-->nf_conntrack_max:Fail"
echo 10800 >/proc/sys/net/netfilter/nf_conntrack_tcp_timeout_established \
[ `cat /proc/sys/net/netfilter/nf_conntrack_tcp_timeout_established` -eq 10800 ] \
&& echo "-->nf_conntrack_tcp_timeout_established:Success" || \
echo "-->nf_conntrack_tcp_timeout_established:Fail"
```
 3. Click **Esc** and enter **:wq** to save and close the file.
 4. Run the following command to set the script permission.
```
chmod +x /usr/local/sbin/vpcGateway.sh
echo "/usr/local/sbin/vpcGateway.sh >/tmp/vpcGateway.log 2>&1" >> /etc/rc.local
```
2. Set the RPS of the public gateway.
 1. Run the following command to create the `set_rps.sh` script in `usr/local/sbin`.
```
vim /usr/local/sbin/set_rps.sh
```
 2. Press **i** to switch to the edit mode and add the following code to the script.
```
# !/bin/bash
echo "--------------------------------------------"
date
mask=0
i=0
total_nic_queues=0
get_all_mask() {
local cpu_nums=$1
if [ $cpu_nums -gt 32 ]; then
mask_tail=""
mask_low32="ffffffff"
idx=$((cpu_nums / 32))
cpu_reset=$((cpu_nums - idx * 32))
if [ $cpu_reset -eq 0 ]; then
mask=$mask_low32
for ((i = 2; i <= idx; i++)); do
mask="$mask,$mask_low32"
done
else
for ((i = 1; i <= idx; i++)); do
mask_tail="$mask_tail,$mask_low32"
done
mask_head_num=$((2 ** cpu_reset - 1))
mask=$(printf "%x%s" $mask_head_num $mask_tail)
fi
else
mask_num=$((2 ** cpu_nums - 1))
mask=$(printf "%x" $mask_num)
fi
echo $mask
}
set_rps() {
if ! command -v ethtool &>/dev/null; then
source /etc/profile
fi
ethtool=$(which ethtool)
cpu_nums=$(cat /proc/cpuinfo | grep processor | wc -l)
if [ $cpu_nums -eq 0 ]; then
exit 0
fi
mask=$(get_all_mask $cpu_nums)
echo "cpu number:$cpu_nums mask:0x$mask"
ethSet=$(ls -d /sys/class/net/eth*)
for entry in $ethSet; do
eth=$(basename $entry)
nic_queues=$(ls -l /sys/class/net/$eth/queues/ | grep rx- | wc -l)
if (($nic_queues == 0)); then
continue
fi
cat /proc/interrupts | grep "LiquidIO.*rxtx" &>/dev/null
if [ $? -ne 0 ]; then # not smartnic
#multi queue don't set rps
max_combined=$(
$ethtool -l $eth 2>/dev/null | grep -i "combined" | head -n 1 | awk '{print $2}'
)
#if ethtool -l $eth goes wrong.
[[ ! "$max_combined" =~ ^[0-9]+$ ]] && max_combined=1
if [ ${max_combined} -ge ${cpu_nums} ]; then
echo "$eth has equally nic queue as cpu, don't set rps for it..."
continue
fi
else
echo "$eth is smartnic, set rps for it..."
fi
echo "eth:$eth queues:$nic_queues"
total_nic_queues=$(($total_nic_queues + $nic_queues))
i=0
while (($i < $nic_queues)); do
echo $mask >/sys/class/net/$eth/queues/rx-$i/rps_cpus
echo 4096 >/sys/class/net/$eth/queues/rx-$i/rps_flow_cnt
i=$(($i + 1))
done
done
flow_entries=$((total_nic_queues * 4096))
echo "total_nic_queues:$total_nic_queues flow_entries:$flow_entries"
echo $flow_entries >/proc/sys/net/core/rps_sock_flow_entries
}
set_rps
```
 3. Click **Esc** and enter **:wq** to save and close the file.
 4. Run the following command to set the script permission.
```
chmod +x /usr/local/sbin/set_rps.sh
echo "/usr/local/sbin/set_rps.sh >/tmp/setRps.log 2>&1" >> /etc/rc.local
chmod +x /etc/rc.d/rc.local
```
3. Restart the public gateway CVM to apply the configurations. Then, test if a CVM without a public IP can access the Internet through the public gateway CVM.



