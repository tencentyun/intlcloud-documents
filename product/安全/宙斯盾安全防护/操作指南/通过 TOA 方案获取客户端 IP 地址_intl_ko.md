비즈니스 요청이 고도 방어 IP로 4계층 포워딩한 후 비즈니스 서버가 메시지를 수신한 뒤 볼 수 있는 오리진 IP 주소는 고도 방어 IP의 출구 IP 주소입니다. 서버가 사용자 실제 IP 주소를 획득할 수 있도록 다음 TOA 방안을 사용할 수 있습니다. 비즈니스 서비스의 Linux 서버에 그에 맞는 TOA 커널 패키지를 설치하고 서버를 다시 시작한 후에 비즈니스는 사용자의 실제 IP 주소를 획득할 수 있습니다.

## TOA 원리
고도 방어 IP로 포워딩한 후, 데이터 패키지가 동시에 SNAT와 DNAT를 진행하고 데이터 패키지의 오리진 주소와 타깃 주소가 모두 수정됩니다.
TCP 프로토콜에서 클라이언트 IP를 서버에 전달하기 위해 클라이언트의 IP, 포트를 포워딩할 때 사용자 지정 tcp option 필드에 삽입합니다.
		
    #define TCPOPT_ADDR	200  
    #define TCPOLEN_ADDR 8	/* |opcode|size|ip+port| = 1 + 1 + 6 */

    /*
    *insert client ip in tcp option, now only support IPV4,
    *must be 4 bytes alignment.
    */
    struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
    }; 
Linux 커널은 소켓을 수신하는 동안 3방향 핸드 셰이크의 ACK 패키지를 받는 경우, `SYN_REVC` 상태에서 `TCP_ESTABLISHED` 상태로 전환합니다. 이때 커널은 `tcp_v4_syn_recv_sock` 함수를 호출합니다. Hook 함수 `tcp_v4_syn_recv_sock_toa `는 기존의 ` tcp_v4_syn_recv_sock ` 함수를 우선적으로 호출한 뒤, `get_toa_data` 함수를 호출하여 TCP OPTION에서 TOA OPTION을 추출한 후에 `sk_user_data` 필드에 저장합니다.

`inet_getname_toa hook inet_getname`을 이용하여 오리진 IP 주소와 포트를 획득할 때, 기존의 `inet_getname`을 우선적으로 호출한 뒤, `sk_user_data`가 공백 여부를 판단합니다. 그 중 실제 IP와 포트를 추출한 데이터가 있다면 `inet_getname`의 반환값을 대체합니다.

클라이언트 프로그램은 사용자 상태에서 getpeername을 호출하고 반환한 IP와 포트는 클라이언트의 기존 IP가 됩니다.

## 커널 패키지 설치 절차
### Centos 6.x/7.x
설치 절차

