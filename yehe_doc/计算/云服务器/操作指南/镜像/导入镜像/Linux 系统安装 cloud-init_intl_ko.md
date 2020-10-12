## 작업 시나리오

Cloud-init은 주로 인스턴스 최초 초기화 시의 사용자 정의 설정 기능을 제공합니다. 가져온 이미지에 cloud-init 서비스가 설치되어 있지 않으면, 해당 이미지를 기반으로 실행한 인스턴스의 정상적인 초기화가 불가능하여 해당 이미지 가져오기에 실패하게 됩니다. 본 문서는 cloud-init 서비스 설치에 대해 안내합니다.
cloud-init 설치는 아래의 두 가지 방식을 추천해 드립니다.
- [cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown) 
- [소프트웨어 보관소의 cloud-init 패키지를 사용하는 방식](#SoftSources)

## 주의 사항
Linux 시스템의 이미지를 가져오기 전에, 이미지 내부에 cloud-init 서비스가 바르게 설치되었는지 확인하시기 바랍니다.

## 전제 조건
cloud-init을 설치할 서버가 외부 네트워크에 정상적으로 액세스할 수 있어야 합니다.

## 작업 순서

<span id="ManualDown"></span>
### cloud-init 소스 패키지 수동 다운로드 방식

#### cloud-init 소스 패키지 다운로드
>?  
> - 정상적으로 설치된 cloud-init-17.1 버전이 Tencent Cloud와 최적의 호환성을 가지므로, 해당 버전의 이미지를 사용해 CVM을 생성하면 모든 설정 항목이 정상적으로 초기화됩니다. 따라서 **cloud-init-17.1.tar.gz** 설치 버전을 권장하며, 다른 버전의 cloud-init 소스 패키지도 [다운로드](https://launchpad.net/cloud-init/+download)하실 수 있습니다. 본 문서는 cloud-init-17.1 버전을 예시로 사용합니다.
> - cloud-init-17.1 또는 다른 버전의 cloud-init 소스 패키지를 설치할 수 없다면 [포터블 버전 cloud-init 패키지 수동 다운로드 방식](#greeninitCloudInit)을 통해 설치할 수 있습니다.
>
다음 명령어를 실행하여 cloud-init 소스 패키지를 다운로드합니다.
```
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

#### cloud-init 설치
1. 다음 명령어를 실행하여 cloud-init 설치 패키지를 압축 해제합니다.
>? 사용하는 운영 체제가 Ubuntu이면 root 계정으로 전환하세요.
>
```
tar -zxvf cloud-init-17.1.tar.gz 
```
2. 다음 명령어를 실행하여 압축 해제한 cloud-init 설치 패키지 디렉터리(즉 cloud-init-17.1 디렉터리)로 이동합니다.
```
cd cloud-init-17.1
```
3. 운영 체제 버전에 맞는 Python-pip을 설치합니다.
 - CentOS 6/7 시리즈에서는 다음 명령어를 실행합니다.
```
yum install python-pip -y
```
 - Ubuntu 시리즈에서는 다음 명령어를 실행합니다.
```
apt-get install python-pip -y
```
설치하는 과정에서 설치할 수 없거나 설치 패키지를 찾지 못하는 오류가 발생하면, [Python-pip을 설치할 수 없는 문제 해결](#updateSoftware)을 참조하여 처리하시기를 바랍니다.
4. 다음 명령어를 실행하여 종속 패키지를 설치합니다.
>!  Cloud-init 종속 모듈 requests 2.20.0 버전 이후부터 Python2.6을 사용하지 않습니다. 이미지 환경의 Python 인터프리터가 Python2.6 이하일 경우, cloud-init 종속 패키지 설치 전에 `pip install ’requests<2.20.0’` 명령어를 실행하여 requests 2.20.0 이하 버전을 설치하시기 바랍니다.
>
```
pip install -r requirements.txt
```
4. 운영 체제 버전에 따라 cloud-utils 모듈을 설치합니다.
 - CentOS 6 시리즈에서는 다음 명령어를 실행합니다.
```
yum install cloud-utils-growpart dracut-modules-growroot -y
dracut -f
```
 - CentOS 7 시리즈에서는 다음 명령어를 실행합니다.
```
yum install cloud-utils-growpart -y
```
 - Ubuntu 시리즈에서는 다음 명령어를 실행합니다.
```
apt-get install cloud-guest-utils -y
```
5. 다음 명령어를 실행하여 cloud-init을 설치합니다.
```
python setup.py build
python setup.py install --init-system systemd
```
>! --init-system 의 선택 가능한 매개변수에는 (systemd, sysvinit, sysvinit_deb, sysvinit_freebsd, sysvinit_openrc, sysvinit_suse, upstart)  [default: None] 이 있습니다. 현재 운영 체제가 사용하고 있는 자동 실행 서비스 관리 방식에 따라 선택하세요. 선택에 오류가 있으면 cloud-init 서비스가 부팅 시 자동 실행될 수 없습니다. 본 문서는 systemd 자동 실행 서비스 관리를 예시로 사용합니다.

#### cloud-init 구성 파일 수정

1. 운영 체제에 따라 적합한 cloud.cfg를 다운로드합니다.
 - Ubuntu 운영 체제의 cloud.cfg [다운로드](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg).
 - CentOS 운영 체제의 cloud.cfg [다운로드](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg).
2. `/etc/cloud/cloud.cfg`의 콘텐츠를 다운로드받은 cloud.cfg 파일의 콘텐츠로 대체합니다.

#### syslog 사용자 추가
다음 명령어를 실행하여 syslog 사용자를 추가합니다.
```
useradd syslog
```

#### cloud-init 서비스의 부팅 시 자동 실행 설정
- **운영 체제가 systemd 자동 실행 관리 서비스인 경우 다음 명령어를 실행하여 설정합니다.**
 1. **Ubuntu 또는 Debian 운영 체제에서는 다음 명령어를 실행해야 합니다.**
```
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```
 2. **모든 운영 체제에서는 다음 명령어를 실행해야 합니다.**
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
 3. **CentOS 및 Redhat 운영 체제에서는 다음 명령어를 실행해야 합니다.**
 /lib/systemd/system/cloud-init-local.service 파일을 다음 콘텐츠로 대체합니다.
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
/lib/systemd/system/cloud-init.service 파일을 다음 콘텐츠로 대체합니다.
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

다음 명령어를 실행하여 cloud-init을 설치합니다.
```
apt-get/yum install cloud-init
```
>? apt-get 또는 yum 명령어를 실행하여 설치한 cloud-init는 현재 운영 체제에서 설정한 소프트웨어 보관소의 기본 cloud-init 버전을 기본 값으로 하고 있습니다. 해당 방식으로 설치한 이미지로 생성한 인스턴스의 경우, 일부 설정 항목 초기화가 예상과 다를 수 있어 [cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown)을 사용해 설치하시기를 권장합니다.
>

#### cloud-init 구성 파일 수정
1. 운영 체제에 따라 적합한 cloud.cfg를 다운로드합니다.
 - Ubuntu 운영 체제의 cloud.cfg [다운로드](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg).
 - CentOS 운영 체제의 cloud.cfg [다운로드](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg).
2. `/etc/cloud/cloud.cfg`의 콘텐츠를 다운로드받은 cloud.cfg 파일의 콘텐츠로 대체합니다.

## 관련 작업
>! 아래의 작업을 실행 완료한 후 서버를 재시작하지 마세요. 그렇지 않은 경우 아래의 작업을 다시 실행해야 합니다.
>
1. 다음 명령어를 실행하여 cloud-init 관련 설정에 성공하였는지 점검합니다.
```
cloud-init init --local
rm -rf /var/lib/cloud
```
2. Ubuntu 또는 Debian 운영 체제에서는 다음 명령어를 실행해야 합니다.
```
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
3. Ubuntu 또는 Debian 운영 체제에서는 `/etc/network/interfaces`을 다음 콘텐츠로 수정해야 합니다.
```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## 부록

<span id="greeninitCloudInit"></span>
### 포터블 버전 cloud-init 패키지 수동 다운로드 방식
[cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown)으로 설치할 수 없다면, 다음 작업을 통해 설치할 수 있습니다.
1. 포터블 버전 cloud-init 패키지를 [다운로드](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz)합니다.
2. 다음 명령어를 실행하여 포터블 버전 cloud-init 패키지를 압축 해제합니다.
```
tar xvf greeninit-x64-beta.tgz 
```
3. 다음 명령어를 실행하여 압축 해제한 포터블 버전 cloud-init 설치 패키지의 디렉터리(greeninit 디렉터리)로 이동합니다.
```
cd greeninit
```
4. 다음 명령어를 실행하여 cloud-init을 설치합니다.
```
sh install.sh 
```

<span id="updateSoftware"></span>
### Python-pip을 설치할 수 없는 문제 해결
Python-pip을 설치하는 과정에서 설치할 수 없거나 설치 패키지를 찾지 못하는 오류가 발생하면, 실제 사용 중인 운영 체제에 맞게 아래의 순서를 참조하여 처리하시기를 바랍니다.
- CentOS 6/7 예시:
  1. 다음 명령어를 실행하여 EPEL 저장소를 설정합니다.
```
yum install epel-release -y
```
  2. 다음 명령어를 실행하여 Python-pip을 설치합니다.
```
yum install python-pip -y
```
- Ubuntu 예시:
  1. 다음 명령어를 실행하여 소프트웨어 패키지 리스트를 업데이트합니다.
```
apt-get update -y
```
  2. 다음 명령어를 실행하여 Python-pip을 설치합니다.
```
apt-get install python-pip -y
```


