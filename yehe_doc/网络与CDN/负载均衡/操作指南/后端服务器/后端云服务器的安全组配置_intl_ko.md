## CVM 보안 그룹 개요
CLB의 백엔드 CVM 인스턴스는 방화벽 역할을 하는 [보안 그룹](https://intl.cloud.tencent.com/document/product/213/12452)을 통해 액세스 제어를 수행할 수 있습니다.
하나 이상의 보안 그룹을 백엔드 CVM과 연결하고 각 보안 그룹에 하나 이상의 규칙을 추가하여 서로 다른 서버의 트래픽 액세스 권한을 제어할 수 있습니다. 보안 그룹에 대한 규칙은 언제든지 수정할 수 있으며 새 규칙은 해당 보안 그룹과 연결된 모든 인스턴스에 자동으로 적용됩니다. 자세한 내용은 [보안 그룹](https://intl.cloud.tencent.com/document/product/213/12452)을 참고하십시오. [VPC](https://intl.cloud.tencent.com/document/product/215/535) 환경에서 [Network ACLs](https://intl.cloud.tencent.com/document/product/215/31850)를 사용하여 액세스를 제어할 수도 있습니다.

## CVM 보안 그룹 구성
Client IP를 허용하고 CVM 보안 그룹에서 서비스 포트를 열어야 합니다.
CLB 인스턴스를 사용하여 비즈니스 트래픽을 CVM 인스턴스로 포워딩하려는 경우 효과적인 상태 확인을 위해 CVM 보안 그룹을 다음과 같이 구성해야 합니다.
1. 공중망 CLB: CLB 인스턴스가 VIP를 사용하여 백엔드 CVM의 상태를 확인할 수 있도록 백엔드 CVM의 보안 그룹에서 CLB VIP를 허용해야 합니다.
2. 사설망 CLB:
   - 사설망 CLB(이전의 ‘애플리케이션 사설망 CLB’)의 경우 CLB 인스턴스가 VPC에 있는 경우 상태 확인을 위해 백엔드 CVM의 보안 그룹에서 CLB VIP를 허용해야 합니다. CLB 인스턴스가 기본 네트워크에 있는 경우 기본적으로 상태 확인 IP가 허용되므로 추가 구성이 필요하지 않습니다.

## CVM 보안 그룹 구성 예시
이 예시는 CLB를 통해 CVM에 액세스할 때 CVM 보안 그룹을 구성하는 예시를 보여줍니다. [Configuring CLB Security Group
](https://intl.cloud.tencent.com/document/product/214/14733)을 참고하여 CLB 보안 그룹의 규칙을 구성합니다.
- **적용 시나리오1:**
TCP:80 리스너 및 백엔드 서비스 포트 8080으로 구성된 공중망 CLB의 경우 Client IP(ClientA IP 및 ClientB IP)만 CLB에 액세스하도록 허용하려면 백엔드 CVM 보안 그룹의 인바운드 규칙을 다음과 같이 구성해야 합니다.
```
ClientA IP + 8080 allow
ClientB IP + 8080 allow
CLB VIP    + 8080 allow
0.0.0.0/0  + 8080 drop
```
- **적용 시나리오2:**
HTTP:80 리스너 및 백엔드 서비스 포트 8080으로 구성된 공중망 CLB의 경우 모든 Client IP가 CLB에 액세스하도록 허용하려면 백엔드 CVM 보안 그룹의 인바운드 규칙을 다음과 같이 구성해야 합니다.
```
0.0.0.0/0 + 8080 allow
```
- **적용 시나리오3:**
CVM 보안 그룹의 CLB VIP가 상태 확인을 수행하도록 허용합니다. VPC를 사용하고 TCP:80 리스너와 리얼 서버 포트 8080으로 구성된 사설망 CLB(이전의 ‘애플리케이션 사설망 CLB’)의 경우, Client IP(ClientA IP 및 ClientB IP)만 CLB에 액세스하도록 허용하고 VIP 및 CLB에 바인딩된 백엔드 CVM에만 액세스하도록 Client IP를 제한하려면,
   - a.  리얼 서버에 대한 보안 그룹 인바운드 규칙을 다음과 같이 구성합니다.
```
ClientA IP + 8080 allow
ClientB IP + 8080 allow
CLB VIP    + 8080 allow
0.0.0.0/0  + 8080 drop
```
    - b.  Client로 사용되는 서버에 대한 보안 그룹 아웃바운드 규칙을 다음과 같이 구성합니다.
```
CLB VIP    + 8080 allow
0.0.0.0/0  + 8080 drop
```

- **적용 시나리오4: 블록리스트**
일부 Client IP가 액세스 요청을 거부하도록 블록리스트를 구성해야 하는 경우 클라우드 서비스와 연결된 보안 그룹을 구성할 수 있습니다. 보안 그룹 규칙은 다음과 같이 구성해야 합니다.
  - 거부할 Client IP + 포트를 보안 그룹에 추가하고 정책 열에서 이 IP의 액세스를 거부하는 옵션을 선택합니다.
  - 기본적으로 모든 IP에서 포트에 대한 액세스 요청을 허용하도록 위의 구성을 완료한 후 다른 보안 그룹 규칙을 추가합니다.
구성이 완료되면 보안 그룹 규칙은 다음과 같습니다.
```
clientA IP + port drop
clientB IP + port drop
0.0.0.0/0  + port accept
```
   >!
   >- 상기 단계를 **지정된 순서대로 엄격하게** 따르십시오. 그렇지 않으면 블록리스트 구성이 실패할 수 있습니다.
   >- 보안 그룹은 상태를 저장합니다. 위의 구성은 모두 **인바운드 규칙**의 구성입니다.
   >

## CVM 보안 그룹 운영 가이드
### 콘솔을 사용하여 백엔드 CVM 보안 그룹 관리
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인하고 해당 CLB 인스턴스 ID를 클릭하여 CLB 세부 정보 페이지로 이동합니다.
2. CLB에 바인딩된 CVM 페이지에서 대상 백엔드 CVM ID를 클릭하여 CVM 세부 정보 페이지로 이동합니다.
3. **보안 그룹** 탭을 클릭합니다. 탭에서 보안 그룹을 바인딩/바인딩 해제합니다.

### Tencent Cloud API를 사용하여 백엔드 CVM 보안 그룹 관리
[AssociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33265) 및 [DisassociateSecurityGroups](https://intl.cloud.tencent.com/document/product/213/33253)를 참고하십시오.

