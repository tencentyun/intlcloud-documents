> Mulai 6 Desember 2019, Tencent Cloud tidak lagi mendukung konfigurasi Public Network Gateway saat membeli CVM. Jika Anda perlu mengonfigurasi gateway, ikuti petunjuk ini.
>

## Skenario

Jika beberapa CVM Anda di Tencent Cloud VPC tidak memiliki alamat IP publik umum tetapi perlu mengakses Internet, Anda dapat menggunakan CVM dengan IP publik (IP publik umum atau elastis) sebagai gateway publik agar dapat mengakses Internet. CVM gateway publik menerjemahkan IP sumber lalu lintas keluar. Ketika CVM lain mengakses Internet melalui CVM gateway publik, CVM gateway publik menerjemahkan IP mereka ke IP publik CVM gateway publik, seperti yang ditunjukkan pada gambar di bawah.
![](https://main.qcloudimg.com/raw/4879fa2798946972e8496c13a1bfa3cc.png)
## Prasyarat
- Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
- CVM gateway publik dan CVM yang perlu mengakses Internet melalui CVM gateway publik terletak di subnet yang berbeda karena CVM gateway publik hanya dapat meneruskan permintaan perutean dari subnet lain.
- CVM gateway publik harus berupa CVM Linux. CVM Windows tidak dapat berfungsi sebagai gateway publik.

## Petunjuk
### Langkah 1: Ikat IP publik elastis (opsional)
>Jika CVM yang berfungsi sebagai gateway publik sudah memiliki alamat IP publik, lewati langkah ini.

1. Di panel navigasi di sebelah kiri, klik **[EIP](https://console.cloud.tencent.com/cvm/eip)** ([EIP]) untuk membuka halaman pengelolaan EIP.
2. Temukan IP publik elastis target, lalu pilih **More** (Lainnya) > **Bind** (Ikat) di kolom **Operation** (Operasi) untuk membuka jendela **Bind resources** (Ikat sumber daya).
![](https://main.qcloudimg.com/raw/c9e46426e64fd6de3d4a2a9dccb91822.png)
3. Pilih instans CVM untuk dijadikan sebagai gateway publik dan ikat ke IP publik elastis.
![](https://main.qcloudimg.com/raw/1642880850b505fa57a598d10247edbc.png)

### Langkah 2: Konfigurasikan tabel perutean untuk subnet gateway
Subnet gateway dan subnet lainnya tidak dapat menggunakan tabel rute yang sama. Tabel rute terpisah harus dibuat untuk subnet gateway.
1. Buat tabel rute kustom
2. Kaitkan tabel rute dengan subnet tempat CVM gateway publik berada seperti yang diminta.
![](https://main.qcloudimg.com/raw/4f804600a0d2120a959e722daf21fa59.png)

### Langkah 3: Konfigurasikan tabel rute untuk subnet lainnya
Tabel rute ini mengarahkan semua lalu lintas dari CVM tanpa IP publik ke gateway sehingga lalu lintas juga dapat mengakses jaringan publik.
Di tabel rute untuk subnet umum, tambahkan kebijakan perutean berikut:
- Tujuan: IP publik yang akan diakses.
- Jenis hop selanjutnya: CVM.
- Hop selanjutnya: IP pribadi dari instans CVM tempat IP publik elastis terikat pada Langkah 1.
![](https://main.qcloudimg.com/raw/68e072841dc6d528fe2ff269e5a982a5.png)

### Langkah 4: Konfigurasikan gateway publik
1. Masuk ke CVM gateway publik, aktifkan penerusan jaringan dan proksi NAT, dan optimalkan parameter terkait.
 1. Jalankan perintah berikut untuk membuat file bernama `vpcGateway.sh` di `usr/local/sbin`.
	```
	vim /usr/local/sbin/vpcGateway.sh
	```
 2. Tekan **i** (i) untuk masuk ke mode edit dan tambahkan kode berikut ke dalam skrip:
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
 3. Tekan **Esc** (Esc) untuk keluar dari mode edit dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali. Kemudian, jalankan perintah berikut:
		```
		chmod +x /usr/local/sbin/vpcGateway.sh
		echo "/usr/local/sbin/vpcGateway.sh  >/tmp/vpcGateway.log 2>&1" >> /etc/rc.local
		```

2. Atur RPS gateway publik.

 1. Jalankan perintah berikut untuk membuat file bernama `setrps.sh` di `usr/local/sbin`.
	```
	vim /usr/local/sbin/set_rps.sh
	```
 2. Tekan **i** (i) untuk masuk ke mode edit dan tambahkan kode berikut ke dalam skrip:
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
				
			  echo "eth:$eth antrian:$nic_queues"
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
 3. Tekan **Esc** (Esc) untuk keluar dari mode edit dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali. Kemudian, jalankan perintah berikut:
	```
	chmod +x /usr/local/sbin/set_rps.sh
	echo "/usr/local/sbin/set_rps.sh >/tmp/setRps.log 2>&1" >> /etc/rc.local
	```
	
3. Boot ulang CVM gateway untuk menerapkan konfigurasi. Kemudian, uji apakah CVM yang tidak memiliki IP publik dapat mengakses Internet melalui CVM gateway publik.
