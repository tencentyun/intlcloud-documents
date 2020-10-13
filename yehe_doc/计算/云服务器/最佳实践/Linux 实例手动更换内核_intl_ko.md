## 작업 시나리오
Bottleneck Bandwidth and Round-trip propagation time(BBR)은 Google사에서 2016년에 개발한 TCP 혼잡 방지 알고리즘으로, Linux 서버의 처리량을 눈에 띄게 향상하며 TCP 연결의 딜레이를 현저히 축소하는 기능을 갖고 있습니다. BBR 실행을 위해서는 4.10 이상의 Linux 커널(Kernel) 버전이 필요하므로, 버전이 4.10 이하라면 본 문서를 참조하여 작업하실 수 있습니다. 본 문서는 Linux 시스템에서 커널의 수동 변경을 통해 BBR을 실행하는 방법에 관해 소개합니다.

## 작업 순서

### 커널 패키지 없데이트
1. 다음 명령어를 실행하여 현재의 커널 버전을 확인합니다.
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


### 새 커널 설치
1. 다음 명령어를 실행하여 ELRepo 리포지토리에서 현재 시스템이 지원하는 커널 패키지를 확인합니다.
```
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
```
2. 다음 명령어를 실행하여 안정적인 최신 메인라인 커널을 설치합니다.
```
yum --enablerepo=elrepo-kernel install kernel-ml
```

### grub 설정 변경
1. 다음 명령어를 실행하여 `/etc/default/grub` 파일을 엽니다.
```
vim /etc/default/grub
```
2. "**i**"를 눌러 편집 모드로 바꾸고, `GRUB_DEFAULT=saved`를 `GRUB_DEFAULT=0`으로 수정합니다.
![](https://main.qcloudimg.com/raw/484e7a6e818dc44c2d4debb9230e0b46.png)
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장한 뒤 돌아갑니다.
4. 다음 명령어를 실행하여 커널 구성을 다시 생성합니다.
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
5. 다음 명령어를 실행하여 시스템을 재시작합니다.
```
reboot
```
6. 다음 명령어를 실행하여 제대로 수정되었는지 확인합니다.
```
uname -r
```

### 여분 커널 삭제
1. 다음 명령어를 실행하여 모든 커널 버전을 확인합니다.
```
rpm -qa | grep kernel
```
2. 다음 명령어를 실행하여 옛 버전의 커널을 삭제합니다.
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
2. "**i**"를 눌러 편집 모드로 바꾸고, 다음 콘텐츠를 추가합니다.
```
net.core.default_qdisc=fq
net.ipv4.tcp_congestion_control=bbr
```
3. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장한 뒤 돌아갑니다.
4. 다음 명령어를 실행하여 `/etc/sysctl.conf` 구성 파일에서 커널 매개변수 설정을 로딩합니다.
```
sysctl -p
```
5. 다음 명령어를 순서대로 실행하여 BBR이 제대로 실행되는지 확인합니다.
```
sysctl net.ipv4.tcp_congestion_control
# 아래의 콘텐츠가 표시되면 됩니다.
# net.ipv4.tcp_congestion_control = bbr
```
```
sysctl net.ipv4.tcp_available_congestion_control
# 아래의 콘텐츠가 표시되면 됩니다.
# net.ipv4.tcp_available_congestion_control = reno cubic bbr
```
6. 다음 명령어를 실행하여 커널 모듈이 로딩되고 있는지 확인합니다.
```
lsmod | grep bbr
```
다음과 같은 정보가 출력되면 성공적으로 실행되었음을 의미합니다.
![](https://main.qcloudimg.com/raw/7d736afd8ce22f421315e149a86527e5.png)



