>! Mulai 6 Desember 2019, Tencent Cloud tidak lagi mendukung konfigurasi CVM sebagai gateway publik di halaman pembelian CVM. Jika Anda perlu mengonfigurasi gateway, ikuti petunjuk di bawah ini.
>

## Ikhtisar

Anda dapat mengakses internet dengan menggunakan CVM gateway publik dengan IP publik atau EIP saat beberapa CVM berbasis VPC Anda tidak memiliki IP publik. CVM gateway publik menerjemahkan IP sumber untuk lalu lintas keluar. Saat CVM lain mengakses internet melalui CVM gateway publik, IP sumber akan diterjemahkan menjadi IP publik CVM gateway publik. Lihat gambar di bawah ini.
![](https://main.qcloudimg.com/raw/5876f3c92f1ae7cb5b4d8f38e59cbfd2.png)

## Prasyarat
- Anda login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
- CVM gateway publik dan CVM yang perlu mengakses internet melalui CVM gateway publik harus berada di subnet yang berbeda karena CVM gateway publik hanya dapat meneruskan permintaan dari subnet lain.
- CVM gateway publik harus CVM Linux. CVM Windows tidak akan berfungsi.

## Petunjuk
### Langkah 1: ikat EIP (opsional)
>?Lewati langkah ini jika CVM gateway publik sudah memiliki alamat IP publik.

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) dan pilih [**EIP**](https://console.cloud.tencent.com/cvm/eip) di bilah sisi kiri.
2. Cari EIP untuk mengikat instans, pilih **More** (Lainnya) > **Bind** (Ikat) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/b25421e826f69e00a1890e9d59c62828.png)
3. Pada jendela pop-up, pilih CVM yang akan dikonfigurasi dan ikat ke EIP.
![](https://main.qcloudimg.com/raw/c23b101995cabbe66d546f2a2bcb64ca.png)

### Langkah 2: konfigurasikan tabel rute untuk subnet gateway
>!Subnet gateway dan subnet lainnya tidak dapat berbagi tabel rute yang sama. Anda perlu membuat tabel rute terpisah untuk subnet gateway.
>
1. [Buat tabel rute kustom](https://intl.cloud.tencent.com/document/product/215/35236).
2. Hubungkan tabel rute dengan subnet tempat CVM gateway publik berada.
![](https://main.qcloudimg.com/raw/c7a6697f7ce1cc4e5c515cfb894ccd25.png)

### Langkah 3: konfigurasikan tabel rute untuk subnet lainnya
Tabel rute ini mengarahkan semua lalu lintas dari CVM tanpa IP publik ke gateway publik sehingga CVM ini juga dapat mengakses jaringan publik.
Tambahkan kebijakan perutean berikut ke tabel rute:
- Tujuan: IP publik yang ingin Anda akses.
- Jenis hop selanjutnya: CVM.
- Hop selanjutnya: IP pribadi dari instans CVM tempat EIP terikat pada Langkah 1.
Untuk informasi selengkapnya, lihat [Mengelola tabel Rute](https://intl.cloud.tencent.com/document/product/215/35236).
![](https://main.qcloudimg.com/raw/9b2d9537e7aa0c00428ef112db300d73.png)

### Langkah 4: konfigurasikan gateway publik
1. [Login ke CVM gateway publik](https://intl.cloud.tencent.com/document/product/213/5436), dan lakukan langkah-langkah berikut untuk mengaktifkan penerusan jaringan dan proksi NAT.
 1. Jalankan perintah berikut untuk membuat skrip `vpcGateway.sh` di `usr/local/sbin`.
```
vim /usr/local/sbin/vpcGateway.sh
```
 2. Tekan **i** untuk beralih ke mode edit dan tambahkan kode berikut ke skrip.
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
 3. Tekan **Esc** dan masukkan **:wq** untuk menyimpan dan menutup file.
 4. Jalankan perintah berikut untuk mengatur izin skrip.
```
chmod +x /usr/local/sbin/vpcGateway.sh
echo "/usr/local/sbin/vpcGateway.sh >/tmp/vpcGateway.log 2>&1" >> /etc/rc.local
```
2. Atur RPS gateway publik.
 1. Jalankan perintah berikut untuk membuat skrip `set_rps.sh` di `usr/local/sbin`.
```
vim /usr/local/sbin/set_rps.sh
```
 2. Tekan **i** untuk beralih ke mode edit dan tambahkan kode berikut ke skrip.
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
 3. Tekan **Esc** dan masukkan **:wq** untuk menyimpan dan menutup file.
 4. Jalankan perintah berikut untuk mengatur izin skrip.
```
chmod +x /usr/local/sbin/set_rps.sh
echo "/usr/local/sbin/set_rps.sh >/tmp/setRps.log 2>&1" >> /etc/rc.local
chmod +x /etc/rc.d/rc.local
```
3. Mulai ulang CVM gateway publik untuk menerapkan konfigurasi. Kemudian, uji apakah CVM tanpa IP publik dapat mengakses Internet melalui CVM gateway publik.

