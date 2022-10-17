CLB 인스턴스가 생성된 후 공중망 트래픽을 격리하도록 CLB 보안 그룹을 구성할 수 있습니다. 본문은 다양한 모드에서 CLB 보안 그룹을 구성하는 방법을 설명합니다.
## 사용 제한
- 하나의 CLB 인스턴스는 최대 5개의 보안 그룹에 바인딩될 수 있습니다.
- 보안 그룹에는 최대 512개의 규칙이 허용됩니다.
- 보안 그룹은 기본 네트워크의 사설망 CLB 인스턴스에 바인딩할 수 없습니다. 사설망 CLB가 [Anycast EIP](https://intl.cloud.tencent.com/document/product/214/32426)에 바인딩되어 있는 경우 해당 인스턴스에 바인딩된 보안 그룹은 적용되지 않습니다.
- 기본적으로 허용은 기본 네트워크 기반 CLB에 사용할 수 없습니다.

## 배경 정보
보안 그룹은 스테이트풀 데이터 패킷을 필터링하고 인스턴스 레벨에서 아웃바운드/인바운드 트래픽을 제어할 수 있는 가상 방화벽입니다. 자세한 내용은 [보안 그룹 개요](https://intl.cloud.tencent.com/document/product/213/12452)를 참고하십시오.

CLB 보안 그룹은 CLB 인스턴스에 바인딩되고 CVM 보안 그룹은 CVM 인스턴스에 바인딩됩니다. 그들은 다른 객체를 대상으로 합니다. CLB 보안 그룹의 경우 다음을 선택할 수 있습니다.
- [기본 허용 활성화](#open-security-group)
- [기본 허용 비활성화](#close-security-group)

>?
>- IPv4 CLB 보안 그룹의 경우 기본적으로 허용은 기본적으로 비활성화되어 있으며 콘솔에서 활성화할 수 있습니다.
>- IPv6 CLB 보안 그룹의 경우 기본적으로 허용이 기본적으로 활성화되어 있으며 비활성화할 수 없습니다.


### 기본 허용 활성화[](id:open-security-group)
![](https://main.qcloudimg.com/raw/0d2b50ca557d805ce5790fcdd3974b40.jpg)
기본 허용이 활성화된 경우:
<ul ><li>지정된 Client IP에서만 액세스를 허용하려면 해당 IP와 CLB 보안 그룹의 Client IP 및 수신 대기 포트를 <strong>허용해야</strong> 하지만 백엔드 CVM 보안 그룹의 Client IP 및 서비스 포트를 <strong>허용할 필요는 없습니다.</strong> 실제 서버는 기본적으로 CLB의 트래픽을 허용하므로 CLB의 액세스 트래픽은 CLB 보안 그룹을 통해서만 전달됩니다.</li>
<li>공중망 IP(일반 공중망 IP 및 EIP 포함)의 트래픽은 여전히 CVM 보안 그룹을 통과해야 합니다.</li>
<li>CLB 인스턴스에 보안 그룹이 구성되지 않은 경우 모든 트래픽이 허용되며 CLB 인스턴스의 VIP에 리스너로 구성된 포트에만 액세스할 수 있습니다. 따라서 수신 포트는 모든 IP의 트래픽을 허용합니다.</li>
<li>지정된 Client IP의 트래픽을 거부하려면 CLB 보안 그룹에서 구성해야 합니다. CVM 보안 그룹의 Client IP 거부는 CLB의 트래픽에는 적용되지 <strong>않고</strong> 공중망 IP(일반 공중망 IP 및 EIP 포함)의 트래픽에만 적용됩니다.</li></ul>


### 기본 허용 비활성화[](id:close-security-group)
![](https://main.qcloudimg.com/raw/9357f8d81a0027110bd6a977cda4aafc.jpg)
기본 허용이 비활성화된 경우:</p>

<ul ><li>지정된 Client IP에서만 액세스를 허용하려면 CLB 보안 그룹의 Client IP 및 수신 대기 포트를 <strong>허용하고</strong> 백엔드 CVM 보안 그룹의 Client IP 및 서비스 포트도 <strong>허용해야 합니다.</strong> 따라서 CLB를 통과하는 비즈니스 트래픽은 CLB 보안 그룹과 CVM 보안 그룹 모두에서 이중으로 확인됩니다.</li>
<li>공중망 IP(일반 공중망 IP 및 EIP 포함)의 트래픽은 여전히 CVM 보안 그룹을 통과해야 합니다.</li>
<li>CLB 인스턴스에 보안 그룹이 구성되어 있지 않으면 CVM 보안 그룹을 통과하는 트래픽만 허용됩니다.</li>
<li>CLB 보안 그룹 또는 CVM 보안 그룹에 대한 액세스를 거부하여 지정된  Client IP의 트래픽을 거부할 수 있습니다.</li></ul>
<p >기본 허용이 비활성화된 경우 효과적인 상태 확인을 위해 CVM 보안 그룹을 다음과 같이 구성해야 합니다.</p>
<ol ><li>공중망 CLB 구성<br>CLB가 VIP를 사용하여 백엔드 CVM 상태를 감지할 수 있도록 백엔드 CVM 보안 그룹에서 CLB VIP를 허용해야 합니다.</li>
<li>사설망 CLB 구성<ul><li>사설망 CLB(이전의 ‘사설망 애플리케이션 CLB’)의 경우 CLB 인스턴스가 VPC에 있는 경우 상태 확인을 위해 백엔드 CVM 보안 그룹에서 CLB VIP를 허용해야 합니다. CLB 인스턴스가 기본 네트워크에 있는 경우 기본적으로 상태 확인 IP가 허용되므로 추가 구성이 필요하지 않습니다.</li></ul></li></ol>

## 작업 단계
다음 예시에서는 포트 80에서 CLB로의 인바운드 트래픽만 허용하도록 보안 그룹을 구성하고 CVM 포트 8080을 통해 서비스를 제공합니다. Client IP에는 제한이 없습니다.
> !이 예시에서 사용된 공중망 CLB 인스턴스의 경우 상태 확인을 위해 백엔드 CVM 보안 그룹에서 CLB VIP를 허용해야 합니다. 현재 IP는 `0.0.0.0/0`으로 설정되어 모든 IP가 허용됩니다.

### 1단계: CLB 인스턴스 및 리스너 생성 및 CVM에 바인딩

자세한 내용은 [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975)를 참고하십시오. HTTP:80 리스너가 생성되어 이 예시에서 서비스 포트가 8080인 백엔드 CVM 인스턴스에 바인딩됩니다.
<img alt="" src="https://main.qcloudimg.com/raw/9ec487d62b6092e6f5b14c1791ef5f4e.png" >

### 2단계: CLB 보안 그룹 구성
1. CLB 보안 그룹 규칙 구성<br><a rel="nofollow" href="https://console.cloud.tencent.com/cvm/securitygroup">보안 그룹 콘솔</a>에 로그인하여 보안 그룹 규칙을 구성합니다. 인바운드 규칙에서는 모든 IP(즉, `0.0.0.0/0`)의 포트 80에서 오는 요청을 허용하고 다른 포트에서 오는 트래픽을 거부합니다.
> ?
> - 보안 그룹 규칙은 위에서 아래로 적용되도록 선별됩니다. 새 규칙이 적용되면 다른 규칙은 기본적으로 거부됩니다. 따라서 순서에 주의하십시오. 자세한 내용은 <a rel="nofollow" href="https://intl.cloud.tencent.com/document/product/215/38750">보안 그룹 개요</a>를 참고하십시오.
> - 보안 그룹에는 인바운드 및 아웃바운드 규칙이 있습니다. 위의 구성은 인바운드 트래픽을 제한하기 위한 것이므로 <strong>인바운드 규칙</strong>이지만 아웃바운드 규칙은 특별히 구성할 필요가 없습니다.
>
  ![](https://main.qcloudimg.com/raw/65b035098c49c77f4a82eed799353bc4.png) 

2. 보안 그룹을 CLB 인스턴스에 바인딩
 1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인합니다.
 2. ‘인스턴스 관리’ 페이지에서 대상 CLB 인스턴스의 ID를 클릭하십시오.
 3. 인스턴스 세부 정보 페이지에서 [보안 그룹] 탭을 클릭하고 ‘바인딩된 보안 그룹’ 모듈에서 [바인딩]을 클릭합니다.
 4. 팝업되는 ‘보안 그룹 구성’ 창에서 CLB 인스턴스에 바인딩된 보안 그룹을 선택하고 [확인]을 클릭합니다.
       ![](https://main.qcloudimg.com/raw/8a9701e700a94ba55a9a650eb87b4456.png) 
     CLB 보안 그룹 구성이 완료되어 포트 80에서만 CLB에 액세스할 수 있습니다.
     <img alt="" src="https://main.qcloudimg.com/raw/a32cd86653185a5138006757aab38075.png" >

### 3단계: 기본 허용 구성
다음과 같이 다양한 구성으로 기본 허용을 활성화 또는 비활성화할 수 있습니다.
- 방법1: 기본 허용을 활성화하여 실제 서버에서 포트를 허용할 필요가 없도록 합니다.
>?이 기능은 기본 네트워크의 CLB에 대해 지원되지 않습니다.
- 방법2: 기본 허용을 비활성화합니다. CVM 보안 그룹에서 Client IP(이 예시에서는 0.0.0.0/0)도 허용해야 합니다.

#### 방법1: 기본 허용 활성화
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인합니다.
2. ‘인스턴스 관리’ 페이지에서 대상 CLB 인스턴스의 ID를 클릭합니다.
3. 인스턴스 세부 정보 페이지에서 [보안 그룹] 탭을 클릭합니다.
2. ‘보안 그룹’ 탭에서 <img style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png">을 클릭하여 기본 허용을 활성화합니다.
3. 기본 허용이 활성화되면 아래와 같이 <strong>규칙 미리보기</strong>에서 보안 그룹 규칙만 확인하면 됩니다.
    ![](https://main.qcloudimg.com/raw/6caa47138ecb97cc3c60cb38971792fd.png)

#### 방법2: 기본 허용 비활성화
기본 허용이 비활성화된 경우 CVM 보안 그룹에서 Client IP를 허용해야 합니다. 비즈니스 트래픽은 CLB 포트 80에서만 CVM에 액세스하고 CVM 포트 8080에서 제공하는 서비스를 사용할 수 있습니다.
>?지정된 Client IP의 트래픽을 허용하려면 CLB 보안 그룹과 CVM 보안 그룹 모두에서 해당 IP를 허용해야 합니다. CLB에 보안 그룹이 없는 경우 CVM 보안 그룹에서 IP를 허용하십시오.
>
1. CVM 보안 그룹 규칙 구성
   백엔드 CVM 인스턴스에 액세스하는 트래픽에 대해 서비스 포트에서만 액세스를 허용하도록 CVM 보안 그룹을 구성할 수 있습니다. <br>[보안 그룹 콘솔](https://console.cloud.tencent.com/cvm/securitygroup)로 이동하여 보안 그룹 정책을 구성합니다. 인바운드 규칙에서는 모든 IP의 모든 포트 8080입니다. 원활한 원격 CVM 로그인 및 Ping 서비스를 위해 보안 그룹에서 22, 3389 및 ICMP 서비스를 엽니다.
   ![](https://console.cloud.tencent.com/cvm/instance/index?rid=1)
2. 보안 그룹을 CVM 인스턴스에 바인딩합니다.
 1. [CVM 콘솔](https://console.intl.cloud.tencent.com/cvm/instance/index?rid=1)에서 CLB 인스턴스에 바인딩된 CVM 인스턴스의 ID를 클릭하여 세부 정보 페이지로 이동합니다.
 2. [보안 그룹] 탭을 선택하고 ‘바인딩된 보안 그룹’ 모듈에서 [바인딩]을 클릭합니다.
 3. ‘보안 그룹 구성’ 팝업 창에서 CVM 인스턴스에 바인딩된 보안 그룹을 선택하고 [확인]을 클릭합니다.       <img alt="" src="https://main.qcloudimg.com/raw/6e0e1c2f834bb7425ef3ca010114165a.png" title="클릭해서 원본 이미지 보기">

