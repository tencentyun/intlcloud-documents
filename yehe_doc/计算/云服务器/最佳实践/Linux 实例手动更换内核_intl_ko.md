## 작업 시나리오
Bottleneck Bandwidth and Round-trip propagation time(BBR)은 Google이 2016년 개발한 TCP 혼합 방지 알고리즘으로 Linux 서버의 처리량을 현저히 향상시키고 TCP 연결 딜레이를 줄일 수 있습니다. BBR을 활성화 하려면 Linux 커널 4.10 이후 버전이 필요하므로, Linux 서버 커널이 4.10 이전 버전이면 이 글을 참고하여 작업을 진행할 수 있습니다.

본문에서는 CentOS 7.5 운영 체제의 CVM을 예로 들어 Linux 시스템에서 수동으로 커널을 교체하고 BBR을 활성화하는 방법을 안내합니다.

## 작업 순서

### 커널 패키지 업데이트
1. 다음 명령어를 실행하여 현재 Kernel 버전을 확인합니다.
```
uname -r
```
2. 다음 명령어를 실행하여 소프트웨어 패키지를 업데이트합니다.
```
yum update -y
```
3. 다음 명령어를 실행하여 ELRepo 공개키를 가져옵니다.
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
```
4. 다음 명령어를 실행하여 ELRepo의 yum 소스를 설치합니다.
```
yum install https://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
```


### 신규 커널 설치
1. 다음 명령어를 실행하여 ELRepo 리포지토리에서 현재 시스템이 지원하는 커널 패키지를 확인합니다.
```
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```
2. 다음 명령어를 실행하여 최신 메인 라인 안정 커널을 설치합니다.
```
yum --enablerepo=elrepo-kernel install kernel-ml
```

### grub 설정 변경
1. 다음 명령어를 실행하여 `/etc/default/grub` 파일을 엽니다.
```
vim /etc/default/grub
```
2. **i**를 눌러 편집 모드로 전환하고 `GRUB_DEFAULT=saved`를 `GRUB_DEFAULT=0`으로 변경합니다.
![](https://main.qcloudimg.com/raw/484e7a6e818dc44c2d4debb9230e0b46.png)
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
4. 다음 명령어를 실행하여 Kernel 구성을 다시 생성합니다.
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
5. 아래의 명령어를 실행하여 시스템을 재시작합니다.
```
reboot
```
6. 다음 명령어를 실행하여 변경 성공 여부를 확인합니다.
```
uname -r
```

### 불필요한 커널 삭제
1. 다음 명령어를 실행하여 모든 Kernel을 조회합니다.
```
rpm -qa | grep kernel
```
2. 다음 명령어를 실행하여 이전 버전의 커널을 삭제합니다.
```
yum remove kernel-old_kernel_version
```
예시:
```
yum remove kernel-3.10.0-957.el7.x86_64
```

### BBR 활성화
1. 다음 명령어를 실행하여 `/etc/sysctl.conf` 파일을 편집합니다.
```
vim /etc/sysctl.conf
```
2. **i**를 눌러 편집 모드로 전환하고 다음을 추가합니다.
```
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
```
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
4. 다음 명령어를 실행하여 `/etc/sysctl.conf` 구성 파일에서 커널 매개변수 설정을 로딩합니다.
```
sysctl -p
```
5. 다음 명령어를 순서대로 실행하여 BBR이 성공적으로 활성화 되었는지 확인합니다.
```
sysctl net.ipv4.tcp_congestion_control
# 설정이 성공적으로 완료되면 다음이 표시됩니다. 
# net.ipv4.tcp_congestion_control = bbr
```
```
sysctl net.ipv4.tcp_available_congestion_control
# 설정이 성공적으로 완료되면 다음이 표시됩니다. 
# net.ipv4.tcp_available_congestion_control = reno cubic bbr
```
6. 다음 명령어를 실행하여 커널 모듈이 로딩되었는지 확인합니다.
```
lsmod | grep bbr
```
다음 정보가 반환되면 성공적으로 활성화된 것입니다.
![](https://main.qcloudimg.com/raw/7d736afd8ce22f421315e149a86527e5.png)



