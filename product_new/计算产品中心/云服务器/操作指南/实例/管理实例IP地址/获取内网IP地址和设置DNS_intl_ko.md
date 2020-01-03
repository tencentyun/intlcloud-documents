본 문서에서는 인스턴스의 개인 IP 주소 획득과 내부 네트워크 DNS 설정과 관련된 작업에 대해 설명합니다.

## 인스턴스의 개인 IP 주소 획득하기
### 콘솔을 사용하여 획득하기
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
2. 인스턴스의 관리 페이지에서 사용자가 조회해야 할 개인 IP 인스턴스를 선택하고 마우스를 "주 IP 주소" 열에 이동하여 <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"> 클릭하면 개인 IP 주소를 복사할 수 있습니다. 아래 이미지를 참조하십시오.
![](https://main.qcloudimg.com/raw/f4849355a4890861e2d07b35de1099a4.png)

### API를 사용하여 획득하기
[DescribeInstances 인터페이스](https://cloud.tencent.com/document/product/213/15728)를 참조하십시오.

### 인스턴스 메타데이터를 사용하여 획득하기

1. CVM에 로그인하십시오.
2. cURL 툴 또는 HTTP의 GET 요청을 통해 인스턴스 메타데이터에 액세스합니다.
> 다음 작업은 cURL 툴을 예로 들어 설명합니다.
>
다음 명령어를 실행하여 개인 IP를 획득합니다.
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
```
리턴한 정보가 개인 IP 주소입니다. 아래 이미지를 참조하십시오.
![](https://mc.qcloudimg.com/static/img/14a13eccebc7eee6f83bc026adb30902/image.png)

인스턴스 메타데이터에 대한 자세한 정보는 [인스턴스 메타데이터 조회](https://intl.cloud.tencent.com/document/product/213/4934)를 참조하십시오.

## 내부 네트워크 DNS 설정 
네트워크 분석에 오류가 발생할 경우 사용자는 CVM 운영 체제의 유형에 따라 수동으로 내부 네트워크 DNS를 설정할 수 있습니다.

### Linux 시스템

1. Linux CVM에 로그인하십시오.
2. 다음 명령어를 실행하여 `/etc/resolv.conf` 파일을 여십시오.
```
vi /etc/resolv.conf
```
3. **i** 또는 **Insert** 를 눌러 편집 모드로 전환하고 [내부 네트워크 DNS](https://intl.cloud.tencent.com/document/product/213/5225) 리스트에서 대응하는 리전에 따라 DNS IP를 수정합니다.
예를 들어 내부 네트워크 DNS IP를 베이징 리전의 개인 네트워크 DNS 서버로 수정합니다.
```
nameserver 10.53.216.182
nameserver 10.53.216.198
options timeout:1 rotate
```
4. **Esc**를 눌러 **:wq**를 입력하면 파일은 저장하고 출력됩니다.

### Windows 시스템

1. Windows CVM에 로그인하십시오.
2. 운영 체제 인터페이스에서 [제어판]>[네트워크와 공유 센터]>[어댑터 장치 변경]을 여십시오.
3. 마우스 우클릭으로 [이더넷]을 클릭하고 [속성]을 선택하면 "이더넷 속성" 창이 열립니다.
4. "이더넷 속성" 창에서 [Internet 프로토콜 버전 4 (TCP/IPv4)]를 더블 클릭하여 여십시오. 아래 이미지를 참조하십시오.
5. [아래의 DNS 서버 주소 사용]을 선택하고 [내부 네트워크 DNS](https://intl.cloud.tencent.com/document/product/213/5225) 리스트에 대응하는 리전에 따라 DNS IP를 수정합니다.
6. [확인]을 클릭하십시오.
