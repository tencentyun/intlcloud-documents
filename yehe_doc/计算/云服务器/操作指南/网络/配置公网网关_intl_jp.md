
<dx-alert infotype="alarm" title="">
**単一のCloud Virtual Machine（CVM）をパブリックゲートウェイとして使用すると、シングルポイントリスクがあるため、本番環境では[NAT Gateway](https://intl.cloud.tencent.com/document/product/1015/30226)を使用することをお勧めします。**
</dx-alert>
注意：2019年12月06日以降、Tencent Cloudは、CVMの購入ページでのパブリックゲートウェイの選択と設定をサポートしません。必要に応じて、このドキュメントでの設定に従って、ご自身で設定してください。




## 概要

Tencent Cloud VPCの一部のCVMに共通のパブリックネットワークIPがないが、パブリックネットワークにアクセスする必要がある場合は、パブリックネットワークIP（共通のパブリックネットワークIPまたはElasticパブリックネットワークIP）を備えたCVMを使用してパブリックネットワークにアクセスできます。パブリックゲートウェイCVMは、アウトバウンドトラフィックのソースアドレス変換を実行します。他のすべてのCVMがパブリックネットワークにアクセスするトラフィックは、パブリックゲートウェイCVMを通過した後、ソースIPがパブリックゲートウェイCVMのパブリックネットワークIPアドレスに変換されます。下図の通りです：
![](https://main.qcloudimg.com/raw/4879fa2798946972e8496c13a1bfa3cc.png)

##  前提条件
- すでに[CVMコンソール](https://console.cloud.tencent.com/cvm/index)ログインしています。
- パブリックゲートウェイCVMは、配置されているサブネット上にないルートの転送要求のみを転送できるため、パブリックゲートウェイCVMは、パブリックゲートウェイを使用してパブリックネットワークにアクセスする必要があるCVMと同じサブネット内に存在することはできません。
- パブリックゲートウェイCVMはLinux CVMである必要があります。Windows CVMをパブリックゲートウェイとして使用することはできません。

## 操作手順
### 手順1：Elasticパブリックネットワークへのバインディング（オプション）

<dx-alert infotype="explain" title="">
パブリックゲートウェイとして使用されるCVMにすでにパブリックネットワークIPアドレスがある場合は、この手順をスキップして次の手順を完了してください。
</dx-alert>

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、左側ナビゲーションバーでは、 **[ElasticパブリックネットワークIP](https://console.cloud.tencent.com/cvm/eip)** をクリックして、ElasticパブリックネットワークIP管理ページへ進みます。
2. インスタンスをバインディングする必要があるElasticパブリックネットワークIPのアクションバーの下にある**その他** > **バインディング**を選択します。
![](https://main.qcloudimg.com/raw/c9e46426e64fd6de3d4a2a9dccb91822.png)
3. 「リソースのバインディング」ポップアップボックスで、パブリックゲートウェイとして選択されたCVMインスタンスを選択してバインディングします。
![](https://main.qcloudimg.com/raw/1642880850b505fa57a598d10247edbc.png)

### 手順2：ゲートウェイが配置されているサブネットのルートテーブルの設定

<dx-alert infotype="notice" title="">
ゲートウェイサブネットと共通サブネットを同じルートテーブルにアソシエイトすることはできません。独立したゲートウェイルートテーブルを作成し、ゲートウェイサブネットをこのルートテーブルにアソシエイトしてください。
</dx-alert>

1. [カスタマイズルートテーブルの作成](https://intl.cloud.tencent.com/document/product/215/35236)。
2. 作成後、サブネットへのアソシエイトアクションが要求されます。パブリックゲートウェイサーバーが配置されているサブネットを直接アソシエイトすることができます。
![](https://main.qcloudimg.com/raw/4f804600a0d2120a959e722daf21fa59.png)

### 手順3：共通サブネットのルートテーブルの設定
共通サブネットのルートテーブルを設定します。デフォルトでルーティングがパブリックゲートウェイCVMを経由することで、共通サブネット内のCVMがパブリックゲートウェイのルーティング転送機能によってパブリックネットワークにアクセスできるように設定します。
共通CVMが配置されているサブネットのルートテーブルに、次のルーティングポリシーを追加します：
- ターゲット側：アクセスするパブリックネットワークアドレス。
- ネクストホップタイプ：CVM。
- ネクストホップ：手順1でElasticパブリックネットワークIPにバインディングされたCVMインスタンスのプライベートネットワークIP。
具体的な操作については、[ルーティングポリシーの設定](https://intl.cloud.tencent.com/document/product/215/40080)をご参照ください。
![](https://main.qcloudimg.com/raw/68e072841dc6d528fe2ff269e5a982a5.png)

### 手順4：パブリックゲートウェイの設定
1. [パブリックゲートウェイCVM](https://intl.cloud.tencent.com/document/product/213/5436)にログインし、次の操作を実行してネットワーク転送およびNATプロキシ機能を有効にします。
 1. 次のコマンドを実行して、`usr/local/sbin`ディレクトリにスクリプト`vpcGateway.sh`を新規作成します。
```
vim /usr/local/sbin/vpcGateway.sh
```
 2. **i**を押して編集モードに切り替え、次のコードをスクリプトに書き込みます。
```
#!/bin/bash
echo "----------------------------------------------------"
echo " `date`"
echo "(1)ip_forward config......"
file="/etc/sysctl.conf"
grep -i "^net\.ipv4\.ip_forward.*" $file &>/dev/null && sed -i \
's/net\.ipv4\.ip_forward.*/net\.ipv4\.ip_forward = 1/' $file || \
echo "net.ipv4.ip_forward = 1" >> $file
echo 1 > /proc/sys/net/ipv4/ip_forward
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
 3. **Esc**を押し、 **:wq** を入力して、ファイルを保存して戻ります。
 4. 次のコマンドを実行して、スクリプトファイルの権限を設定します。
```
chmod +x /usr/local/sbin/vpcGateway.sh
echo "/usr/local/sbin/vpcGateway.sh >/tmp/vpcGateway.log 2>&1" >> /etc/rc.local
```
2. パブリックゲートウェイのrpsの設定：
 1. 次のコマンドを実行して、`usr/local/sbin`ディレクトリにスクリプト`set_rps.sh`を新規作成します。
```
vim /usr/local/sbin/set_rps.sh
```
 2. **i**を押して編集モードに切り替え、次のコードをスクリプトに書き込みます。
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
 3. **Esc**を押して、 **:wq** を入力し、ファイルを保存して戻ります。
 4. 次のコマンドを実行して、スクリプトファイルの権限を設定します。
```
chmod +x /usr/local/sbin/set_rps.sh
echo "/usr/local/sbin/set_rps.sh >/tmp/setRps.log 2>&1" >> /etc/rc.local
chmod +x /etc/rc.d/rc.local
```
3. 上記の設定が完了すると、パブリックゲートウェイCVMをリスタートして設定を有効にし、パブリックネットワークIPがないCVMで、パブリックネットワークに正常にアクセスできるかどうかをテストします。



