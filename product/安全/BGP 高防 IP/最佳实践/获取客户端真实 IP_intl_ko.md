

## 비웹사이트 비즈니스 포워딩 규칙 사용
Anti-DDoS Advanced가 비웹사이트 비즈니스 포워딩 규칙을 사용하며 오리진 서버는 toa 모듈을 사용하여 클라이언트의 실제 IP를 획득해야 합니다.

### 기본 원리
Anti-DDoS Advanced가 공중망 프록시 모드를 사용하기 때문에 데이터 패킷의 오리진 주소와 대상 주소 모두 수정됩니다. 오리진 서버에서 표시된 데이터 패킷 오리진 주소는 Anti-DDoS Advanced 인스턴스의 오리진 요청 IP로 클라이언트의 실제 IP가 아닙니다. 클라이언트 IP를 서버에 포워딩하기 위해, 포워딩 시 Anti-DDoS Advanced는 클라이언트 IP와 포트를 사용자 지정 tcp option 필드에 기록합니다. 다음과 같습니다.
```
#define TCPOPT_ADDR  200
#define TCPOLEN_ADDR 8      /* |opcode|size|ip+port| = 1 + 1 + 6 */

/*
 * insert client ip in tcp option, now only support IPV4,
 * must be 4 bytes alignment.
 */
struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
};
```

### 지원 운영 체제
•	CentOS 6.x
•	CentOS 7.x
>!
- Windows 운영 체제는 toa 모듈을 사용하는 클라이언트 실제 IP 획득을 지원하지 않습니다.
- Linux 기타 운영 체제는 [Tencent Cloud 기술 지원](https://cloud.tencent.com/about/connect)에 문의하십시오.

### 주의 사항
- 우선 테스트 환경에서 설치와 테스트를 진행하여 기능 가용성, 실행 안정성을 확인 후 다시 공식적 환경에서 배포하길 권장합니다.
- 커널을 업그레이드하려면 업그레이드 실패 등 예외 발생을 막기 위해 커널 업그레이드 전 기존 커널을 저장하길 권장합니다.
-  toa는 IPv4만 지원합니다. IPv6을 기본적으로 사용하는 환경에서 클라이언트 IP를 올바르게 획득할 수 없습니다.

### 클라이언트 실제 IP 가져오기
1. root 사용자로 아래 명령을 실행하여 컴파일 환경을 설치합니다.
`yum install gcc kernel-headers kernel-devel -y `
2. 설치 파일을 [다운로드](https://daaa-1254383475.cos.ap-shanghai.myqcloud.com/TOA_CentOS_v1.zip) 및 압축 해제합니다.
 ```
wget  https://daaa-1254383475.cos.ap-shanghai.myqcloud.com/TOA_CentOS_v1.zip
unzip TOA_CentOS_v1.zip
 ```
 <span id="step3"></span>
3. `uname -r` 명령을 실행하여 커널 버전을 확인합니다.
 예시: 
```
[root@VM_0_2_centos toa]# uname -r
3.10.0-514.26.2.el7.x86_64
```
4. [절차 3](#step3)의 조회 결과에 따라 Makefile 구성 파일의 경로 매개변수 KERNEL_DIR을 수정합니다.
예시:
```
[root@VM_0_2_centos toa]# vim Makefile 
obj-m := toa.o
KERNEL_DIR := /usr/src/kernels/3.10.0-514.26.2.el7.x86_64/
PWD := $(shell pwd)
#EXTRA_CFLAGS+=-D__GENKSYMS__
all:
        make -C $(KERNEL_DIR) M=$(PWD) modules
clean:    
        rm *.o *.ko *.mod.c  Module.symvers modules.order
```
5. `make` 명령을 실행하여 컴파일합니다.
6. 모듈을 이동하고 로딩합니다.
```
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```
 - 로딩 성공 후, 클라이언트 오리진 IP를 정상적으로 가져올 수 있습니다.
 - 클라이언트 오리진 IP를 아직도 획득할 수 없는 경우 `lsmod | grep toa` 명령을 실행하여 toa 모듈 로딩 상태를 점검할 수 있습니다.

### toa 모듈 탑재 해제
root 사용자로 아래 명령을 실행하여 toa 모듈을 탑재 해제합니다.
```
rmmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```

## 웹사이트 비즈니스 포워딩 규칙 사용
Anti-DDoS Advanced가 웹사이트 비즈니스 포워딩 규칙을 사용할 경우, HTTP 헤더의 X-Forwareded-For 필드를 이용하여 클라이언트 실제 IP를 가져올 수 있습니다.
X-Forwareded-For는 HTTP 헤드 확장 필드로 서버가 프록시 등 방식을 통해 연결한 클라이언트의 실제 IP를 식별하는 데 목적이 있습니다.
형식은 다음과 같습니다.
`X-Forwareded-For：Client，proxy1，proxy2，proxy3……  `
Anti-DDoS Advanced가 사용자의 접근 요청을 실제 서버에 포워딩하면, 요청 사용자의 실제 IP가 X-Forwareded-For 필드의 헤드 부분에 기록됩니다. 그렇기 때문에 오리진 서버 응용프로그램은 HTTP 헤드 X-Forwarded-For 필드의 내용만 가져오면 됩니다.
세부 정보는 [7계층 포워딩을 통한 실제 클라이언트 IP 획득 방법](https://cloud.tencent.com/document/product/214/3728)을 참조하십시오.

