## 사용 시나리오
사용자가 EIP를 통해 외부 네트워크를 액세스할 경우 NAT 모드 또는 EIP 패스스루 모드를 선택할 수 있으며 현재 NAT 모드를 기본으로 합니다.
- NAT 모드에서 EIP는 로컬에서 볼 수 없습니다.
- EIP 패스스루 후, EIP는 로컬에 표시되며 구성 중에 EIP 주소를 매번 수동으로 추가할 필요가 없으므로 개발 비용을 절감할 수 있습니다.
-NAT 모드는 대부분의 요구 사항을 충족할 수 있지만 CVM 내에서 공인 IP 를 확인해야 하는 시나리오의 경우 패스스루 모드를 사용해야 합니다.

## 사용 제한
-현재 EIP 패스스루는 화이트리스트 제어를 통해 VPC 내의 디바이스만 지원하며, 필요한 경우 [티켓 신청] (https://console.cloud.tencent.com/workorder/category) 을 제출하십시오.
>-NAT Gateway는 패스스루 모드를 활성화한 EIP를 바인딩할 수 있지만 패스스루 효과는 없습니다.
-CVM용 EIP 패스스루는 NAT 게이트웨이와 함께 사용할 수 없습니다. CVM이 있는 서브넷의 라우팅 테이블에 NAT 게이트웨이를 통해 공용 네트워크에 액세스하는 라우팅 정책이 구성되어 있으면 CVM의 EIP 가 패스스루 기능을 구현하지 못합니다. [NAT 게이트웨이 및 EIP 의 우선 순위 조정] (https://intl.cloud.tencent.com/document/product/1015/327634) 을 통해 클라우드 서버가 NAT 게이트웨이 대신 자신의 EIP 를 통해 공용 네트워크에 먼저 액세스하도록 할 수 있으며, 이때 EIP 패스스루 기능이 구현됩니다.

## 작업 순서
EIP 패스스루는 콘솔뿐 아니라 운영 체제 내에서 네트워크 ENI 를 추가하고 비즈니스 요구 사항에 따라 운영 체제 내 라우팅을 구성해야 하기 때문에 내부 네트워크 트래픽이 개인 IP 를 통과하고 외부 네트워크 트래픽이 공인 IP 를 이동하도록 IP 를 구성하는 스크립트를 제공합니다.
> 다른 비즈니스 시나리오가 있는 경우 특정 비즈니스 시나리오에 따라 라우팅을 설정합니다.
>
### Linux CVM에 EIP 패스스루 구성
>
>Linux 스크립트는 시스템 버전 CentOS 6.x, CentOS 7 및 Ubuntu를 지원합니다.
>-Linux 스크립트는 주 ENI (eth0) 만 지원하며 보조 ENI는 일시적으로 지원되지 않습니다.
>-주 ENI 에 바인딩된 공인 IP 가 EIP 가 아니고 먼저 EIP 로 변환해야 하는 경우 [공인 IP EIP] (https://intl.cloud.tencent.com/document/product/213/16586 # converging-public-IP-to-EIP) 를 참조하십시오.

## 작업 시나리오
Linux 스크립트는 개인 IP 와 공인 IP 가 모두 주 ENI (eth0) 에 있고 공용 네트워크 주소는 공인 IP 를 통해 액세스하며 인트라넷 주소는 개인 IP 를 통해 액세스하는 시나리오를 대상으로 합니다.

### 1 단계: EIP 패스스루 스크립트 다운로드
EIP 패스스루 프로세스로 인해 네트워크가 중단되므로 먼저 EIP 패스스루 스크립트를 CVM에 확보해야 합니다. 다음 방법 중 하나를 선택합니다.
- **방법 1: EIP 패스스루 스크립트 업로드**
 1. EIP 패스스루 설정 스크립트를 다운로드합니다. 다운로드 경로: [Linux 스크립트 다운로드] (https://EIP-direct-124277469.cos.ap-guangzhou.myqcloud.com/EIP _ direct.sh).
 2. 스크립트를 로컬에 다운로드한 후 EIP 패스스루가 필요한 클라우드 서버에 업로드합니다.
- **방법 2: 직접 명령어 사용**
CVM에 로그인하여 CVM에서 직접 다음 명령 다운로드를 수행합니다.
```
wget https://eip-direct-1254277469.cos.ap-guangzhou.myqcloud.com/eip_direct.sh
```

### 2단계: EIP 패스스루 스크립트 실행
1. EIP 패스스루가 필요한 CVM 클라우드 서버에 로그인하십시오.
2. EIP 패스스루 스크립트를 실행하십시오. 자세한 방법:
 1. 다음 명령을 실행하여 실행 권한을 추가합니다.
```
chmod +x eip_direct.sh
```
 2. 다음 명령을 실행하여 스크립트를 실행합니다.
```
./eip_direct.sh install XX.XX.XX.XX
```
여기서 XX.XX.XX.XX 는 EIP 주소이며 선택적 입력 가능하며 입력하지 않을 경우 `. /eip_direct.sh install' 을 직접 실행하면 됩니다.

### 3단계: EIP 패스스루 시작
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인하십시오.
2. 해당 EIP 행을 찾아 오른쪽 작업 표시줄에서 [자세히 보기] > [패스스루]를 클릭합니다.


### CVM 서버에 EIP 패스스루 구성
>
>-Windows 시스템의 EIP 패스스루, 개인 IP 와 공인 IP 각각 1 개의 ENI가 필요합니다. 주 ENI 는 공인 IP , 보조 ENI는 공인 IP 만 있으면 됩니다.
>-Windows 가 패스스루를 설정하는 동안 외부 네트워크 중단되며 [VNC 로그인 방식] (https://intl.cloud.tencent.com/document/product/213/324896) 이 권장됩니다.
-주 ENI가 바인딩된 공인 IP 가 EIP 가 아닌 경우 먼저 EIP 로 변환해야 하며 [공인 IP-EIP] (https://intl.cloud.tencent.com/document/product/213/16586 # converting-public-IP-to-EIP) 를 참조하십시오.

## 작업 시나리오
Windows 스크립트 타깃 시나리오:주 ENI 는 외부 네트워크 트래픽을, 보조 ENI 는 내부 네트워크 트래픽을 사용합니다.

#### 1 단계: EIP 패스스루 스크립트 다운로드 < span id="step1"/>
EIP 패스스루 프로세스로 인해 네트워크가 중단되므로 먼저 EIP 패스스루 스크립트를 CVM에 다운로드해야 합니다.
다음 링크를 CVM의 브라우저에서 열어 EIP 패스스루 스크립트를 다운로드하십시오.
```
https://windows-1254277469.cos.ap-guangzhou.myqcloud.com/eip_windows_direct.bat   
```

#### 2 단계: 보조 ENI 설정
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/overview)에 로그인하십시오.
2. CVM 목록에서 구성된 CVM ID 를 클릭하면 상세 페이지로 이동합니다.
3. [ENI] 탭을 선택하고 [ENI 바인딩] 을 클릭하여 주 ENI와 동일한 서브넷의 새로운 네트워크 카드를 생성합니다.
![](https://main.qcloudimg.com/raw/2da530f15e824ff99858f08397687cf6.png)
4. 팝업창에서 [생성된 ENI 및 바인딩] 을 선택하고 관련 정보를 입력한 후 자동으로 IP 를 할당하고 [확인] 을 클릭합니다.
![](https://main.qcloudimg.com/raw/cb6fe49d3bbefd792355ade6e62f29f3.png)

#### 3 단계: 주 ENI 패스스루 구성
1. [EIP 콘솔](https://console.cloud.tencent.com/cvm/eip?rid=1)에 로그인하십시오.
2. 주 ENI 바인딩에 해당하는 EIP 가 있는 행을 찾아 오른쪽 작업 플랫폼 에서 [자세히 보기] > [패스스루]를 클릭합니다.

#### 4 단계: CVM 내 IP 설정
1. CVM에 로그인하면 운영 중 외부 네트워크 액세스가 중단되므로 [VNC 로그인 방법] (https://intl.cloud.tencent.com/document/product/213/324896) 을 사용해야 합니다.
2. 운영 체제 인터페이스에서 왼쪽 아래의 < imgsrc = "https://main.qcloudimg.com/raw/87d894b7e837d9f47828cf2e2922.png" style = "margin:-3px0px; Width:25px "> < imgsrc =" https://main.qcloudimg.com/raw/f0c84862ef303056c201ce7c85a26eec.png "style =" margin:-3px; "를 클릭합니다 >, “Windows PowerShell” 창을 열고 `firewall.cpl ` 를 입력하여 “Windows 방화벽” 페이지를 엽니다.
3. [Windows 방화벽 활성화 및 종료]를 클릭해 “사용자 정의 설정” 인터페이스에 진입하십시오.
![](https://main.qcloudimg.com/raw/e6d6a44be911ec5f60a6205b6f47a2c7.png)
4. “개인 네트워크 설정” 및 “공용 네트워크 설정” 모듈에서 각각 [Windows 방화벽 닫기]를 선택하고 확인을 클릭합니다.
![](https://main.qcloudimg.com/raw/cdb7703dec781e98101f7f3fd7ecf71f.png)
5. [1 단계] (#step1) 에서 다운로드한 스크립트를 두 번 클릭하여 실행하고 공인 IP 주소를 입력한 후 연속해서 두 번 리턴하면 됩니다. 
6. “Windows PowerShell” 창에서 `ipconfig` 를 입력하여 주 ENI의 IPv4 주소가 공용 네트워크 주소로 되는 것을 확인합니다.

> 패스스루가 성공하면 주 ENI에 개인 IP 를 다시 할당하지 마십시오. 구성된 경우 CVM은 공용 네트워크에 액세스할 수 없습니다.

