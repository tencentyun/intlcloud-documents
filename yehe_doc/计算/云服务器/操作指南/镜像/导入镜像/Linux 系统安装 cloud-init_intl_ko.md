## 작업 시나리오

Cloud-init 는 인스턴스 최초 초기화 시의 사용자 정의 설정 기능을 제공합니다. 가져온 이미지에 cloud-init 서비스가 설치되어 있지 않으면, 해당 이미지를 기반으로 실행한 인스턴스가 정상적으로 초기화될 수 없으므로 해당 이미지 가져오기에 실패하게 됩니다. 본 문서는 cloud-init 서비스 설치에 관해 안내합니다.
cloud-init 설치는 아래의 두 가지 방식을 추천드립니다.
- [cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown)을 통해 
- [소프트웨어 보관소 상의 cloud-init 패키지를 사용하는 방식](#SoftSources)을 통해

## 주의 사항
Linux 시스템의 이미지를 가져오기 전, 이미지 내부에 cloud-init 서비스가 바르게 설치되었는지 확인하세요.

## 전제 조건
cloud-init를 설치할 서버가 외부 네트워크에 정상적으로 액세스할 수 있어야 합니다.

## 작업 순서

<span id="ManualDown"></span>
### cloud-init 소스 패키지 수동 다운로드 방식

#### cloud-init 소스 패키지 다운로드
>  
> - 정상적으로 설치된 상황에서 cloud-init-17.1 버전이 Tencent Cloud와 최적의 호환성을 갖고 있어, 해당 버전의 이미지로 생성해야 CVM의 모든 설정 옵션이 정상적으로 초기화될 수 있습니다. 그러므로 **cloud-init-17.1.tar.gz** 설치 버전을 권장합니다. 사용자는 [다운로드](https://launchpad.net/cloud-init/+download)하여 기타 버전의 cloud-init 소스 패키지를 획득할 수 있습니다. 본 문서는 cloud-init-17.1 버전을 예시로 사용합니다.
> - cloud-init-17.1 또는 기타 버전의 cloud-init 소스 패키지를 설치할 수 없다면 [그린 버전 cloud-init 패키지 수동 다운로드 방식](#greeninitCloudInit)을 통해 설치할 수 있습니다.
>
다음 명령어를 실행하여 cloud-init 소스 패키지를 다운로드합니다.
```
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

#### cloud-init 설치
1. 다음 명령어를 실행하여 cloud-init 설치 패키지를 압축 해제합니다.
> 사용하는 운영 체제가 Ubuntu이면 root 계정으로 전환하세요.
>
```
tar -zxvf cloud-init-17.1.tar.gz 
```
2. 다음 명령어를 실행하여 압축 해제한 cloud-init 설치 패키지 디렉터리(즉 cloud-init-17.1 디렉터리)로 들어갑니다.
```
cd cloud-init-17.1
```
3. 운영 체제 버전에 따라 Python-pip를 설치합니다.
 - CentOS 6/7 시리즈는 다음 명령어를 실행합니다.
```
yum install python-pip -y
```
 - Ubuntu 시리즈는 다음 명령어를 실행합니다.
```
apt-get install python-pip -y
```
4. 다음 명령어를 실행하여 종속 패키지를 설치합니다.
>  Cloud-init 종속 모듈 requests 2.20.0 버전 이후부터 Python2.6 을 사용하지 않습니다. 이미지 환경의 Python 인터프리터가 Python2.6 및 이하일 경우, cloud-init 종속 패키지 설치 전에 `pip install ’requests<2.20.0’` 명령어를 실행하여 requests 2.20.0 이하 버전을 설치하세요.
>
```
pip install -r requirements.txt
```
4. 운영 체제 버전에 따라 cloud-utils 모듈을 설치합니다.
 - CentOS 6 시리즈는 다음 명령어를 실행합니다.
```
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
 - CentOS 7 시리즈는 다음 명령어를 실행합니다.
```
yum install cloud-utils-growpart -y
```
 - Ubuntu 시리즈는 다음 명령어를 실행합니다.
```
apt-get install cloud-guest-utils -y
```
5. 다음 명령어를 실행하여 cloud-init를 설치합니다.
```
python setup.py build
python setup.py install --init-system systemd
```
> --init-system 의 선택 가능한 매개변수에는 (systemd, sysvinit,  sysvinit_deb, sysvinit_freebsd, sysvinit_openrc, sysvinit_suse, upstart)  [default: None] 이 있습니다. 현재 운영 체제가 사용하고 있는 자동 실행 서비스 관리 방식에 따라 선택하세요. 선택에 오류가 있을 경우 cloud-init 서비스를 자동 실행할 수 없습니다. 본 문서는 systemd 자동 실행 서비스 관리를 예시로 사용합니다.

#### cloud-init 구성 파일 수정

1. 각 운영 체제에 따라 cloud.cfg를 다운로드합니다.
 - Ubuntu 운영 체제의 cloud.cfg를 [다운로드](http://cloudinit-1251783334.cosgz.myqcloud.com/ubuntu-cloud.cfg)합니다.
 - CentOS 운영 체제의 cloud.cfg를 [다운로드](http://cloudinit-1251783334.cosgz.myqcloud.com/centos-cloud.cfg)합니다.
2. `/etc/cloud/cloud.cfg`의 내용을 다운로드 완료한 cloud.cfg 파일 내용으로 대체합니다.

#### syslog 사용자 추가
다음 명령어를 실행하여 syslog 사용자를 추가합니다.
```
useradd syslog
```

#### 시작 시 cloud-init 서비스 자동 실행 설정
- **운영 체제가 systemd 자동 실행 관리 서비스인 경우 다음 명령어를 실행하여 설정합니다.**
 1. **Ubuntu 또는 Debian 운영 체제에 대해 다음 명령어를 실행해야 합니다.**
```
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **모든 운영 체제는 다음 명령어를 실행해야 합니다.**
```
systemctl enable cloud-init-local.service 
systemctl start cloud-init-local.service
systemctl enable cloud-init.service
systemctl start cloud-init.service
systemctl enable cloud-config.service
systemctl start cloud-config.service
systemctl enable cloud-final.service
systemctl start cloud-final.service
systemctl status cloud-init-local.service
systemctl status cloud-init.service
systemctl status cloud-config.service
systemctl status cloud-final.service
```
 3. **CentOS 와 Redhat 운영 체제에 대해 다음 명령어를 실행해야 합니다.**
 /lib/systemd/system/cloud-init-local.service 파일을 다음 내용으로 대체합니다.
```
[Unit]
Description=Initial cloud-init job (pre-networking)
Wants=network-pre.target
After=systemd-remount-fs.service
Before=NetworkManager.service
Before=network-pre.target
Before=shutdown.target
Conflicts=shutdown.target
RequiresMountsFor=/var/lib/cloud
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init --local
ExecStart=/bin/touch /run/cloud-init/network-config-ready
RemainAfterExit=yes
TimeoutSec=0
# Output needs to appear in instance console output
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
/lib/systemd/system/cloud-init.service 파일을 다음 내용으로 대체합니다.
```
[Unit]
Description=Initial cloud-init job (metadata service crawler)
Wants=cloud-init-local.service
Wants=sshd-keygen.service
Wants=sshd.service
After=cloud-init-local.service
After=systemd-networkd-wait-online.service
After=networking.service
After=systemd-hostnamed.service
Before=network-online.target
Before=sshd-keygen.service
Before=sshd.service
Before=systemd-user-sessions.service
Conflicts=shutdown.target
[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init init
RemainAfterExit=yes
TimeoutSec=0
# Output needs to appear in instance console output
StandardOutput=journal+console
[Install]
WantedBy=cloud-init.target
```
- **운영 체제가 sysvinit 자동 실행 관리 서비스인 경우 다음 명령어를 실행하여 설정합니다.**
```
chkconfig --add cloud-init-local
chkconfig --add cloud-init
chkconfig --add cloud-config
chkconfig --add cloud-final
chkconfig cloud-init-local on 
chkconfig cloud-init on 
chkconfig cloud-config on 
chkconfig cloud-final on 
```


<span id="SoftSources"></span>
### 소프트웨어 보관소의 cloud-init 패키지를 사용하는 방식

#### cloud-init 설치

다음 명령어를 실행하여 cloud-init를 설치합니다.
```
apt-get/yum install cloud-init
```
> apt-get 또는 yum 명령어를 실행하여 설치한 cloud-init 는 현재 운영 체제에서 설정한 소프트웨어 보관소의 기본 cloud-init 버전을 기본 값으로 하고 있습니다. 해당 방식으로 설치한 이미지가 생성한 인스턴스의 경우, 일부 설정 옵션 초기화가 예상과 다를 수 있어 [cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown)을 사용해 설치할 것을 권장합니다.
>

#### cloud-init 구성 파일 수정
1. 각 운영 체제에 따라 cloud.cfg를 다운로드합니다.
 - Ubuntu 운영 체제의 cloud.cfg를 [다운로드](http://cloudinit-1251740579.cosgz.myqcloud.com/ubuntu-cloud.cfg)합니다.
 - CentOS 운영 체제의 cloud.cfg를 [다운로드](http://cloudinit-1251740579.cosgz.myqcloud.com/centos-cloud.cfg)합니다.
2. `/etc/cloud/cloud.cfg`의 내용을 다운로드 완료한 cloud.cfg 파일 내용으로 대체합니다.

## 관련 작업
> 아래의 작업을 실행 완료한 후 서버를 재시작하지 마세요. 그렇지 않은 경우 아래의 작업을 다시 실행해야 합니다.
>
1. 다음 명령어를 실행하여 cloud-init 관련 설정에 성공했는지 점검합니다.
```
cloud-init init --local
rm -rf /var/lib/cloud
```
2. Ubuntu 또는 Debian 운영 체제에 대해 다음 명령어를 실행해야 합니다.
```
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
3. Ubuntu 또는 Debian 운영 체제에 대해 `/etc/network/interfaces`를 다음 내용으로 수정해야 합니다.
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## 부록

<span id="greeninitCloudInit"></span>
### 포터블 버전 cloud-init 패키지 수동 다운로드 방식
[cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown)으로 설치할 수 없다면 다음 작업을 통해 설치할 수 있습니다.
1. 포터블 버전 cloud-init 패키지를 [다운로드](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz)합니다.
2. 다음 명령어를 실행하여 포터블 버전 cloud-init 패키지를 압축 해제합니다.
```
tar xvf greeninit-x64-beta.tgz 
```
3. 다음 명령어를 실행하여 압축 해제한 포터블 버전 cloud-init 설치 패키지 디렉터리(즉 greeninit 디렉터리)로 들어갑니다.
```
cd greeninit
```
4. 다음 명령어를 실행하여 cloud-init를 설치합니다.
```
sh install.sh 
```






