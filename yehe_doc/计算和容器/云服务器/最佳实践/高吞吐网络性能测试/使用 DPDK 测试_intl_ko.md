## 작업 시나리오
본문은 DPDK 방법을 사용하여 높은 처리량의 CVM 네트워크 성능을 테스트하는 방법을 설명합니다.


## 작업 순서

### DPDK 컴파일 및 설치 
1. 테스트 서버 2대를 준비합니다. [사용자 정의 Linux CVM 설정](https://intl.cloud.tencent.com/document/product/213/10517)을 참고하여 테스트 서버를 구매합니다. 본문의 테스트 서버는 CentOS 8.2 운영 체제를 사용합니다.
2. 테스트 서버에 순서대로 로그인하고 다음 명령을 실행하여 DPDK 툴을 다운로드합니다. CVM에 로그인하는 방법은 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.
```
yum install -y sysstat wget tar automake make gcc 
```
```
wget http://git.dpdk.org/dpdk/snapshot/dpdk-17.11.tar.gz
```
```
tar -xf dpdk-17.11.tar.gz 
```
```
mv dpdk-17.11 dpdk
```
3. txonly 엔진을 수정하여 각 DPDK 송신 패킷의 CPU 상의 UDP 트래픽 포트가 여러 스트림을 생성하도록 합니다.
 - 다음 명령어를 실행하여 `dpdk/app/test-pmd/txonly.c` 파일을 수정합니다.
```
vim dpdk/app/test-pmd/txonly.c
``` 
**i**를 눌러 편집 모드로 들어가 다음 내용을 수정합니다.
    1. `#include "testpmd.h"`를 찾아 새 행에 다음 내용을 입력합니다.
```
RTE_DEFINE_PER_LCORE(struct udp_hdr, lcore_udp_hdr);
```
		다음과 같이 수정을 완료합니다.
![](https://main.qcloudimg.com/raw/69d640ddccd5e24538d51249e0fd0d6a.png)
    2. `ol_flags |= PKT_TX_MACSEC;`를 찾아 새 행에 다음 내용을 입력합니다.
```
/* dummy test udp port */
static uint16_t test_port = 0;
test_port++;
memcpy(&RTE_PER_LCORE(lcore_udp_hdr), &pkt_udp_hdr, sizeof(pkt_udp_hdr));
RTE_PER_LCORE(lcore_udp_hdr).src_port = rte_cpu_to_be_16(rte_lcore_id() * 199 + test_port % 16);
RTE_PER_LCORE(lcore_udp_hdr).dst_port = rte_cpu_to_be_16(rte_lcore_id() * 1999 + test_port % 16);
```
다음과 같이 수정을 완료합니다.
![](https://main.qcloudimg.com/raw/f3d08bb74601e96fbc59025906ee294d.png)
    3. `copy_buf_to_pkt(&pkt_udp_hdr, sizeof(pkt_udp_hdr), pkt,`를 찾아, 다음 내용으로 바꿉니다.
```
copy_buf_to_pkt(&RTE_PER_LCORE(lcore_udp_hdr), sizeof(RTE_PER_LCORE(lcore_udp_hdr)), pkt,
```
다음과 같이 수정을 완료합니다.
![](https://main.qcloudimg.com/raw/b235e11355eb0d96d8412b3ae15cc2e9.png)
**Esc**를 누르고 **:wq**를 입력하여 수정 사항을 저장하고 종료합니다.
 - 다음 명령어를 실행하여 `dpdk/config/common_base` 파일을 수정합니다.
```
vim dpdk/config/common_base
```
**i**를 눌러 편집 모드로 들어가 `CONFIG_RTE_MAX_MEMSEG=256`을 찾아 1024로 수정합니다. 다음과 같이 수정을 완료합니다.
![](https://main.qcloudimg.com/raw/6dea86be41b819b3f16042630346d2e3.png)
**Esc**를 누르고 **:wq**를 입력하여 수정 사항을 저장하고 종료합니다.
>? 수신측과 발신측 모두 상기 구성 파일을 수정해야 합니다. 다음 명령을 사용하여 수정된 파일을 피어로 전송하여 중복 수정을 방지합니다.
>```
scp -P 22 /root/dpdk/app/test-pmd/txonly.c root@<IP주소>:/root/dpdk/app/test-pmd/
scp -P 22 /root/dpdk/config/common_base root@<IP주소>:/root/dpdk/config
```
>
4. 다음 명령어를 실행하여 `dpdk/app/test-pmd/txonly.c`의 IP 주소를 테스트 서버용 IP로 수정합니다.
```
vim dpdk/app/test-pmd/txonly.c
``` 
**i**를 눌러 편집 모드로 들어가 다음 내용을 찾습니다.
```
#define IP_SRC_ADDR (198U << 24) | (18 << 16) | (0 << 8) | 1;
#define IP_DST_ADDR (198U << 24) | (18 << 16) | (0 << 8) | 2;   
```
숫자 198, 18, 0, 1을 디바이스 IP로 바꿉니다. SRC_ADDR은 발신측 IP, DST_ADDR은 수신측 IP입니다.
5. 디바이스 운영 체제에 따라 다음 명령을 실행하여 numa를 설치합니다.
<dx-tabs>
::: CentOS
```
yum install numactl-devel
```
:::
::: Ubuntu
```
apt-get install libnuma-dev
```
:::
</dx-tabs>
6. `dpdk/` 디렉터리에서 다음 명령을 실행하고 KNI를 비활성화합니다.
```
sed -i  "s/\(^CONFIG_.*KNI.*\)=y/\1=n/g" ./config/*
```
7. 운영 체제 커널 버전이 비교적 높은 경우(예: 5.3) 다음 명령을 실행하여 차이를 차단하십시오.
```
sed -i "s/\(^WERROR_FLAGS += -Wundef -Wwrite-strings$\)/\1 -Wno-address-of-packed-member/g" ./mk/toolchain/gcc/rte.vars.mk
```
```
sed -i "s/fall back/falls through -/g" ./lib/librte_eal/linuxapp/igb_uio/igb_uio.c
```
8. 다음 명령을 실행하여 DPDK를 컴파일합니다.
```
make defconfig
```
```
make -j
```

###  Hugepage 메모리 설정
다음 명령을 실행하여 Hugepage 메모리를 설정합니다.
```
echo 2048 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```
오류 메시지가 나타나면 Hugepage 메모리가 부족한 것입니다. 다음 예시와 같이 명령 설정을 조정할 수 있습니다.
```
echo 4096 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
```

### 커널 모듈 설치 및 인터페이스 바인딩
>?이 단계는 Python이 필요하므로 [Python 공식 웹사이트](https://www.python.org/doc/)에서 필요한 버전을 다운로드하여 설치하십시오. 본문에서는 Python 3.6.8을 예로 사용합니다.
>
1. 로그인 방식을 [VNC를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32494)으로 전환합니다. ENI 드라이버가 igb_uio 사용자 모드 드라이버에 바인딩된 후, 해당 ENI는 ssh 또는 IP를 통해 액세스할 수 없으며, VNC 또는 console을 통한 액세스만 지원됩니다.
2. 다음 명령을 순서대로 실행하여 UIO 모듈을 설치하고 virito 인터페이스를 바인딩합니다.
```
ifconfig eth0 0
```
```
ifconfig eth0 down
```
```
modprobe uio
```
```
insmod /root/dpdk/build/kmod/igb_uio.ko
```
```
cd /root/dpdk/usertools/
```
```
python3 dpdk-devbind.py --bind=igb_uio 00:05.0
```
>? 명령어의 00.05.0은 예시 주소입니다. ENI의 실제 주소를 얻으려면 다음 명령을 실행하십시오.
> ```
python3 dpdk-devbind.py -s
```
>
테스트 완료 후, 다음 명령을 실행하여 ENI 변경 사항을 복구할 수 있습니다.
```
cd /root/dpdk/usertools/
```
```
python3 dpdk-devbind.py --bind=virtio-pci 00:05.0
```
```
ifconfig eth0 up
```

### 대역폭 및 처리량 테스트
>?
>- 테스트 명령은 txpkts 매개변수를 사용하여 송신 패킷 크기를 제어합니다. 테스트 대역폭은 1430B를 사용하고, 테스트 pps는 64B를 사용합니다.
>- 이 단계의 명령 매개변수는 CentOS 8.2 운영 체제에 적용됩니다. 다른 시스템 미러 이미지 버전을 사용하는 경우 실제 시나리오에 따라 매개변수를 조정하고 다시 테스트합니다. 예를 들어, CentOS 7.4 커널 버전이 3.10으로 CentOS 8.2 커널 버전 4.18과 성능 차이가 있을 경우, 대역폭 테스트 명령어의 'nb-cores'를 2로 수정합니다. 명령 매개변수에 대한 더 많은 정보는 [estpmd-command-line-options](https://doc.dpdk.org/guides-17.11/testpmd_app_ug/run_app.html#testpmd-command-line-options)를 참고하십시오.
> 
1. 다음 명령을 실행합니다. 발신측은 TX only 모드를 사용하여 testpmd를 실행하고 수신측은 rxonly 모드를 활성화합니다.
 - 발신측:
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=16 --rxq=16 --nb-cores=1 --forward-mode=txonly --txpkts=1430 --stats-period=1
```
 - 수신측:
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=48 --rxq=48 --nb-cores=16 --forward-mode=rxonly --stats-period=1
```
2. 다음 명령을 실행하여 pps(UDP 64B 패킷)를 테스트합니다.
 - 발신측:
```
/root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=16 --rxq=16 --nb-cores=3 --forward-mode=txonly --txpkts=64 --stats-period=1
```
 - 수신측:
```
 /root/dpdk/build/app/testpmd -- --txd=128 --rxd=128 --txq=48 --rxq=48 --nb-cores=16 --forward-mode=rxonly --stats-period=1
```
아래 이미지와 같이 테스트 결과를 가져옵니다.
![](https://main.qcloudimg.com/raw/778c351d2b7975581bff0d7ab05b9f88.png)

### 네트워크 대역폭 계산
수신측 PPS와 테스트 패킷 길이에 따라 현재 네트워크의 수신 대역폭을 계산할 수 있으며, 공식은 다음과 같습니다.
PPS × packet length × 8bit/B × 10<sup>-9</sup> = 대역폭
테스트에서 얻은 데이터와 결합하여, 현재 대역폭은 다음과 같이 계산할 수 있습니다.
4692725pps × 1430B × 8bit/B × 10<sup>-9</sup>  ≈ 53Gbps
>?
>- 메시지 길이는 14B 이더넷 헤더, 8B CRC 및 20B IP 헤더를 포함하여 1430B입니다.
>- 테스트 결과의 Rx-pps는 순시값입니다. 더 정확한 결과와 평균값을 얻기 위해 여러 번 테스트할 수 있습니다.
