본문은 레이어 4(TCP 전용) CLB 서비스가 하이브리드 클라우드 배포 및 NAT64 CLB 시나리오에서 TOA를 통해 실제 클라이언트 IP를 가져오는 방법을 설명합니다.
<dx-steps>
-[TOA 로딩](#load-toa)
-[리얼 서버에 적용](#adapt-rs)
-[(옵션)TOA 상태 모니터링](#monitor-toa)
</dx-steps>

>?레이어 4(TCP) CLB는 TOA를 통해 실제 클라이언트 IP를 가져올 수 있지만 레이어 4(UDP) 및 레이어 7(HTTP/HTTPS) CLB는 그렇지 않습니다.
>
## 응용 시나리오
### 하이브리드 클라우드 배포
[Hybrid Cloud Deployment](https://intl.cloud.tencent.com/document/product/214/38442) 시나리오에서 IDC와 VPC의 IP는 겹칠 수 있으므로 SNAT IP가 필요합니다. 서버의 경우 실제 클라이언트 IP는 보이지 않으며 TOA를 통해 가져와야 합니다.

### NAT64 CLB
NAT64 CLB 시나리오에서 실제 IPv6 클라이언트 IP는 리얼 서버에 보이지 않는 IPv4 공중망 IP로 변환됩니다.
이 경우, 실제 클라이언트 IP는 TOA를 통해 얻을 수 있으며, 즉, TCP 패킷은 필드 TCP option에 실제 클라이언트 IP를 삽입한 후 실제 클라이언트 IP 정보를 서버로 전송하고 클라이언트는 TOA 커널 모듈의 API를 호출하여 실제 클라이언트 IP를 가져올 수 있습니다..


## 제한 설명
<dx-accordion>
::: 리소스 제한
- TOA 컴파일 환경의 커널 버전은 서비스 환경의 커널 버전과 일치해야 합니다.
- 컨테이너 환경에서는 TOA 커널 모듈을 호스트에 로딩해야 합니다.
- TOA 커널 모듈을 로딩하려면 root 권한이 필요합니다.
:::
::: 호환성 제한
 - UDP 리스너는 TOA를 통해 실제 클라이언트 IP를 가져올 수 없습니다.
 - 클라이언트와 리얼 서버 간에 이미 TOA 관련 작업이 있는 경우 리얼 서버는 실제 클라이언트 IP를 가져오지 못할 수 있습니다.
 -  TOA가 삽입된 후에는 새 연결에만 적용됩니다.
 - TOA는 필드 TCP option에서 주소 추출과 같은 추가 처리를 수행해야 하므로 서버 성능이 저하될 수 있습니다.
 - Tencent Cloud TOA를 다른 TOA 모듈과 함께 사용할 때 호환성 문제가 발생할 수 있습니다.
 - Tencent Cloud TOA는 TencentOS에 내장되어 있으며 하이브리드 클라우드 배포 시나리오에서 실제 원본 IP를 얻는 데 사용할 수 있습니다. 서버가 TencentOS에서 실행되고 하이브리드 클라우드에 배포되는 경우 `modprobe toa` 명령을 직접 실행하여 TOA를 로딩할 수 있습니다. 서버가 Linux에서 실행되는 경우 Linux TOA를 대신 사용해야 합니다.
:::
</dx-accordion>



## [TOA 로딩](id:load-toa)
1. Tencent Cloud의 Linux OS 버전에 해당하는 TOA 패키지를 다운로드하고 압축을 풉니다.
<dx-accordion>
::: centos
[CentOS 8.0 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%208.0.1905.zip)
[CentOS 7.6 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%207.6.1810.zip)
[CentOS 7.2 64](https://clb-toa-1255852779.file.myqcloud.com/CentOS%207.2.1511.zip)

:::
::: debian
[Debian 9.0 64](https://clb-toa-1255852779.file.myqcloud.com/Debian%209.zip)
:::
::: suse linux
[SUSE 12 64](https://clb-toa-1255852779.file.myqcloud.com/SUSE%2012.zip)
[SUSE 11 64](https://clb-toa-1255852779.file.myqcloud.com/SUSE%2011.zip)
:::
::: ubuntu
[Ubuntu 18.04.4 LTS 64](https://clb-toa-1255852779.file.myqcloud.com/Ubuntu%2018.04.4%20LTS.zip)
[Ubuntu 16.04.7 LTS 64](https://clb-toa-1255852779.file.myqcloud.com/Ubuntu%2016.04.7%20LTS.zip)
:::
</dx-accordion>

2. [](id:step2)압축 해제 후 cd 명령을 실행하여 압축이 해제된 폴더에 액세스하고 모듈 로딩 명령을 실행합니다.
```
insmod toa.ko
```
3. 다음 명령어를 실행하여 TOA가 로딩되었는지 확인합니다. ‘to load success’ 메시지가 표시되면 로딩이 성공한 것입니다.
```
dmesg -T | grep TOA
```
4. 로딩된 후 실행 스크립트에서 `toa.ko` 파일을 로딩합니다(ko 파일은 서버가 다시 시작되면 다시 로딩해야 함).
5. (옵션)TOA가 더 이상 필요하지 않은 경우 다음 명령을 실행하여 제거합니다.
```
rmmod toa
```
6. (옵션)다음 명령을 실행하여 모듈이 제거되었는지 확인합니다. ‘TOA unloaded’ 메시지가 표시되면 성공적으로 제거된 것입니다.
```
dmesg -T
```

상기 OS 버전에 대한 설치 패키지를 찾을 수 없는 경우 Linux OS용 일반 소스 패키지를 다운로드하고 컴파일하여 ko 파일을 가져올 수 있습니다. 이 일반 버전은 대부분의 Linux 릴리스 버전(예시: Centos8, Centos7, Ubuntu18.04 및 Ubuntu16.04)을 지원합니다.
>? Linux 커널과 Linux 릴리스 버전은 다양하므로 호환성 문제가 발생할 수 있습니다. TOA 소스 패키지를 사용하기 전에 OS에서 컴파일하는 것이 좋습니다.
>
1. 소스 패키지를 다운로드합니다.
>!OS가 Linux인 경우 Linux TOA 소스 패키지를 다운로드하십시오. TencentOS인 경우 TLinux TOA 소스 패키지를 다운로드합니다.
>
  - Linux
```
wget "https://clb-toa-1255852779.file.myqcloud.com/tgw_toa_linux_ver.tar.gz"
```
  - Tencent TLinux
```
wget "https://clb-toa-1255852779.file.myqcloud.com/tgw_toa_tlinux_ver.tar.gz"
```
2. TOA용 Linux 환경을 컴파일하려면 먼저 GCC 컴파일러, Make 툴 및 커널 개발 패키지를 설치해야 합니다.
<dx-accordion>
::: CentOS 환경 설치 단계

```
yum install gcc
yum install make
//커널 개발 패키지를 설치합니다. 패키지 헤더 파일 및 라이브러리의 버전은 커널 버전과 일치해야 합니다.
yum install kernel-devel-`uname -r`
```
:::
::: Ubuntu 및 Debian 설치 작업

```
apt-get install gcc
apt-get install make
//커널 개발 패키지를 설치합니다. 패키지 헤더 파일 및 라이브러리의 버전은 커널 버전과 일치해야 합니다.
apt-get install linux-headers-`uname -r`
```
:::
::: SUSE 환경 설치 단계
```
zypper install gcc
zypper install make
//커널 개발 패키지를 설치합니다. 패키지 헤더 파일 및 라이브러리의 버전은 커널 버전과 일치해야 합니다.
zypper install kernel-default-devel
```
:::
</dx-accordion>

3. 소스 패키지를 컴파일하여 toa.ko 파일을 생성합니다. 컴파일 과정에서 `warning` 및 `error` 메시지가 표시되지 않으면 컴파일이 성공한 것입니다. Linux OS용 소스 패키지를 예로 들어 보겠습니다.
```
tar zxvf tgw_toa_linux_ver.tar.gz
cd tgw_toa_linux_ver//압축 해제된 tgw_toa 디렉터리로 이동
make
```
4. toa.ko 컴파일이 성공하면 [2단계](#step2)를 수행하여 TOA를 로딩합니다.


## [리얼 서버 적용](id:adapt-rs)
<dx-accordion>
::: 하이브리드 클라우드 배포
하이브리드 클라우드에서 리얼 서버를 적용할 때 표준 Linux 네트워크 프로그래밍 API를 호출하기만 하면 코드 변경 없이 실제 클라이언트 IP를 가져올 수 있습니다. 다음은 코드 예시를 보여줍니다.
```
struct sockaddr v4addr;  
len = sizeof(struct sockaddr);  
//get_peer_name 은 표준 Linux 네트워크 프로그래밍 API입니다.
if (get_peer_name(client_fd, &v4addr, &len) == 0) {  
	inet_ntop(AF_INET, &(((struct sockaddr_in *)&v4addr)->sin_addr), from, sizeof(from));  
	printf("real client v4 [%s]:%d\n", from, ntohs(((struct sockaddr_in *)&v4addr)->sin_port));   
}
```
:::
::: NAT64 CLB
NAT64 CLB 시나리오에서 실제 원본 IP를 얻으려면 리얼 서버에 `toa.ko` 커널 모듈을 삽입한 후 원본 코드를 수정해야 하며 TOA는 해당 IP 주소를 리얼 서버에 전달합니다.
1. IP 주소를 저장할 데이터 구조를 정의합니다.
```
struct toa_nat64_peer {  
	struct in6_addr saddr;  
	uint16_t sport;  
};  
....  
struct toa_nat64_peer client_addr;  
....  
```
2. TOA 변수를 정의하고 호출하여 실제 원본 IPv6 주소를 가져옵니다.
```
enum {  
	TOA_BASE_CTL            = 4096,  
	TOA_SO_SET_MAX          = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP       = TOA_BASE_CTL,  
	TOA_SO_GET_MAX          = TOA_SO_GET_LOOKUP,  
};  
getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr, &len);  
```
3. 원본 IP 주소를 가져옵니다.
```
real_ipv6_saddr = client_addr.saddr;  
real_ipv6_sport = client_addr.sport;
```

전체 구성 예시는 다음과 같습니다.
```
//TOA 변수를 정의합니다. 'TOA_BASE_CTL'을 4096으로 설정합니다.
enum {  
	TOA_BASE_CTL            = 4096,  
	TOA_SO_SET_MAX          = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP       = TOA_BASE_CTL,  
	TOA_SO_GET_MAX          = TOA_SO_GET_LOOKUP,  
};  
//IP 주소를 저장할 데이터 구조를 정의합니다.
struct toa_nat64_peer {  
	struct in6_addr saddr;  
	uint16_t sport;  
};  
//주소를 저장할 변수를 선언합니다.  
struct toa_nat64_peer client_addr;  
.……  
//클라이언트의 파일 디스크립터를 가져옵니다. 여기서 listenfd는 서버의 수신 파일 디스크립터입니다.  
client_fd = accept(listenfd, (struct sockaddr*)&caddr, &length);  
// NAT64 시나리오에서 사용자의 실제 원본 IP를 가져오기 위해 호출합니다.  
char from[40];  
int len = sizeof(struct toa_nat64_peer);  
if (getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr, &len) == 0) {  
	inet_ntop(AF_INET6, &client_addr.saddr, from, sizeof(from));  
	//원본 IP와 원본 port 가져오기  
	printf("real client [%s]:%d\n", from, ntohs(client_addr.sport));  
}  
```
:::
::: 하이브리드 클라우드에서 사용되는 NAT64 CLB
NAT64 CLB가 하이브리드 클라우드에서 사용되는 시나리오에서 실제 원본 IP를 얻으려면 리얼 서버에 `toa.ko` 커널 모듈을 삽입한 후 원본 코드를 수정해야 하며 TOA는 해당 IP 주소를 리얼 서버에 전달합니다.

전체 구성 예시는 다음과 같습니다.
```
//TOA 변수를 정의합니다. 'TOA_BASE_CTL'을 4096으로 설정합니다.  
enum {  
	TOA_BASE_CTL = 4096,  
	TOA_SO_SET_MAX = TOA_BASE_CTL,  
	TOA_SO_GET_LOOKUP = TOA_BASE_CTL,  
	TOA_SO_GET_MAX = TOA_SO_GET_LOOKUP,   
};  

//IP 주소를 저장할 데이터 구조를 정의합니다.    
struct toa_nat64_peer {    
	struct in6_addr saddr;    
	uint16_t sport;    
};    

//주소를 저장할 변수를 선언합니다.    
struct toa_nat64_peer client_addr_nat64;    
.......  
//클라이언트의 파일 디스크립터를 가져옵니다. 여기서 listenfd는 서버의 수신 파일 디스크립터입니다.  
//NAT64 시나리오에서 실제 클라이언트 IP를 가져오기 위해 호출합니다.   
char from[40];    
int len = sizeof(struct toa_nat64_peer);  
int ret;  
ret = getsockopt(client_fd, IPPROTO_IP, TOA_SO_GET_LOOKUP, &client_addr_nat64, &len);  
if (ret == 0) {  
	inet_ntop(AF_INET6, &(client_addr_nat64.saddr), from, sizeof(from));    
	//원본 IP와 원본 Port를 가져옵니다.   
	printf("real client v6 [%s]:%d\n", from, ntohs(client_addr_nat64.sport));   
} else if (ret != 0) {  
	struct sockaddr v4addr;  
	len = sizeof(struct sockaddr);  
	//원본 IP와 원본 Port를 가져옵니다.  
	//하이브리드 클라우드 배포 시나리오에서 원본 IP 주소는 SNAT 뒤의 IP 주소입니다.  
	//비하이브리드 클라우드 배포 시나리오에서 원본 IP 주소는 SNAT 및 NAT64가 없는 클라이언트 IP 주소입니다.  
	//이 함수의 의미는 실제 클라이언트 주소와 포트를 가져오는 것입니다.  
	if (get_peer_name(client_fd, &v4addr, &len) == 0) {  
		inet_ntop(AF_INET, &(((struct sockaddr_in *)&v4addr)->sin_addr), from, sizeof(from));  
		printf("real client v4 [%s]:%d\n", from, ntohs(((struct sockaddr_in *)&v4addr)->sin_port));   
	}  
}  
```
:::
</dx-accordion>


## [(옵션)TOA 상태 모니터링](id:monitor-toa)
실행 안정성을 보장하기 위해 이 커널 모듈을 사용하여 상태를 모니터링할 수 있습니다. toa.ko 커널 모듈을 삽입한 후 다음 방법 중 하나로 컨테이너 호스트에서 TOA 작업 상태를 모니터링할 수 있습니다.
<dx-accordion>
::: 방법1: TOA에 저장된 IPv6 주소 확인
다음 명령어를 실행하여 TOA에 저장된 IPv6 주소를 확인합니다.
- 이 명령을 실행하면 성능이 저하될 수 있습니다. 주의하여 진행하십시오.

```
cat /proc/net/toa_table
```
:::
::: 방법 2: TOA 메트릭 확인
다음 명령을 실행하여 TOA 메트릭을 확인하십시오.
```
cat /proc/net/toa_stats
```
![](https://qcloudimg.tencent-cloud.cn/raw/0dcbd6a263316481f50d99c2e4fbab7a.png)
모니터링 메트릭은 다음과 같이 설명됩니다.
<table>
<thead>
<tr>
<th>메트릭</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>syn_recv_sock_toa</td>
<td>TOA 정보와의 연결을 수신합니다.</td>
</tr>
<tr>
<td>syn_recv_sock_no_toa</td>
<td>TOA 정보 없이 연결을 수신합니다.</td>
</tr>
<tr>
<td>getname_toa_ok</td>
<td>이 수는 getsockopt를 호출하고 원본 IP를 성공적으로 가져오거나 accept를 호출하여 클라이언트 요청을 수신할 때 증가합니다.</td>
</tr>
<tr>
<td>getname_toa_mismatch</td>
<td>이 수는 getsockopt를 호출하고 필요한 유형과 일치하지 않는 원본 IP를 가져올 때 증가합니다. 예를 들어 클라이언트 연결에는 IPv4 원본 IP 주소가 포함되어 있는 반면 IPv6 주소를 받으면 개수가 증가합니다.</td>
</tr>
<tr>
<td>getname_toa_empty</td>
<td>이 카운트는 TOA를 포함하지 않는 클라이언트 파일 디스크립터에서 getsockopt 함수가 호출될 때 증가합니다.</td>
</tr>
<tr>
<td>ip6_address_alloc</td>
<td>TOA가 TCP 데이터 패킷에 저장된 원본 IP와 원본 port를 가져오면 정보를 저장할 공간을 할당합니다.</td>
</tr>
<tr>
<td>ip6_address_free</td>
<td>연결이 릴리스되면 toa는 이전에 원본 IP 및 원본 port를 저장하는 데 사용된 메모리를 릴리스합니다. 모든 연결이 닫히면 각 CPU에 대한 ip6_address_alloc의 총 개수는 이 메트릭의 개수와 같아야 합니다.</td>
</tr>
</tbody>
</table>

:::
</dx-accordion>


## FAQ
<dx-accordion>
::: NAT64 CLB에 TOA를 삽입한 후 서버 프로그램을 수정해야 하는 이유는 무엇입니까?
클라이언트 IP 유형이 변경되지 않고 유지되는 NAT64 CLB 시나리오와 다른 하이브리드 클라우드 배포 시나리오에서 클라이언트 IP(IPv4)가 IPv6 주소로 변환되기 때문입니다. 따라서 서버가 IPv6 주소를 이해할 수 있도록 서버 프로그램을 수정해야 합니다.
:::
::: 내 OS가 Linux 릴리스 버전 또는 TLinux 커널을 기반으로 하는지 어떻게 알 수 있습니까?
- 다음 명령을 실행하여 내 커널 버전을 확인하십시오. 명령 출력에 `tlinux`가 표시되면 TLinux OS를 사용하고 있는 반면 linux는 Linux OS를 사용하고 있음을 나타냅니다.
```
uname -a
```
![](https://qcloudimg.tencent-cloud.cn/raw/3f266a4c245030173564cff0d3c77f73.png)

- 다음 명령을 사용하여 버전을 확인할 수도 있습니다. `tlinux` 또는 `tl2`가 반환되면 TLinux OS를 사용하고 있는 것입니다.
```
rpm -qa | grep kernel
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/4559818bd61436d7a752bcd9caf1b53d.png" width="70%">
:::
::: 원본 IP를 받지 못한 경우 사전 확인은 어떻게 합니까?
1. 다음 명령어를 실행하여 TOA가 로딩되었는지 확인합니다.
```
lsmod | grep toa
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/5b92aa9de0db3e43e91316c4363886f1.png" width="70%">
2. 서버 프로그램이 원본 IP를 얻기 위해 올바른 호출을 했는지 확인하십시오. [리얼 서버 적용](#adapt-rs)을 참고하십시오.
3. 서버에서 TCP 패킷을 캡처하고 패킷에 원본 IP 정보가 포함되어 있는지 확인합니다.
 - tcp option 출력에 `unknown-200`이 표시되면 TCP option 필드에 SNAT 이후의 실제 원본 IP가 삽입되었음을 나타냅니다.
 - `unknown-253`이 표시되면 NAT64 시나리오에 실제 원본 IPv6 주소가 삽입되었음을 나타냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e8fed1ab42370a97889c7dcdce660b72.png)
4. TOA 주소가 포함된 패킷이 서버로 전송된 경우 toa.ko를 DEBUG 버전으로 컴파일하고 커널 로그를 통해 문제를 추가로 찾습니다. 다운로드한 TOA 원본 디렉터리에서 DEBUG 컴파일 옵션을 Makefile에 추가합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e89cf9fd3d96a760485fb04c966ef6b0.png"width="60%">
5. 다음 명령을 실행하여 다시 컴파일합니다.
```
make clean
make
```
6. 다음 명령을 실행하여 원본 ko를 제거하고 최신 버전 ko를 설치합니다.
```
rmmod toa 
insmod ./toa.ko
```
7. 다음 명령을 실행하여 커널 로그를 관찰합니다.
```
dmesg -Tw
```
다음 메시지가 표시되면 TOA가 정상적으로 작동하는 것입니다. 서버 프로그램이 실제 원본 IP를 얻기 위해 호출했는지 또는 API가 잘못 사용되었는지 추가로 확인할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/9a958fc2b0ae9d185cd228c6668c7162.png)
8. 이전 단계에서 문제를 찾지 못한 경우 [티켓을 제출](https://console.cloud.tencent.com/workorder/category)하십시오.
:::
</dx-accordion>
