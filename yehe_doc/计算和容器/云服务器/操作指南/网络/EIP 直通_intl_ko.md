## 사용 시나리오
사용자는 EIP를 통해 외부 네트워크에 액세스할 때, NAT 모드와 EIP 다이렉트 커넥트(Direct Connect) 모드 중에 선택할 수 있습니다. 현재는 NAT 모드로 적용되어 있습니다.
- NAT 모드에서는 로컬에 EIP가 표시되지 않습니다.
- EIP 다이렉트 커넥트 후에는 로컬에 EIP가 표시되며, 설정할 때마다 매번 EIP 주소를 수동으로 추가할 필요가 없어 개발 비용을 절감할 수 있습니다.
- NAT 모드에서도 대부분의 수요를 만족할 수는 있으나, CVM 내에서 공인 IP를 조회해야 하는 시나리오에서는 다이렉트 커넥트 모드를 사용해야 합니다.

## 사용 제한
- 현재 EIP 다이렉트 커넥트는 화이트리스트로 관리할 수 있으며, VPC 내의 디바이스만 지원됩니다. 사용을 원하신다면 [티켓을 신청](https://console.cloud.tencent.com/workorder/category)하시기 바랍니다.
- NAT Gateway에는 다이렉트 커넥트 모드를 활성화한 EIP를 바인딩할 수 있지만, 다이렉트 커넥트 효과는 적용되지 않습니다.
- CVM의 EIP 다이렉트 커넥트를 NAT Gateway와 동시에 사용할 수 없습니다. CVM이 위치한 서브넷 라우팅 테이블에 NAT Gateway를 통해 공용 네트워크에 액세스하는 라우팅 정책을 설정했다면 CVM 상의 EIP는 다이렉트 커넥트 기능을 발휘할 수 없게 됩니다. [NAT Gateway 및 EIP 우선순위 변경](https://intl.cloud.tencent.com/document/product/1015/32734)을 통해 CVM이 NAT Gateway가 아닌 자체 EIP를 통해 공용 네트워크에 액세스하도록 하여 EIP 다이렉트 커넥트 기능을 구현할 수 있습니다.

## 작업 순서
EIP 다이렉트 커넥트는 콘솔에서 실행해야 하며, 운영 체제에서도 IP를 ENI에 추가한 뒤 비즈니스 수요에 따라 운영 체제 내의 라우터를 설정해야 합니다. 이를 위해 내부 네트워크 트래픽은 개인 IP를, 외부 네트워크 트래픽은 공인 IP를 통하도록 IP 설정 스크립트를 제공하고 있습니다.
>다른 비즈니스 시나리오가 있다면, 구체적인 시나리오에 따라 라우터를 설정하시기 바랍니다.
>
### Linux CVM에 EIP 다이렉트 커넥트 설정
>
>- Linux 스크립트에서 지원하는 시스템 버전은 CentOS 6 이상 및 Ubuntu입니다.
>- Linux 스크립트는 주 ENI(eth0)만 지원하며, 보조 ENI는 아직 지원하지 않습니다.
>- 주 ENI에 바인딩된 공인 IP가 EIP가 아니라면, 먼저 EIP로 변경해야 합니다. 자세한 내용은 [공인 IP를 EIP로 변경](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip)을 참조 바랍니다.

#### 작업 시나리오
Linux 스크립트는 개인 IP와 공인 IP 모두가 주 ENI(eth0)에 있고, 공용 네트워크 주소는 공인 IP를 통해, 내부 네트워크 주소는 개인 IP를 통해 액세스하는 시나리오를 대상으로 합니다.

#### 1단계: EIP 다이렉트 커넥트 스크립트 다운로드
EIP 다이렉트 커넥트 과정에서 네트워크 연결이 끊길 수 있으므로, 먼저 EIP 다이렉트 커넥트 스크립트를 CVM으로 가져오시기 바랍니다. 아래의 방법 중 하나를 택해 진행할 수 있습니다.
- **방법1: EIP 다이렉트 커넥트 스크립트 업로드**
 1. EIP 다이렉트 커넥트 설정 스크립트를 다운로드합니다. 
 2. Linux 스크립트를 로컬에 다운로드한 후에 EIP 다이렉트 커넥트를 진행할 CVM에 업로드합니다.
- **방법2: 직접적으로 명령어 사용**
CVM에 로그인한 뒤 CVM에서 아래의 명령어를 직접 실행해 다운로드합니다.
```
wget https://network-data-1255486055.cos.ap-guangzhou.myqcloud.com/eip_direct.sh
```

#### 2단계: EIP 다이렉트 커넥트 스크립트 실행
1. EIP 다이렉트 커넥트가 필요한 CVM에 로그인합니다.
2. EIP 다이렉트 커넥트 스크립트를 실행합니다. 자세한 방법은 아래와 같습니다.
 1. 다음 명령어를 실행하여 권한을 추가합니다.
```
chmod +x eip_direct.sh
```
 2. 다음 명령어를 실행하여 스크립트를 실행합니다.
```
./eip_direct.sh install XX.XX.XX.XX
```
그중에서 XX.XX.XX.XX는 EIP 주소로 선택 입력 사항입니다. 작성하지 않는다면 `./eip_direct.sh install`를 바로 실행하시기 바랍니다.

### 3단계: EIP 다이렉트 커넥트 활성화
1. [EIP 콘솔](https://console.cloud.tencent.com/cvm/eip?rid=1)에 로그인합니다.
2. 해당 EIP의 행을 찾아 오른쪽 작업란에서 [More]>[다이렉트 커넥트]를 클릭합니다.


### Windows CVM에 EIP 다이렉트 커넥트 설정
>
>- Windows 시스템의 EIP 다이렉트 커넥트는 개인 IP와 공인 IP에 각각 하나의 ENI가 필요합니다. 주 ENI에는 공인 IP를 설정하고, 보조 ENI에는 개인 IP를 설정하면 됩니다.
>- Windows에서 다이렉트 커넥트를 설정하는 과정에서 외부 네트워크 연결이 끊길 수 있습니다. 따라서 [VNC 로그인](https://intl.cloud.tencent.com/document/product/213/32496)을 사용하시기를 권장합니다.
- 주 ENI에 바인딩된 공인 IP가 EIP가 아니라면, 먼저는 EIP로 변경해야 합니다. 자세한 내용은 [공인 IP를 EIP로 변경](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip)을 참조 바랍니다.

#### 작업 시나리오
Windows 스크립트는 주 ENI는 외부 네트워크 트래픽으로, 보조 ENI는 내부 네트워크 트래픽으로 통하도록 하는 시나리오를 대상으로 합니다.

#### 1단계: EIP 다이렉트 커넥트 스크립트 다운로드<span id="step1" />
EIP 다이렉트 커넥트 과정에서 네트워크 연결이 끊길 수 있으니 먼저 EIP 다이렉트 커넥트 스크립트를 CVM에 다운로드하시기 바랍니다.
CVM의 브라우저에서 아래의 링크를 열고 EIP 다이렉트 커넥트 스크립트를 다운로드하시기 바랍니다.
```
https://windows-1254277469.cos.ap-guangzhou.myqcloud.com/eip_windows_direct.bat
```

#### 2단계: 보조 ENI 설정
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/overview)에 로그인합니다.
2. CVM 리스트에서 설정할 CVM ID를 클릭한 뒤 상세 페이지로 이동합니다.
3. [ENI] 탭을 선택하고 [Bind ENI]를 클릭해 주 ENI와 서브넷이 같은 ENI 하나를 생성합니다.
![](https://main.qcloudimg.com/raw/2da530f15e824ff99858f08397687cf6.png)
4. 팝업창에서 [Create and Bind an ENI]를 선택해 관련 정보를 입력하고, IP 자동 할당을 선택한 다음 [OK]를 클릭합니다.
![](https://main.qcloudimg.com/raw/cb6fe49d3bbefd792355ade6e62f29f3.png)

#### 3단계: 주 ENI 다이렉트 커넥트 설정
1. [EIP 콘솔](https://console.cloud.tencent.com/cvm/eip?rid=1)에 로그인합니다.
2. 해당 주 ENI에 바인딩된 EIP의 행을 찾아 오른쪽 작업란에서 [More]>[다이렉트 커넥트]를 클릭합니다.

#### 4단계: CVM 내부에 IP 설정
1. 작업 과정에서 외부 네트워크 액세스가 끊길 수 있으니 CVM에 로그인 시 [VNC 로그인](https://intl.cloud.tencent.com/document/product/213/32496)을 사용하시기 바랍니다.
2. 운영 체제 인터페이스 왼쪽 하단의 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width:25px"> 모양을 선택하고, <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: -3px 0px;"> 모양을 클릭해 'Windows PowerShell' 창을 엽니다. `firewall.cpl `을 입력하고 엔터를 눌러 'Windows 방화벽' 페이지를 엽니다.
3. [Windows 방화벽 설정 또는 해제]를 클릭해 '설정 사용자 지정' 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/e6d6a44be911ec5f60a6205b6f47a2c7.png)
4. '개인 네트워크 설정'과 '공용 네트워크 설정'에서 각각 [Windows 방화벽 사용 안 함]을 선택하고 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/cdb7703dec781e98101f7f3fd7ecf71f.png)
5. [1단계](#step1)에서 다운로드한 스크립트를 더블 클릭하면 바로 실행할 수 있으며, 공인 IP 주소를 입력한 뒤 엔터를 두 번 연속 누르면 됩니다. 
6. 'Windows PowerShell' 창에 `ipconfig` 입력 후 엔터를 누르면 주 ENI 상의 IPv4 주소가 공용 네트워크 주소로 변경되어 있음을 확인할 수 있습니다.

>다이렉트 커넥트 설정을 완료한 후에는 주 ENI에 또다시 개인 IP를 설정하지 않도록 합니다. 이를 설정하게 되면 CVM에서 공용 네트워크에 액세스할 수 없습니다.

