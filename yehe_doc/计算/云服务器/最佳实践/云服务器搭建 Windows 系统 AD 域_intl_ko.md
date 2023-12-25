## 작업 시나리오
AD(Active Directory)는 Microsoft 서비스의 핵심 컴포넌트입니다. AD는 사용자의 일괄 관리, 애플리케이션 배포 및 패치 업데이트와 같은 효율적인 관리를 실현할 수 있습니다. 많은 Microsoft 컴포넌트(예시: Exchange) 및 장애 조치 클러스터에도 AD 도메인 환경이 필요합니다. 본 문서에서는 Windows Server 2012 R2 데이터센터 버전 64비트 운영 체제를 예로 들어 AD 도메인을 구축하는 방법을 소개합니다.

## 전제 조건

- 2개의 Windows Cloud Server(CVM) 인스턴스가 도메인 컨트롤러(DC) 및 클라이언트(Client)로 생성되었습니다.
- 생성된 인스턴스는 다음 조건을 충족해야 합니다.
	- NTFS 파티션.
	- DNS 서비스 지원.
	- TCP/IP 프로토콜 지원.

## 인스턴스 네트워크 환경
- 네트워크 정보: 네트워크 유형은 VPC이며 스위치의 VPC IP 대역은 10.0.0.0/16입니다.
- 도메인 정보: 예시 도메인은 'example.com'입니다. DC로서의 CVM 인스턴스 IP 주소는 10.0.5.102이고 클라이언트로서의 CVM 인스턴스 IP 주소는 10.0.5.97입니다.
<dx-alert infotype="notice" title="">
AD 도메인 구축 후 CVM 인스턴스가 항상 동일한 IP 주소를 사용하는지 확인하십시오. 그렇지 않으면 IP 주소 변경으로 인해 액세스 예외가 발생합니다.
</dx-alert>



## 개념
AD(Active Directory)는 Microsoft 서비스의 핵심 구성 요소이며 관련 용어 및 개념은 다음과 같습니다.
- **DC**: Domain Controllers, 도메인 컨트롤러.
- **DN**: Distinguished Name, 고유 이름.
- **OU**: Organizational Unit, 조직 단위.
- **CN**: Canonical Name, 정식 이름.
- **SID**: Security Identifier, 보안 식별자.


## 작업 단계

<dx-alert infotype="explain" title="">
기존 도메인 컨트롤러를 사용하여 사용자 정의 이미지를 만들어 새 도메인 컨트롤러를 배포하는 것은 권장되지 않습니다. 반드시 사용해야 하는 경우 사용자 정의 이미지를 생성하기 전에 새 인스턴스의 호스트 이름(hostname)과 인스턴스의 호스트 이름이 같아야 합니다. 그렇지 않으면 "서버의 보안 데이터베이스에 이 워크스테이션 신뢰 관계가 없습니다" 라는 오류가 보고될 수 있습니다. 이 문제를 해결하기 위해 인스턴스 생성 후 동일한 호스트 이름으로 수정할 수도 있습니다.
</dx-alert>



### AD 도메인 컨트롤러 배포[](id:Step1)
1. DC의 인스턴스로 로그인합니다. 자세한 내용은 [표준 방식으로 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/41018)을 참고하십시오.
2. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-3px 0px">을(를) 클릭하고 서버 관리자를 엽니다.
3. **역할 및 기능 추가**를 클릭하면 ‘역할 및 기능 추가 마법사’ 창이 팝업됩니다.
4. 아래 이미지와 같이 '설치 유형 선택' 인터페이스에서 **역할 기반 또는 기능 기반 설치**를 선택하고, 다음 단계를 2회 연속 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/413f2376200fe7a64d56035206ac2c21.png)
5. ‘인터페이스 역할 선택’ 인터페이스에서 아래와 같이  ‘Active Directory 도메인 서비스’와 ‘DNS 서버’를 선택하고 팝업 창에서 **기능 추가** 및 **계속**을 클릭합니다.
이 단계에서는 동일한 인스턴스에 AD 도메인 서비스와 DNS 서비스를 배포하는 것을 예시로 사용합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a9f62f646661dc1c3559b12328ed8077.png)
6. 기본 설정을 유지하고 **다음 단계**를 4회 연속 클릭합니다.
7. 정보 확인 페이지에서 **설치**를 클릭합니다.
설치가 완료되면 ‘역할 및 기능 추가’ 대화 상자를 비활성화합니다.
8. 운영 체제 인터페이스에서 <img src='https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png' style="margin:-3px 0px">을(를) 클릭하고 서버 관리자를 엽니다.
9. 서버 관리자 창에서 <img src="https://main.qcloudimg.com/raw/b7b26ebdfecb3b158adac1a37d7a23f3.png" style="margin:-3px 0px">을(를) 클릭하여 **이 서버를 도메인 컨트롤러로 향상**을 선택합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bc6e02bf64866c4458ec6599babe09a2.png)
10. 열린 ‘Active Directory 도메인 서비스 설정 마법사’ 창에서 ‘배포 작업 선택’을 **신규 포리스트 추가**로 설정하고 루트 도메인 이름을 입력합니다. 본 문서에서는 'example.com'을 예로 듭니다. 아래 이미지와 같이 **다음 단계**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b91884139c592c76cf3547fa7c5de711.png)
11. DSRM(디렉터리 서비스 복원 모드) 암호를 설정하고 **다음 단계**를 클릭합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/192ba48444d9fef4faf46a2c5eb73983.png)
12. 기본 설정을 유지하고 **다음 단계**를 연속 4번 클릭합니다.
13. ‘전제 조건 확인’에서 **설치**를 클릭하여 AD 도메인 서버 설치를 시작합니다.
설치가 완료되면 인스턴스가 자동으로 재시작되며, 인스턴스에 재접속하면 **제어판** > **시스템 및 보안** > **시스템**에서 설치 결과를 확인할 수 있습니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/32475970bbb3c6ff99a6ced08c3e72e1.png)

