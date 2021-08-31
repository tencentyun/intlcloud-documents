## 작업 시나리오

[USB/IP](http://usbip.sourceforge.net/)는 하나의 오픈 소스 프로젝트로, 커널이 포함되어 있어 Linux 환경에서 USB/IP를 사용하여 USB 장치를 원격으로 공유할 수 있습니다. 본 문서는 다음의 환경을 예로 들어, USB/IP를 사용한 USB 장치 원격 공유 방법을 소개합니다.
USB Client: CentOS 7.6 운영 체제의 CVM
USB Server: Debian 운영 체제의 로컬 컴퓨터

## 주의 사항
Linux 운영 체제의 릴리스 버전이 다르면 USB/IP 설치 방법과 커널 모듈 이름에 다소 차이가 있을 수 있습니다. 현재 사용하고 있는 Linux 시스템이 USB/IP 기능을 지원하는지 확인하시기 바랍니다.


## 작업 순서

### USB Server 설정

1. 로컬 컴퓨터에서 다음 명령어를 순서대로 실행하여 USB/IP를 설치하고 관련 커널 모듈을 다운로드합니다.
```
sudo apt-get install usbip
sudo modprobe usbip-core
sudo modprobe vhci-hcd
sudo modprobe usbip_host
```
2. USB 장치를 삽입한 뒤 다음 명령어를 실행하여 사용 가능한 USB 장치를 조회합니다.
```
usbip list --local
```
예를 들어, 로컬 컴퓨터에 Feitian 이라는 U-Key 를 삽입하면, 다음과 같은 결과를 출력합니다.
```
busid 1-1.3(096e:031b)
Feitian Technologies, Inc.: unknown product(096e:031b)
```
3. busid 값을 기록하고 다음 명령어를 순서대로 실행하여 리스너 서비스를 실행합니다. USB/IP 포트 번호를 지정하여 USB 장치를 공유합니다.
```
sudo usbipd -D [--tcp-port PORT]
sudo usbip bind -b [busid]
```
예를 들어, 지정한 USB/IP의 포트 번호가 3240 포트이고(즉 USB/IP의 기본 포트), busid 값은 `1-1.3`이라면, 다음의 명령어를 실행합니다.
```
sudo usbipd -D
sudo usbip bind -b 1-1.3
```
4. (선택) 다음 명령어를 실행하여 SSH 터널을 생성하고, 포트 리스너를 사용합니다.
> 로컬 컴퓨터에 공인 IP가 없다면 이 작업을 실행하시고, 로컬 컴퓨터에 공인 IP가 있다면 이 작업을 건너뛰시기 바랍니다.
>
```
ssh -Nf -R USB/IP 지정 포트 번호: localhost: USB/IP 지정 포트 번호 root@your_host
```
`your_host`는 CVM의 IP 주소를 나타냅니다.
예를 들어, USB/IP 포트 번호가 3240 포트이고 CVM의 IP 주소가 192.168.15.24 라면, 다음의 명령어를 실행합니다.
```
ssh -Nf -R 3240:localhost:3240 root@192.168.15.24
```


### USB Client 설정

> 다음의 작업 순서는 로컬 컴퓨터에 공인 IP가 없는 상황을 예로 들어 설명합니다. 로컬 컴퓨터에 공인 IP가 있다면, 작업 순서 중의 `127.0.0.1` 를 본인의 로컬 컴퓨터의 공인 IP 주소로 수정하시기 바랍니다.
>

1. [표준 방식으로 Linux 인스턴스에 로그인(권장)](https://intl.cloud.tencent.com/document/product/213/5436)합니다.
2. 다음 명령어를 순서대로 실행하여, USB/IP 소스를 다운로드합니다.
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -ivh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
```
3. 다음 명령어를 순서대로 실행하여 USB/IP를 설치합니다.
```
yum -y install kmod-usbip usbip-utils
modprobe usbip-core
modprobe vhci-hcd
modprobe usbip-host
```
4. 다음 명령어를 실행하여 CVM에서 사용 가능한 USB 장치를 조회합니다.
```
usbip list --remote 127.0.0.1
```
예를 들어, Feitian 이라는 U-Key 정보를 찾으면, 다음과 같은 결과를 출력합니다.
```
Exportable USB devices
======================
-127.0.0.1 1-1.3: Feitian Technologies, Inc.: unknown product(096e:031b):/sys/devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.3:(Defined at Interface level)(00/00/00)
```
5. 다음 명령어를 실행하여 USB 장치를 서버에 바인딩합니다.
```
usbip attach --remote=127.0.0.1 --busid=1-1.3
```
6. 다음 명령어를 실행하여 현재 USB 장치 리스트를 조회합니다.
```
lsusb
```
다음과 같은 정보가 출력되면, 공유에 성공했음을 의미합니다.
```
Bus 002 Device 002:ID096e:031b Feitian Technologies, Inc.
Bus 002 Device 001:ID1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 001:ID1d6b:0001 Linux Foundation 1.1 root hub
```
