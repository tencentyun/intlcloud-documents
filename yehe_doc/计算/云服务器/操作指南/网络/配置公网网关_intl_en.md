> As of December 6, 2019, Tencent Cloud no longer supports Public Network Gateway configuration when purchasing a CVM. If you need to configure a gateway, following these instructions.
>

## Scenario

If some of your CVMs in Tencent Cloud VPC do not have common public IP addresses but need to access the Internet, you can use a CVM with a public IP (common or elastic public IP) as the public gateway to enable them to access the Internet. The public gateway CVM translates the source IP of outbound traffic. When any other CVMs access the Internet through the public gateway CVM, the public gateway CVM translates their IPs to the public IP of the public gateway CVM, as shown in the figure below.
![](https://main.qcloudimg.com/raw/4879fa2798946972e8496c13a1bfa3cc.png)
## Prerequisites
- Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
- The public gateway CVM and the CVMs that need to access the Internet through the public gateway CVM are located in different subnets because the public gateway CVM can only forward routing requests from other subnets.
- The public gateway CVM must be a Linux CVM. A Windows CVM cannot serve as a public gateway.

## Directions
### Step 1: Bind an elastic public IP (optional)
>If the CVM that serves as the public gateway already has a public IP address, skip this step.

1. In the navigation panel to the left, click **[EIP](https://console.cloud.tencent.com/cvm/eip)** to go to the EIP management page.
2. Find the target elastic public IP and select **More** > **Bind** in the **Operation** column to bring up the **Bind resources** window.
![](https://main.qcloudimg.com/raw/c9e46426e64fd6de3d4a2a9dccb91822.png)
3. Select a CVM instance to serve as the public gateway and bind it to the elastic public IP.
![](https://main.qcloudimg.com/raw/1642880850b505fa57a598d10247edbc.png)

### Step 2: Configure a routing table for the subnet of the gateway
The gateway subnet and other subnets cannot use the same route table. A separate route table must be created for the gateway subnet.
1. Create a custom route table
2. Associate the route table with the subnet where the public gateway CVM is located as prompted.
![](https://main.qcloudimg.com/raw/4f804600a0d2120a959e722daf21fa59.png)

### Step 3: Configure a route table for the other subnets
This route table directs all traffic from the CVMs without a public IP to the gateway so they can access public networks as well.
In the route table for the common subnet, add the following routing policy:
- Destination: public IP to be accessed.
- Next-hop type: CVM.
- Next hop: private IP of the CVM instance to which the elastic public IP is bound in Step 1.
![](https://main.qcloudimg.com/raw/68e072841dc6d528fe2ff269e5a982a5.png)

### Step 4: Configure the public gateway
1. Log in to the public gateway CVM, enable network forwarding and NAT proxy, and optimize related parameters.
 1. Run the following command to create a file named `vpcGateway.sh` in `usr/local/sbin`.
	```
	vim /usr/local/sbin/vpcGateway.sh
	```
 2. Press **i** to enter edit mode and add the following code in the script:
		```
	#!/bin/bash
	echo "----------------------------------------------------"
	echo "          `date`"

	echo "(1)ip_forward config......"
	file="/etc/sysctl.conf"
	grep -i "^net\.ipv4\.ip_forward.*" $file &>/dev/null && sed -i \
	's/net\.ipv4\.ip_forward.*/net\.ipv4\.ip_forward = 1/' $file || \
	echo "net.ipv4.ip_forward = 1"  >> $file
	echo 1 >/proc/sys/net/ipv4/ip_forward 
	[ `cat /proc/sys/net/ipv4/ip_forward` -eq 1 ] && echo "-->ip_forward:Success" || \
	echo "-->ip_forward:Fail"

	echo "(2)Iptables set......"
	iptables -t nat -A POSTROUTING -j MASQUERADE && echo "-->nat:Success" || echo "-->nat:Fail"
	iptables -t mangle -A POSTROUTING -p tcp -j TCPOPTSTRIP --strip-options timestamp && \
	echo "-->mangle:Success" || echo "-->mangle:Fail"

	echo "(3)nf_conntrack config......"
	echo 262144 >  /sys/module/nf_conntrack/parameters/hashsize
	[ `cat /sys/module/nf_conntrack/parameters/hashsize` -eq 262144 ] && \
	echo "-->hashsize:Success" ||  echo "-->hashsize:Fail"

	echo 1048576 > /proc/sys/net/netfilter/nf_conntrack_max
	[ `cat /proc/sys/net/netfilter/nf_conntrack_max` -eq 1048576 ] && \
	echo  "-->nf_conntrack_max:Success" ||  echo  "-->nf_conntrack_max:Fail"

	echo 10800 >/proc/sys/net/netfilter/nf_conntrack_tcp_timeout_established \
	[ `cat /proc/sys/net/netfilter/nf_conntrack_tcp_timeout_established` -eq 10800 ] \
	 && echo  "-->nf_conntrack_tcp_timeout_established:Success" ||  \
	 echo  "-->nf_conntrack_tcp_timeout_established:Fail"
	```
 3. Press **Esc** to exit edit mode and enter **:wq** to save the file and go back. Then, run the following commands:
		```
		chmod +x /usr/local/sbin/vpcGateway.sh
		echo "/usr/local/sbin/vpcGateway.sh  >/tmp/vpcGateway.log 2>&1" >> /etc/rc.local
		```

2. Set the RPS of the public gateway.

 1. Run the following command to create a file named `setrps.sh` in `usr/local/sbin`.
	```
	vim /usr/local/sbin/set_rps.sh
	```
 2. Press **i** to enter edit mode and add the following code in the script:
	```
	#!/bin/bash
	echo "--------------------------------------------"
	* date
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
		  echo "cpu number:$cpu_nums  mask:0x$mask"
			
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
				
			  echo "eth:$eth  queues:$nic_queues"
			  total_nic_queues=$(($total_nic_queues + $nic_queues))
			  i=0
			  while (($i < $nic_queues)); do
				  echo $mask >/sys/class/net/$eth/queues/rx-$i/rps_cpus
				  echo 4096 >/sys/class/net/$eth/queues/rx-$i/rps_flow_cnt
					i=$(($i + 1))
			 done
		  done
			
		  flow_entries=$((total_nic_queues * 4096))
		  echo "total_nic_queues:$total_nic_queues  flow_entries:$flow_entries"
		  echo $flow_entries >/proc/sys/net/core/rps_sock_flow_entries
	}
	set_rps
	```
 3. Press **Esc** to exit edit mode and enter **:wq** to save the file and go back. Then, run the following commands:
	```
	chmod +x /usr/local/sbin/set_rps.sh
	echo "/usr/local/sbin/set_rps.sh >/tmp/setRps.log 2>&1" >> /etc/rc.local
	```
	
3. Reboot the gateway CVM to apply the configurations. Then, test if a CVM that has no public IP can access the Internet through the public gateway CVM.