### 클라이언트 SID 수정
클라이언트 인스턴스의 SID를 수정하려면 [SID 수정 작업 설명](https://intl.cloud.tencent.com/document/product/213/4829)을 참고하십시오.


### 클라이언트를 AD 도메인에 추가
1. 클라이언트의 인스턴스로 로그인합니다. 자세한 내용은 [표준 방식으로 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/41018)을 참고하십시오.
2. DNS 서버 주소를 수정합니다.
  1. **제어판** > **네트워크 및 Internet** > **네트워크 및 공유 센터**를 열고 ‘네트워크 및 공유 센터’ 창에서 **이더넷**을 클릭합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ecbcc37005bc2924ab9cb76055fd0666.png)
  2. ‘이더넷 상태’ 창에서 **속성**을 클릭합니다.
  3. ‘이더넷 속성’ 창에서 ‘Internet 프로토콜 버전4(TCP/IPv4)’를 선택하고 **속성**을 클릭합니다.
  4. ‘Internet 프로토콜 버전4(TCP/IPv4) 속성’ 창에서 ‘다음 DNS 서버 주소 사용’을 선택하고, DNS 서버 주소를 DC 인스턴스의 IP 주소로 설정합니다. 이 문서에서는 `10.0. 5.102`를 예시로 합니다. 아래 이미지와 같습니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/2201da4809892efa26558b3a99e6d324.png)
    [AD 도메인 컨트롤러 배포](#Step1)에서 AD 도메인 서비스와 DNS 서비스는 동일한 CVM 인스턴스(IP 주소: 10.0.5.102)에 배포되었으므로 여기에서 지정하는 DNS 서버의 주소는 10.0.5.102 입니다.
 5. **확인**을 클릭하여 수정 사항을 저장합니다.
3. cmd 창에서 다음 명령어를 실행하여 DNS 서버 IP 주소를 ping할 수 있는지 확인합니다.
```
ping example.com
```
반환된 결과는 아래 이미지와 같이 DNS 서버 IP 주소를 ping할 수 있음을 나타냅니다.
![](https://qcloudimg.tencent-cloud.cn/raw/cfd1ab27a7aaaeb42f9a78c67e476a53.png)
4. **제어판** > **시스템 및 보안** > **시스템**을 열고 ‘시스템’ 창에서 **설정 변경**을 클릭합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6fb71866831646df81ed08c47e10843a.png)
5. ‘시스템 속성’ 팝업 창에서 **변경**을 클릭합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/dbfe2df50797ee5fc07cb2ede72dc7ba.png)
6. ‘컴퓨터 이름/도메인 변경’ 팝업 창에서 필요에 따라 컴퓨터 이름을 수정하고 ‘도메인’이 `example.com`에 속하도록 설정합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/52b3f11a0347a93eb52d47069d3def1a.png)
7. **확인**을 클릭합니다.
8. ‘Windows 보안’ 팝업 창에서 DC 인스턴스의 사용자 이름과 로그인 비밀번호를 입력하고 **확인**을 클릭합니다.
아래 이미지와 같은 확인 창이 팝업되면 도메인이 성공적으로 추가된 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/80856c8d02b87e6b00ef44df88941e89.png)
9. **확인**을 클릭합니다. 인스턴스를 재시작하면 설정이 적용됩니다.
<dx-alert infotype="explain" title="">
클라이언트인 CVM 인스턴스의 경우 도메인에 가입된 클라이언트 인스턴스를 사용하여 사용자 정의 이미지를 생성하는 것은 권장되지 않습니다. 새 이미지에 의해 생성된 인스턴스가 ‘서버의 보안 데이터베이스에 이 워크스테이션 신뢰 관계가 없습니다’ 오류가 보고될 수 있습니다. 정말 필요한 경우 새 사용자 정의 이미지를 생성하기 전에 도메인에서 로그아웃하는 것이 좋습니다.
</dx-alert>