1. 설치 패키지 다운로드
 (1) [Centos 6.x 다운로드](http://toakernel-1253438722.cossh.myqcloud.com/kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm)
 (2) [Centos 7.x 다운로드](http://toakernel-1253438722.cossh.myqcloud.com/kernel-3.10.0-693.el7.centos.toa.x86_64.rpm)
2. 패키지 파일 설치
							
			rpm -hiv kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm --force						
3. 설치 후 CVM 다시 시작

			reboot
4. 명령을 실행하여 toa 모듈 로딩 성공 여부 검사

			lsmod | grep toa
5. 로딩하지 않았다면 수동 시작
    
			modprobe toa
6. 다음 명령으로 toa 모듈 자동 로딩 활성화 가능

			echo “modprobe toa” >> /etc/rc.d/rc.local
			
###  Ubuntu 16.04
설치 패키지 다운로드:
(1) [커널 패키지 다운로드](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-4.4.87.toa_1.0_amd64.deb )
(2) [커널 header 패키지 다운로드](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-4.4.87.toa_1.0_amd64.deb)
설치 절차:

			dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
헤더 패키지는 설치하지 않아도 되며, 관련 개발이 필요한 경우 설치하십시오.
설치한 후에 CVM을 다시 시작하며,` lsmod | grep toa `로 toa 모듈 로딩 여부를 검사합니다. 로딩되지 않았다면 `modprobe toa`로 시작합니다.
다음 명령으로 toa 모듈 로딩을 시작합니다.
		
		echo “modprobe toa” >> /etc/rc.d/rc.local
		 
### Debian 8

(1) [커널 패키지 다운로드](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-3.16.43.toa_1.0_amd64.deb)
(2) [커널 header 패키지 다운로드](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-3.16.43.toa_1.0_amd64.deb)

설치 방법은 Ubuntu와 동일합니다.


비즈니스 서버인 Linux 운영 체제의 유형과 버전에 따라 그에 맞는 커널 패키지를 다운로드하고 다음 절차에 따라 조작하십시오. 사용자 운영 체제와 일치하는 커널 패키지가 없는 경우, 사용자는 다음 TOA 오리진 코드를 참조하여 가이드 작업을 설치할 수 있습니다.

## TOA 오리진 코드 커널 설치 가이드

### 오리진 코드 설치

1. [toa 패치](http://kb.linuxvirtualserver.org/images/3/34/Linux-2.6.32-220.23.1.el6.x86_64.rs.src.tar.gz)가 있는 오리진 코드 패키지를 다운로드하고 toa 패치를 클릭하면 설치 패키지를 다운로드할 수 있습니다.
2. 압축을 해제합니다.
3. .config를 편집하고 `CONFIG_IPV6=M`이 `CONFIG_IPV6=y`로 변경됩니다.
4. 사용자 지정 설명을 추가해야 할 경우, Makefile을 편집할 수 있습니다.
5. make -jn(n은 스레드 수입니다).
6. `make modules_install`'
7. `make install`'
8. /Boot/grub/menu.lst를 수정하고 default가 새로 설치한 커널(title 순서는 0에서 시작)로 변경됩니다.
9. 다시 시작하면 toa 커널이 됩니다.
10. `lsmode | grep toa`로 toa 모듈 로딩 여부를 검사합니다. 로딩되지 않았다면 `modprobe toa`로 시작합니다.

### 커널 패키지 제작

rpm 패키지를 직접 제작할 수 있고, 당사가 제공할 수도 있습니다.

1. kernel-2.6.32-220.23.1.el6.src.rpm 설치 

			rpm -hiv kernel-2.6.32-220.23.1.el6.src.rpm
2. 커널 오리진 코드 디렉터리 생성

			rpmbuild -bp ~/rpmbuild/SPECS/kernel.spec
3. 오리진 코드 디렉터리 1개 복사

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/ cp -a linux-2.6.32-220.23.1.el6.x86_64/ linux-2.6.32-220.23.1.el6.x86_64_new   
4. 복사한 오리진 코드 디렉터리에서 toa 패치 제작

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64_new/ 
			patch -p1 < /usr/local/src/linux-2.6.32-220.23.1.el6.x86_64.rs/toa-2.6.32-220.23.1.el6.patch
5. .config를 편집하여 SOURCE 디렉터리로 복사

			sed -i 's/CONFIG_IPV6=m/CONFIG_IPV6=y/g' .config 
			echo -e '\n# toa\nCONFIG_TOA=m' >> .config
			cp .config ~/rpmbuild/SOURCES/config-x86_64-generic
6. 기존 오리진 코드의 .config 삭제

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64 
			rm -rf .config
7. 최종 패치 생성
    
			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
			diff -uNr linux-2.6.32-220.23.1.el6.x86_64 linux-2.6.32-220.23.1.el6.x86_64_new/ >
			~/rpmbuild/SOURCES/toa.patch
8. kernel.spec 편집

    vim ~/rpmbuild/SPECS/kernel.spec
ApplyOptionPath에서 다음 내용(buildid 등 사용자 지정 커널 패키지 이름 수정 가능) 추가 

			Patch999999: toa.patch
    ApplyOptionalPatch toa.patch
9. rpm 패키지 제작

			rpmbuild -bb --with baseonly --without kabichk --with firmware --without debuginfo --target=x86_64 ~/rpmbuild/SPECS/kernel.spec
10. 커널 rpm 패키지 설치
		 rpm -hiv kernel-xxxx.rpm --force
	 
다시 시작, toa 모듈 로딩






