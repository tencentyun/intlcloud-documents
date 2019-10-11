
## 1. CVM 인스턴스 생성과 구성
파일 시스템에 접근하려면 파일 시스템을 Linux 또는 Windows를 기반으로 한 Tencent Cloud CVM 인스턴스에 탑재해야 합니다. 이 절차에서 Windows에 기반한 Tencent Cloud CVM 인스턴스를 생성 및 구성하게 됩니다. Linux에 기반한 CVM을 사용하고 싶다면 문서 [CFS로 네트워크 파일 시스템 생성(Linux)](/doc/product/582/11523)을 참조하십시오. 이미 CVM 인스턴스를 생성하였다면 단계 2 [파일 시스템 및 탑재 지점 생성](#1)으로 점프하십시오.

Tencent Cloud 홈페이지에 로그인하여 [클라우드 제품]>[컴퓨팅과 네트워크]>[CVM]을 선택하고 [바로 구매]를 클릭해 [CVM 구매 페이지](https://buy.cloud.tencent.com/buy/cvm)에 진입합니다.

### 1. 지역과 모델 선택
![](//mc.qcloudimg.com/static/img/3ed8bab8cce3dde578a6e3fb14267ea5/image.png)
- 연/월정액 또는 사용량 기반 요금제 모드를 선택합니다. 사용량 기반 요금제 CVM을 구입할 수 없는 사용자는 우선 [실명 인증](https://console.cloud.tencent.com/developer/auth)을 완성하십시오. 더 많은 정보는 [요금제 설명](/doc/product/213/2180)을 참조하십시오.
- 지역과 가용 영역을 선택합니다. 여러 대의 CVM이 필요할 경우, 다른 가용 영역을 선택하면 재해 복구를 실현할 수 있습니다.
- 모델과 구성을 선택합니다. 인스턴스 유형에 대한 상세한 설명은 [인스턴스 유형 개요](/doc/product/213/7153)를 참조하십시오.

### 2. 이미지 선택
![](//mc.qcloudimg.com/static/img/56c4ecbdb12dd0a366ecf701153fce1d/image.png)
- 이미지 제공업체를 선택합니다.
Tencent Cloud는 공공 이미지, 사용자 지정 이미지, 공유 이미지, 서비스 시장을 제공합니다. [이미지 유형](/doc/product/213/4941)을 참조하여 선택할 수 있습니다. 이제 막 Tencent Cloud 사용을 시작한 사용자는 공공 이미지를 선택하길 추천합니다. 정품 Windows 운영체제를 포함하며 후속 실행 환경은 스스로 구축하면 됩니다.
- 운영체제 선택: Windows Server를 선택합니다.
- 시스템 버전을 선택합니다.

### 3. 저장과 네트워크 선택
![](//mc.qcloudimg.com/static/img/e95a5bf7bf47c60f43dd0ee62946b67a/image.png)
- 디스크 유형과 데이터 디스크 크기를 선택합니다.
Tencent Cloud는 클러우드 디스크와 로컬 디스크 두 가지 유형(모두 기본적으로 50GB 시스템 디스크이며, 시스템 디스크 크기는 임의 선택)을 제공합니다.
 - 클라우드 디스크: 디스크 1개당 백업 3개의 분산식 저장 방식으로 데이터 신뢰성이 높습니다.
 - 로컬 디스크: CVM 소재 물리적 컴퓨터의 저장 장치로 지연이 낮지만 단일 실패 지점 리스크가 존재합니다. 구체적인 비교는 [제품 분류](/doc/product/362/2353)를 참조하십시오.
- 네트워크 유형을 선택합니다.
Tencent Cloud는 기본 네트워크 또는 VPC 두 가지 옵션을 제공합니다.
 - 기본 네트워크: 초보자에게 적합하며 동일한 사용자의 CVM은 사설망을 통해 상호 연결됩니다.
 - VPC: 고급 사용자에게 적합하며 다른 VPC 사이의 로직은 격리됩니다.
- 공중망 대역폭을 선택합니다
Tencent Cloud는 대역폭 기반 요금제와 트래픽 기반 요금제 두 가지를 제공합니다.
 - 대역폭 기반 요금제: 고정 대역폭을 선택하며 이를 초과할 시 패킷이 손실됩니다. 네트워크 파동이 작은 환경에 적합합니다.
 - 트래픽 기반 요금제: 실제 사용한 트래픽에 따라 비용을 받습니다. 대역폭 피크값을 제한하여 의외 트래픽으로 인한 비용 발생을 피할 수 있으며, 일시적으로 대역폭이 해당 값을 초과하면 패킷이 손실됩니다. 네트워크 파동이 큰 환경에 적합합니다.
- 서버 수량을 선택합니다.
- 구매 시간과 갱신 방식을 선택합니다(연/월정액 요금제 CVM만 해당).

### 4. 정보 구성
![](//mc.qcloudimg.com/static/img/fbc4230b5e6a19ef6ec60ffebfc62aaa/image.png)
- CVM 서버 명명: 생성 후 명명하거나 즉시 명명할 수 있습니다.
- 로그인 정보 설정: 비밀번호를 설정하거나 자동 생성할 수 있습니다. 설정한 비밀번호는 생성 후 수정할 수 있으며, 자동 생성된 비밀번호는 내부 메시지 방식으로 발송됩니다.
- 보안 그룹 선택(**로그인 포트 3389 개방 확보**, 더 많은 정보는 [보안 그룹](/doc/product/213/5221))을 참조하십시오.

[바로 구매] 버튼을 클릭하여 지불을 완료하면 [콘솔](https://console.cloud.tencent.com/cvm)에 진입해 CVM을 수령할 수 있습니다.
CVM을 생성하면 내부 메시지를 받게 되며, 인스턴스 이름, 공인 IP 주소, 사설 IP 주소, 로그인 이름, 초기 로그인 비밀번호 등 정보가 포함되어 있습니다. 이 정보를 사용하여 인스턴스 로그인 및 관리할 수 있습니다.
 

<span id="1"></span>
## 2. 파일 시스템 및 탑재 지점 생성

1. Tencent Cloud [콘솔](https://console.cloud.tencent.com/)에 진입하여 [클라우드 제품]>[스토리지]>[CFS]를 클릭하면 CFS 콘솔에 진입할 수 있습니다.
![](//mc.qcloudimg.com/static/img/4fee6ea61cfba11927f6891527237610/image.png)

2. Tencent Cloud CFS 콘솔에서 [생성]을 클릭하면 파일 시스템 생성 팝업창이 표시됩니다. 파일 시스템 생성 팝업창에 관련 정보를 입력하고 오류가 없음을 확인한 뒤 [확인]을 클릭하면 파일 시스템이 생성됩니다.
![](https://main.qcloudimg.com/raw/3797c04469bf0da994d2e2876a2a39ad.png)
 - 이름: 생성한 파일 시스템을 명명할 수 있습니다.
 - 지역과 가용 영역: 클라이언트와 가까운 지역은 접근 지연 현상을 줄여 다운로드 속도를 향상시킬 수 있습니다.
 - 파일 프로토콜: NFS(Linux, Unix 클라이언트에 더욱 적합함), CIFS/SMB(Windows 클라이언트에 더욱 적합함)
 - 네트워크 유형: Tencent Cloud는 기본 네트워크와 VPC 두 가지를 제공합니다. 기본 네트워크는 초보자에게 적합하며 동일 사용자의 CVM은 사설망을 통해 상호 연결됩니다. VPC는 고급 사용자에게 적합하며 다른 VPC 사이의 로직은 격리됩니다.
  	
 > **주의:**
 > 자신의 CVM 인스턴스 소재 네트워크에 따라 파일 시스템을 생성 및 탑재합니다.
 > - VPC의 CVM에서 파일 시스템을 공유하려면 파일 시스템을 생성할 때 VPC를 선택해야 합니다. 파일 시스템이 VPC에 속할 경우, 특별한 네트워크 설정을 진행하지 않았다면 동일 VPC 내 CVM 인스턴스만 탑재할 수 있습니다.
 > - 기본 네트워크의 CVM에서 파일 시스템을 공유하려면 파일 시스템을 생성할 때 기본 네트워크를 선택해야 합니다. 파일 시스템이 기본 네트워크에 속할 경우, 특별한 네트워크 설정을 진행하지 않았다면 동일 기본 네트워크 내 CVM 인스턴스만 탑재할 수 있습니다.
 > - 여러 네트워크에서 파일 시스템을 공유하려면 [가영 영역 간/네트워크 간 접근 가이드](/doc/product/582/9764)를 참조하십시오.

3. 탑재 지점 정보를 획득합니다. 파일 시스템 및 탑재 지점 생성 완료 후, 인스턴스 ID를 클릭하고 파일 시스템 세부 정보에 진입하여 [탑재 지점 정보]를 클릭하면 Windows의 탑재 명령을 획득합니다.

NFS 파일 시스템 탑재 지점 정보는 다음과 같습니다.
![](https://mc.qcloudimg.com/static/img/f50435216defb4083874bc78d568001e/image.png)

CIFS/SMB 파일 시스템 탑재 지점 정보는 다음과 같습니다. 
![](https://main.qcloudimg.com/raw/939aafe4bca9907bc391d41e8798c4a6.png)



## 3. 인스턴스 연결
일반적인 Windows CVM 로그인 방법을 소개합니다. 상황에 따라 다른 로그인 방식을 사용할 수 있으며 여기에서는 콘솔을 통한 로그인을 소개합니다. 더 많은 로그인 방식은 [Windows 인스턴스 로그인](/doc/product/213/5435)을 참조하십시오.

**전제 조건**
CVM에 로그인하려면 관리자 계정과 비밀번호를 사용해야 합니다.
- 관리자 계정: Windows 유형의 인스턴스에 대해 관리자 계정은 Administrator로 통일됩니다.
- 비밀번호: 비밀번호는 CVM 구매 시 설정한 비밀번호입니다.
   
**콘솔을 통한 CVM 로그인**
1. CVM 목록의 작업열에서 [로그인] 버튼을 클릭하면 VNC를 통해 Windows CVM에 연결할 수 있습니다.
![](//mc.qcloudimg.com/static/img/d017c67c9f447c1441cf74ed4ac2b279/image.png)
2. 왼쪽 상단 [Ctrl-Alt-Delete]을 클릭해 명령을 발송하여 시스템 로그인 페이지에 진입합니다.
![](//mc.qcloudimg.com/static/img/e4dbc02ca9ae2a7cb9ada5316effd31a/image.png)
3. 계정(Administrator)과 비밀번호를 입력하면 로그인할 수 있습니다.

> **주의:**
>해당 터미널은 독점적이며 동일한 시간에 한 명의 사용자만 콘솔을 사용하여 로그인할 수 있습니다.


**네트워크 통신 확인**
탑재 전, 클라이언트와 파일 시스템의 네트워크 연결을 확인해야 합니다. telnet 명령을 통해 확인할 수 있습니다. 각 프로토콜 및 클라이언트의 개방 포트 정보는 다음과 같습니다.

파일 시스템 프로토콜 | 클라이언트 개방 포트 | 네트워크 연결 확인
------- | ------- | ---------
NFS 3.0 | 111, 892, 2049 |  telnet 111 또는 892 또는 2049
NFS 4.0 | 2049 |  telnet 2049
CIFS/SMB | 445 |  telnet 445 

참고: CFS는 ping을 지원하지 않습니다.

## 4. 파일 시스템 탑재
### CIFS/SMB 파일 시스템 탑재
#### 그래픽 인터페이스를 통해 파일 시스템 탑재
a. "매핑 네트워크 드라이브" 열기
파일 시스템을 탑재해야 할 Windows에 로그인하고 "시작" 메뉴에서 "컴퓨터"를 찾아 마우스 오른쪽 버튼을 클릭하면 메뉴가 나타나면 메뉴의 "매핑 네트워크 드라이브"를 클릭합니다. 
![](https://main.qcloudimg.com/raw/515b5b21a19e3f3518c75441326e1800.png)
![](https://main.qcloudimg.com/raw/b0396ce0f8f108f3e89a2f2bfb3d7f71.png)

b. 접근 경로 입력
팝업된 설정창에 "드라이브" 문자 및 폴더(CIFS/SMB 파일 시스템에서 보이는 탑재 디렉터리)를 설정합니다.
![](https://main.qcloudimg.com/raw/8d58ee713b9e072156caf8019b4242d5.png)
![](https://main.qcloudimg.com/raw/939aafe4bca9907bc391d41e8798c4a6.png)



c. 읽기/쓰기 인증
확인 후, 페이지가 이미 탑재한 파일 시스템으로 바로 리디렉션됩니다. 마우스 오른쪽 버튼을 클릭하여 파일 하나를 생성하여 읽기/쓰기의 정확성을 인증할 수 있습니다.
![](https://mc.qcloudimg.com/static/img/60b9388885536ec7d81b1cf7f76c39d5/image.png)

#### 명령행을 통해 파일 시스템 탑재
FSID를 사용하여 파일 시스템 탑재를 진행하십시오. 탑재 명령은 다음과 같습니다.
```
net use <공유 디렉터리 이름>: \\10.10.11.12\FSID 
```
예시:
```
net use X: \\10.10.11.12\fjie120
```

> **주의:**
> FSID는 [콘솔]>[파일 시스템 세부 정보]>[탑재 지점 정보]에서 획득할 수 있습니다.
![](https://main.qcloudimg.com/raw/939aafe4bca9907bc391d41e8798c4a6.png)


### NFS 파일 시스템 탑재
#### 1. NFS 서비스 활성화
탑재 전, 시스템이 NFS 서비스를 이미 활성화하였는지 확인하십시오. 여기는 Windows Server 2012 R2를 예시로 NFS 서비스를 활성화합니다.
1.1 [제어판]>[프로그램]>[Windows 기능 활성화 또는 비활성화]>[서버 역할]에서 [NFS 서버]를 선택합니다.
![](https://mc.qcloudimg.com/static/img/eaeed922e9d1f673e47137d80a88fa70/image.png)
1.2 [제어판]>[프로그램]>[Windows 기능 활성화 또는 비활성화]>[특성] 페이지에서 [NFS 클라이언트]를 선택합니다. [NFS 클라이언트]를 선택하면 Windows NFS 클라이언트 서비스를 활성화할 수 있습니다.
![](https://mc.qcloudimg.com/static/img/4f9d7ac7b877ceffc5bc2b1d7c050a24/image.png)

#### 2. NFS 서비스 활성화 여부 인증
Windows의 명령행 도구를 열고, 제어판에서 다음 명령을 실행합니다. NFS 관련 정보를 반환하면 NFS 클라이언트 정상 운행 중임을 의미합니다.
```
mount -h
```
![](https://mc.qcloudimg.com/static/img/4e4f9db217874ccec91ac1f888c8e451/image.png)

#### 3. 익명 접근 사용자와 사용자 그룹 추가
3.1 레지스트리 열기
명령행창에 regedit 명령을 입력하고 Enter를 누르면 레지스트리창을 열 수 있습니다.
![](https://mc.qcloudimg.com/static/img/c9fca9a1b123a5b2dbc69b0ce66d539f/image.png)

3.2 구성 항목 AnonymousUid와 AnonymousGid 추가
연 레지스트리에서 다음 경로를 찾아 선택합니다. 
```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ClientForNFS\CurrentVersion\Default
```
오른쪽 빈 공간에서 마우스 오른쪽 버튼을 클릭하면 [new]가 팝업됩니다. 메뉴에서 운영체제에 따라 [DWORD(32-bit) Value] 또는 [QWORD(64-bit) Value]를 선택합니다. 이때, 목록에 새로운 기록이 나타나고 이름 칸을 AnonymousUid로 수정하면 되며, 데이터값은 기본값인 0으로 설정하면 됩니다. 동일한 방법을 사용하여 이름이 AnonymousGid인 기록을 계속 추가하고 데이터를 역시 기본값인 0으로 설정합니다.
![](https://mc.qcloudimg.com/static/img/381cdc3b68fb35be5dcceb2a4c962e33/image.png)
![](https://mc.qcloudimg.com/static/img/80bb0cfbffbed939522459a830df3eac/image.png)

3.3 다시 시작하여 구성 적용
레지스트리를 종료하고 Windows 시스템을 다시 시작하면 레지스트리 수정이 완료됩니다.

#### 4. 파일 시스템 탑재
파일 시스템 탑재는 그래픽 인터페이스를 통한 탑재와 CMD 명령행을 통한 탑재 두 가지가 있습니다.
1)그래픽 인터페이스를 통한 탑재
a. "매핑 네트워크 드라이브" 열기
파일 시스템을 탑재해야 할 Windows에 로그인하고 "시작" 메뉴에서 "컴퓨터"를 찾아 마우스 오른쪽 버튼을 클릭하면 메뉴가 나타나면 메뉴의 "매핑 네트워크 드라이브"를 클릭합니다. 
![](https://main.qcloudimg.com/raw/515b5b21a19e3f3518c75441326e1800.png)
![](https://main.qcloudimg.com/raw/b0396ce0f8f108f3e89a2f2bfb3d7f71.png)
b. 접근 경로 입력
팝업된 설정창에 "드라이브" 문자 및 폴더(NFS 파일 시스템에서 보이는 탑재 디렉터리)를 설정합니다.
![](https://main.qcloudimg.com/raw/8d58ee713b9e072156caf8019b4242d5.png)
![](https://mc.qcloudimg.com/static/img/caa18888e6da73b19de8eefc18ff3680/image.png)
c. 읽기/쓰기 인증
확인 후, 페이지가 이미 탑재한 파일 시스템으로 바로 리디렉션됩니다. 마우스 오른쪽 버튼을 클릭하여 파일 하나를 생성하여 읽기/쓰기의 정확성을 인증할 수 있습니다.
![](https://mc.qcloudimg.com/static/img/60b9388885536ec7d81b1cf7f76c39d5/image.png)

2)CMD 명령행을 통해 탑재
Windows의 명령행 도구에 다음 명령을 입력하여 파일 시스템을 탑재합니다. 시스템 디폴트 서브 디렉터리는 FSID입니다.

```
mount  <탑재 지점 IP>:/<FSID> <공유 디렉터리 이름>:
```

예시:
```
mount 10.10.0.12:/z3r6k95r X:
```

> **주의:**
> FSID 탑재 명령은 [CFS 콘솔]>[파일 시스템 세부 정보]>[탑재 지점 정보]에서 획득할 수 있습니다.

### 5.파일 시스템 탑재 해제
#### 그래픽 인터페이스를 통해 공유 디렉터리 탑재 해제
이미 탑재한 파일 시스템을 연결 해제하려면 마우스 오른쪽 버튼으로 디스크를 클릭해 메뉴에서 [연결 해제] 옵션을 클릭하면 파일 시스템 연결을 끊을 수 있습니다.
![](https://mc.qcloudimg.com/static/img/376cd0547aa64f4d519e5444c5a58f93/image.png)

#### CMD 명령을 통해 NFS 공유 디렉터리 탑재 해제 

상황에 따라 공유 디렉터리를 탑재 해제하려면 다음 명령을 사용하십시오. 그 중 "디렉터리 이름"은 루트 디렉터리 또는 파일 시스템의 완전 경로가 됩니다.
```
umount <디렉터리 이름>：
```
예시:
```
umount X：
```


## 5. 리소스 중지
Tencent Cloud 콘솔로 손쉽게 CVM 인스턴스와 파일 시스템을 중지할 수 있습니다. 비용이 계속 발생되지 않도록 사용하지 않는 리소스는 중지하는 것이 가장 좋습니다.
1. Tencent Cloud 인스턴스를 중지합니다. Tencent Cloud CVM [콘솔](https://console.cloud.tencent.com/cvm/index)에 진입해 중지해야 할 인스턴스를 선택하고 [더 보기]>[CVM 상태]를 클릭하여 [폐기]를 선택해 CVM 인스턴스를 중지할 수 있습니다.
![](//mc.qcloudimg.com/static/img/76c588284e3b525702d748b5cd7b8b00/image.png)
2. 파일 시스템을 중지합니다. Tencent Cloud CFS [콘솔](https://console.cloud.tencent.com/cfs)에 진입해 중지할 파일 시스템을 선택하고 [삭제] 클릭 후 [확인]하면 파일 시스템을 삭제할 수 있습니다.
![](//mc.qcloudimg.com/static/img/28cade4807a283ffdcb1fc2a39a7ad88/image.png)

