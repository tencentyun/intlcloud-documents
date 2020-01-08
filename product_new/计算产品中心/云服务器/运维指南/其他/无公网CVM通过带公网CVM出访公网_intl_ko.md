## 작업 시나리오
CVM 구매 시 대역폭 최댓값을 0Mbps으로 선택했다면 CVM이 공용 네트워크에 액세스할 수 없습니다. 본 문서는 CentOS7.5를 예시로 사용하여 공용 네트워크 IP가 없는 CVM에서 PPTP VPN을 통해 공용 네트워크 IP가 있는 CVM의 공용 네트워크로 연결하는 방법을 소개합니다.


## 전제 조건
- 동일한 VPC에서 생성된 두 개의 CVM(**공용 네트워크 IP가 없는 CVM**과 **공용 네트워크 IP가 있는 CVM**)이 있어야 합니다.
- 공용 네트워크 IP가 있는 CVM의 내부 네트워크 IP를 얻어야 합니다.

## 작업 순서
### 공용 네트워크 IP가 있는 CVM에서 PPTP 구성

1. 공용 네트워크 IP가 있는 CVM에 로그인하십시오.
2. 아래의 명령어를 실행하여 PPTP를 설치하십시오.
```
yum install -y pptpd
```
2. 아래의 명령어를 실행하여 ‘pptpd.conf’ 구성 파일을 여십시오.
```
vim /etc/pptpd.conf
```
3. “**i**” 또는 “**Insert**”를 눌러 편집 모드로 전환한 뒤 파일 끝부분에 다음을 추가하십시오.
```
localip 192.168.0.1
remoteip 192.168.0.234-238,192.168.0.245
```
4. “**Esc**”를 누르고 “**:wq**”를 입력하여 파일을 저장한 뒤 돌아가십시오.
5. 아래의 명령어를 실행하여 ‘/etc/ppp/chap-secrets’ 구성 파일을 여십시오.
```
vim /etc/ppp/chap-secrets
```
6. <span id="step7"> “**i**” 또는 “**Insert**”를 눌러 편집 모드로 전환한 후 다음의 형식에 따라 파일 끝부분에 연결한 PPTP의 사용자 이름과 비밀번호를 추가하십시오.</span>
```
사용자 이름    pptpd    비밀번호    *
```
예를 들어, 연결한 PPTP의 사용자 이름이 root이고, 로그인 비밀번호가 123456인 경우 추가할 정보는 다음과 같습니다.
```
root    pptpd    123456    *
```
7. “**Esc**”를 누르고 “**:wq**”를 입력하여 파일을 저장한 뒤 돌아가십시오.
8. 아래의 명령어를 실행하여 PPTP 서비스를 시작하십시오.
```
systemctl start pptpd
```
9. 다음의 명령어를 순서대로 실행하여 전달 기능을 시작하십시오.
```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.0/24 -j MASQUERADE
```

### 공용 네트워크 IP가 없는 CVM에서 PPTP 구성

1. 공용 네트워크 IP가 없는 CVM에 로그인하십시오.
2. 아래의 명령어를 실행하여 PPTP 클라이언트를 설치하십시오.
```
yum install -y pptp pptp-setup
``` 
3. 아래의 명령어를 실행하여 구성 파일을 생성하십시오.
```
pptpsetup --create 구성 파일 이름 --server 공용 네트워크 IP가 있는 CVM의 내부 네트워크 IP --username이 PPTP에 연결된 사용자 이름 --password가 PPTP에 연결된 비밀번호 --encrypt
```
예를 들어, test 구성 파일을 생성한 후 공용 네트워크 IP 주소를 얻은 CVM의 내부 네트워크 IP가 10.100.100.1인 경우 아래의 명령어를 실행하십시오.
```
pptpsetup --create test --server 10.100.100.1 --username root --password 123456 --encrypt
```
4. 아래의 명령어를 실행하여 PPTP에 연결하십시오.
```
pppd call test(3단계에서 생성된 구성 파일 이름)
```
5. 다음의 명령어를 순서대로 실행하여 라우팅을 설정하십시오.
```
route add -net 10.0.0.0/8 dev eth0
route add -net 172.16.0.0/12 dev eth0
route add -net 192.168.0.0/16 dev eth0
route add -net 169.254.0.0/16 dev eth0
route add -net 9.0.0.0/8 dev eth0
route add -net 100.64.0.0/10 dev eth0
route add -net 0.0.0.0 dev ppp0
```

### 구성 성공 여부 검사
공용 네트워크 IP가 없는 CVM에서 다음 명령어를 실행하여, 임의의 외부 네트워크 주소를 PING 한 뒤 PING 가능 여부를 검사하십시오.
```
ping -c 4 외부 네트워크 주소
```
아래와 유사한 결과가 리턴될 경우 구성이 성공했음을 나타냅니다.
![](https://main.qcloudimg.com/raw/c841782ce0976982d1f289d3437ec0ed.png)



