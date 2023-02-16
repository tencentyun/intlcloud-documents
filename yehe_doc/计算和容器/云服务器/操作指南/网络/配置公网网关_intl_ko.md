
<dx-alert infotype="alarm" title="">
**단일 클라우드 서버(CVM)를 공용 네트워크로 사용하면 단일 지점 장애 리스크가 있으므로 생성 환경에서는 [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015/30226)를 사용하는 것이 좋습니다.**
</dx-alert>
2019년 12월 06일부터 Tencent Cloud는 CVM 구매 시 공용망 게이트웨이 설정을 더 이상 지원하지 않습니다. 게이트웨이를 설정해야 하는 경우 다음 방법을 따르십시오.




## 작업 시나리오

Tencent Cloud VPC의 일부 CVM에 일반 공용 IP 주소가 없지만 인터넷에 액세스해야 하는 경우 공용망 게이트웨이로 공용 IP(일반 공용 IP 또는 EIP)가 있는 CVM을 사용하여 인터넷에 액세스할 수 있습니다. 공용망 게이트웨이 CVM은 아웃바운드 트래픽의 소스 IP를 변환합니다. 다른 CVM이 공용망 게이트웨이 CVM을 통해 인터넷에 액세스하면 공용망 게이트웨이 CVM은 아래 그림과 같이 자신의 IP를 공용망 게이트웨이 CVM의 공용 IP로 변환합니다.
![](https://main.qcloudimg.com/raw/4879fa2798946972e8496c13a1bfa3cc.png)

## 전제 조건
- [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인되어 있어야 합니다.
- 공용망 게이트웨이 CVM과 공용망 게이트웨이 CVM을 통해 인터넷에 액세스해야 하는 CVM은 다른 서브넷에 위치합니다. 공용망 게이트웨이 CVM은 다른 서브넷의 라우팅 요청만 포워딩할 수 있기 때문입니다.
- 공용망 게이트웨이 CVM은 Linux CVM이어야 합니다. Windows CVM은 공용망 게이트웨이 역할을 할 수 없습니다.

## 작업 단계
### 1단계: EIP 바인딩(옵션)

<dx-alert infotype="explain" title="">
공용망 게이트웨이 역할을 하는 CVM에 이미 공용 IP 주소가 있는 경우 이 단계를 건너뜁니다.
</dx-alert>

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하고 왼쪽 사이드바에서 **[EIP](https://console.cloud.tencent.com/cvm/eip)** 를 클릭하여 EIP 관리 페이지로 이동합니다.
2. 인스턴스를 바인딩할 EIP를 찾아 작업 열에서 **더 보기** > **바인딩**을 선택합니다.
![](https://main.qcloudimg.com/raw/c9e46426e64fd6de3d4a2a9dccb91822.png)
3. ‘리소스 바인딩’ 팝업 창에서 공용망 게이트웨이로 사용할 CVM 인스턴스를 선택하고 바인딩합니다.
![](https://main.qcloudimg.com/raw/1642880850b505fa57a598d10247edbc.png)

### 2단계: 게이트웨이 서브넷에 대한 라우팅 테이블 설정

<dx-alert infotype="notice" title="">
게이트웨이 서브넷과 다른 서브넷은 동일한 라우팅 테이블을 사용할 수 없습니다. 게이트웨이 서브넷에 대해 별도의 라우팅 테이블을 생성해야 합니다.
</dx-alert>

1. [Creating Custom Route Tables](https://intl.cloud.tencent.com/document/product/215/35236).
2. 프롬프트에 따라 공용망 게이트웨이 CVM이 있는 서브넷과 라우팅 테이블을 연결합니다.
![](https://main.qcloudimg.com/raw/4f804600a0d2120a959e722daf21fa59.png)

### 3단계: 다른 서브넷에 대한 라우팅 테이블 설정
이 라우팅 테이블은 공용 IP가 없는 CVM의 모든 트래픽을 게이트웨이로 전달하므로 공용 네트워크에도 액세스할 수 있습니다.
일반 서브넷의 라우팅 테이블에서 다음 라우팅 정책을 추가합니다.
- 대상: 액세스할 공용 IP입니다.
- 다음 홉 유형: CVM.
- 다음 홉: 1단계에서 EIP가 바인딩된 CVM 인스턴스의 개인 IP입니다.
자세한 내용은 [Managing Routing Policies](https://intl.cloud.tencent.com/document/product/215/40080)를 참고하십시오.
![](https://main.qcloudimg.com/raw/68e072841dc6d528fe2ff269e5a982a5.png)

### 4단계: 공용망 게이트웨이 설정
1. [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)하고 네트워크 전송 및 NAT 프록시를 활성화하고 관련 매개변수를 최적화합니다.
 1. 다음 명령을 실행하여 `usr/local/sbin` 디렉터리에 `vpcGateway.sh`라는 파일을 생성합니다.
```
vim /usr/local/sbin/vpcGateway.sh
```
 2. **i**를 눌러 편집 모드로 이동하여 스크립트에 다음 코드를 추가합니다.
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
 3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
 4. 다음 명령을 실행하여 스크립트 파일 권한을 설정합니다.
```
chmod +x /usr/local/sbin/vpcGateway.sh
echo "/usr/local/sbin/vpcGateway.sh >/tmp/vpcGateway.log 2>&1" >> /etc/rc.local
```
2. 공용망 게이트웨이의 rps를 설정합니다.
 1. 다음 명령을 실행하여 `usr/local/sbin` 디렉터리에 `set_rps.sh`라는 파일을 생성합니다.
```
vim /usr/local/sbin/set_rps.sh
```
 2. **i**를 눌러 편집 모드로 이동하여 스크립트에 다음 코드를 추가합니다.
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
 3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
 4. 다음 명령을 실행하여 스크립트 파일 권한을 설정합니다.
```
chmod +x /usr/local/sbin/set_rps.sh
echo "/usr/local/sbin/set_rps.sh >/tmp/setRps.log 2>&1" >> /etc/rc.local
chmod +x /etc/rc.d/rc.local
```
3. 게이트웨이 CVM을 재부팅하여 설정을 적용합니다. 그 다음 공용 IP가 없는 CVM이 공용망 게이트웨이 CVM을 통해 인터넷에 액세스할 수 있는지 테스트합니다.



