
## 작업 시나리오

Cloud-init은 주로 인스턴스 최초 초기화 시의 사용자 정의 설정 기능을 제공합니다. 가져온 이미지에 cloud-init 서비스가 설치되어 있지 않으면, 해당 이미지를 기반으로 실행한 인스턴스의 정상적인 초기화가 불가능하여 해당 이미지 가져오기에 실패하게 됩니다. 본 문서는 cloud-init 서비스 설치에 대해 안내합니다.
cloud-init 설치는 아래의 두 가지 방식을 추천드립니다.
- [cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown)을 통해 
- [소프트웨어 보관소의 cloud-init 패키지를 사용하는 방식](#SoftSources)을 통해

## 주의 사항
Linux 시스템의 이미지를 가져오기 전에, 이미지 내부에 cloud-init 서비스가 바르게 설치되었는지 확인하시기 바랍니다.

## 전제 조건
cloud-init을 설치할 서버가 외부 네트워크에 정상적으로 액세스할 수 있어야 합니다.

## 작업 단계
<dx-tabs>
::: \scloud-init\s 소스 패키지 수동 다운로드[](id:ManualDown)

### cloud-init 소스 패키지 다운로드

<dx-alert infotype="explain" title="">
- 정상 설치된 cloud-init-17.1 버전이 Tencent Cloud와 최적의 호환성을 가지므로, 해당 버전의 이미지를 사용해 CVM을 생성하면 모든 구성 옵션이 정상적으로 초기화됩니다. 따라서 **cloud-init-17.1.tar.gz** 버전 설치를 권장하며, 다른 버전의 cloud-init 소스 패키지도 [다운로드](https://launchpad.net/cloud-init/+download)하실 수 있습니다. 본 문서는 cloud-init-17.1 버전을 예시로 사용합니다.
- cloud-init-17.1 또는 다른 버전의 cloud-init 소스 패키지를 설치할 수 없다면 [포터블 버전 cloud-init 패키지 수동 다운로드 방식](#greeninitCloudInit)을 통해 설치할 수 있습니다.
</dx-alert>


다음 명령어를 실행하여 cloud-init 소스 패키지를 다운로드합니다.
```shellsession
wget https://launchpad.net/cloud-init/trunk/17.1/+download/cloud-init-17.1.tar.gz
```

### cloud-init 설치
1. 다음 명령어를 실행하여 cloud-init 설치 패키지를 압축 해제합니다.
<dx-alert infotype="explain" title="">
사용 중인 운영 체제가 Ubuntu라면 root 계정으로 전환하시기 바랍니다.
</dx-alert>
```shellsession
tar -zxvf cloud-init-17.1.tar.gz 
```
2. 다음 명령어를 실행하여 압축 해제한 cloud-init 설치 패키지 디렉터리(즉 cloud-init-17.1 디렉터리)로 이동합니다.
```shellsession
cd cloud-init-17.1
```
3. 운영 체제 버전에 맞는 Python-pip를 설치합니다.
    - CentOS 6/7 시리즈에서는 다음 명령어를 실행합니다.
    ```shellsession
    yum install python3-pip -y
    ```
    - Ubuntu 시리즈에서는 다음 명령어를 실행합니다.
    ```shellsession
    apt-get -y install python3-pip
    ```
설치 과정에서 설치할 수 없거나 설치 패키지를 찾지 못하는 오류가 발생하는 경우, [Python-pip을 설치할 수 없는 문제 해결](#updateSoftware)을 참조하여 처리하시기 바랍니다.
4. 다음 명령을 실행하여 pip를 업그레이드합니다.
```
python3 -m pip install --upgrade pip
```
5. 다음 명령어를 실행하여 종속 패키지를 설치합니다.
<dx-alert infotype="notice" title="">
Cloud-init 종속 모듈 requests 2.20.0 버전 이후부터 Python2.6을 사용하지 않습니다. 이미지 환경의 Python 인터프리터가 Python2.6 이하일 경우, cloud-init 종속 패키지 설치 전에 `pip install 'requests&lt;2.20.0'` 명령어를 실행하여 requests 2.20.0 이하 버전을 설치하시기 바랍니다.
</dx-alert>
```shellsession
pip3 install -r requirements.txt
```

6. 운영 체제 버전에 따라 cloud-utils 모듈을 설치합니다.
    - CentOS 6 시리즈에서는 다음 명령어를 실행합니다.
    ```shellsession
    yum install cloud-utils-growpart dracut-modules-growroot -y
    dracut -f
    ```
    - CentOS 7 시리즈에서는 다음 명령어를 실행합니다.
    ```shellsession
    yum install cloud-utils-growpart -y
    ```
    - Ubuntu 시리즈에서는 다음 명령어를 실행합니다.
    ```shellsession
    apt-get install cloud-guest-utils -y
    ```

7 다음 명령어를 실행하여 cloud-init을 설치합니다.
```shellsession
python3 setup.py build
```
```shellsession
python3 setup.py install --init-system systemd
```

<dx-alert infotype="notice" title="">
--init-system 의 선택 가능한 매개변수에는 (systemd, sysvinit, sysvinit_deb, sysvinit_freebsd, sysvinit_openrc, sysvinit_suse, upstart)  [default: None]이 있습니다. 현재 운영 체제가 사용하고 있는 자동 실행 서비스 관리 방식에 따라 선택하시기 바랍니다. 잘못 선택할 경우 시작 시 cloud-init 서비스를 자동 실행할 수 없습니다. 본 문서는 systemd 자동 실행 서비스 관리를 예시로 사용합니다.
</dx-alert>


[](id:cloud-init)
### cloud-init 구성 파일 수정

1. 운영 체제에 따라 적합한 cloud.cfg를 다운로드합니다.
    - Ubuntu 운영 체제의 cloud.cfg [다운로드](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg).
    - CentOS 운영 체제의 cloud.cfg [다운로드](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg).
2. `/etc/cloud/cloud.cfg`의 콘텐츠를 다운로드한 cloud.cfg 파일의 콘텐츠로 대체합니다.


### syslog 사용자 추가
다음 명령어를 실행하여 syslog 사용자를 추가합니다.
```shellsession
useradd syslog
```

### 시작 시 cloud-init 서비스 자동 실행 설정
- **운영 체제가 systemd 자동 실행 관리 서비스인 경우 다음 명령어를 실행하여 설정합니다.**
<dx-alert infotype="explain" title="">
`strings /sbin/init | grep "/lib/system"` 명령을 수행할 수 있습니다. 반환되는 메시지가 있을 경우 운영 체제는 systemd 자동 실행 관리 서비스입니다.
</dx-alert>

- **Ubuntu 또는 Debian 운영 체제에서는 다음 명령어를 실행해야 합니다.**
```shellsession
 ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init 
```

- **모든 운영 체제에서는 다음 명령어를 실행해야 합니다.**
```shellsession
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

- **CentOS 및 Redhat 운영 체제에서는 다음 명령어를 실행해야 합니다.**
 /lib/systemd/system/cloud-init-local.service 파일을 다음 콘텐츠로 대체합니다.
```shellsession
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
```shellsession
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
<dx-alert infotype="explain" title="">
`strings /sbin/init | grep "sysvinit"` 명령을 수행할 수 있습니다. 반환되는 메시지가 있을 경우 운영 체제는 sysvinit 자동 실행 관리 서비스입니다.
</dx-alert>
```shellsession
chkconfig --add cloud-init-local
chkconfig --add cloud-init
chkconfig --add cloud-config
chkconfig --add cloud-final
chkconfig cloud-init-local on 
chkconfig cloud-init on 
chkconfig cloud-config on 
chkconfig cloud-final on 
```
:::
::: 소프트웨어 소스에서 \scloud-init\s 패키지 사용[](id:SoftSources)
### cloud-init 설치

다음 명령어를 실행하여 cloud-init을 설치합니다.
```shellsession
apt-get/yum install cloud-init
```
<dx-alert infotype="explain" title="">
apt-get 또는 yum 명령어를 통해 설치한 cloud-init은 현재 운영 체제에서 설정한 소프트웨어 보관소의 기본 cloud-init 버전을 기본값으로 하고 있습니다. 해당 방식으로 설치한 이미지로 생성한 인스턴스의 일부 설정 옵션 초기화가 예상과 다를 수 있으므로 [cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown)으로 설치하시길 권장합니다.
</dx-alert>



### cloud-init 구성 파일 수정
1. 운영 체제에 따라 적합한 cloud.cfg를 다운로드합니다.
   - Ubuntu 운영 체제의 cloud.cfg [다운로드](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/ubuntu/cloud.cfg).
   - CentOS 운영 체제의 cloud.cfg [다운로드](https://cloudinit-1251783334.cos.ap-guangzhou.myqcloud.com/centos/cloud.cfg).
2. `/etc/cloud/cloud.cfg`의 콘텐츠를 다운로드한 cloud.cfg 파일의 콘텐츠로 대체합니다.
:::
</dx-tabs>



## 관련 작업


<dx-alert infotype="notice" title="">
아래의 작업을 완료한 후 서버를 재시작할 경우 해당 작업을 다시 실행해야 하므로 서버 재시작을 삼가 주시기 바랍니다.
</dx-alert>


1. 다음 명령어를 실행하여 cloud-init 관련 설정에 성공했는지 점검합니다.
```shellsession
cloud-init init --local
```
다음과 유사한 정보가 반환되면 cloud-init가 성공적으로 설정된 것입니다.
```shellsession
Cloud-init v. 17.1 running 'init-local' at Fri, 01 Apr 2022 01:26:11 +0000. Up 38.70 seconds.
```
2. 다음 명령어를 실행하여 cloudinit의 캐시 기록을 삭제합니다.
```shellsession
rm -rf /var/lib/cloud
```
3. Ubuntu 또는 Debian 운영 체제에서는 다음 명령어를 실행해야 합니다.
``` shellsession
rm -rf /etc/network/interfaces.d/50-cloud-init.cfg
```
4. Ubuntu 또는 Debian 운영 체제에서는 `/etc/network/interfaces`을 다음 콘텐츠로 수정해야 합니다.
```shellsession
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).
source /etc/network/interfaces.d/*
```

## 부록
[](id:greeninitCloudInit)
### 포터블 버전 cloud-init 패키지 수동 다운로드 방식
[cloud-init 소스 패키지 수동 다운로드 방식](#ManualDown)으로 설치할 수 없을 경우, 다음 작업을 통해 설치할 수 있습니다.
1. 다음 명령을 실행하여 `/usr/local` 디렉터리로 전환합니다.
```shellsession
cd /usr/local
```
2. 포터블 버전 cloud-init 패키지를 [다운로드](https://image-tools-1251783334.cos.ap-guangzhou.myqcloud.com/greeninit-x64-beta.tgz)합니다. 다운로드한 설치 패키지를 `/usr/lcoal` 디렉터리에 업로드합니다.
>!참고: 설치 디렉터리는 반드시 시스템 디스크 디렉터리여야 하며 파일 시스템 간 교차할 수 없으므로 `/usr/local` 디렉터리에 설치하는 것이 좋습니다
3. 다음 명령어를 실행하여 포터블 버전 cloud-init 패키지를 압축 해제합니다.
```shellsession
tar xvf greeninit-x64-beta.tgz 
```
4. 다음 명령어를 실행하여 압축 해제한 포터블 버전 cloud-init 설치 패키지의 디렉터리(greeninit 디렉터리)로 이동합니다.
```shellsession
cd greeninit
```
5. 다음 명령어를 실행하여 cloud-init을 설치합니다.
```shellsession
sh install.sh 
```
[](id:updateSoftware)
### Python-pip을 설치할 수 없는 문제 해결
Python-pip 설치 과정에서 설치할 수 없거나 설치 패키지를 찾지 못하는 오류가 발생하는 경우, 실제 사용 중인 운영 체제에 맞게 아래의 순서를 참고하여 처리하시기 바랍니다.
<dx-tabs>
::: CentOS\s6/7 시리즈 예시
  1. 다음 명령어를 실행하여 EPEL 저장소를 설정합니다.
```shellsession
yum install epel-release -y
```
  2. 다음 명령어를 실행하여 Python-pip을 설치합니다.
```shellsession
yum install python3-pip -y
```
:::
::: Ubuntu\s 예시
  1. 다음 명령을 실행하여 캐시를 삭제합니다.
```shellsession
apt-get clean all
```
  1. 다음 명령을 실행하여 소프트웨어 패키지 리스트를 업데이트하십시오.
```shellsession
apt-get update -y
```
  2. 다음 명령을 실행하여 Python-pip을 설치합니다.
```shellsession
apt-get -y install python3-pip
```
:::
</dx-tabs>
