[ENI](https://intl.cloud.tencent.com/product/eni)(Elastic Network Interface, ENI)는 VPC 내의 CVM을 바인딩하는 일종의 탄력적 네트워크 인터페이스로서 여러 CVM 사이에서 자유롭게 마이그레이션할 수 있습니다. ENI는 관리 네트워크 설정 및 신뢰도 높은 네트워크 솔루션의 구축에 큰 도움이 됩니다.

ENI는 VPC, 가용존 및 서브넷 속성을 갖고 있어 동일한 가용존의 CVM만 바인딩할 수 있습니다. 1대의 CVM는은 여러 ENI를 바인딩할 수 있으며 구체적인 바인딩 수량은 CVM 규격에 따라 결정됩니다.

## 개념

 - **주 ENI 및 보조 ENI:** VPC의 CVM 구축 시 연동 생성된 ENI가 주ENI이고, 사용자가 자체 생성한 ENI는 보조 ENI가 됩니다. 그중 주 ENI는 바인딩 및 바인딩 해제를 지원하지만, 보조 ENI는 바인딩 및 바인딩 해제를 지원하지 않습니다.
 - **주 개인 IP:** ENI의 주 개인IP는 ENI 생성 시 시스템에서 랜덤으로 할당하거나 사용자가 자체 설정할 수 있습니다. 주 ENI의 주 개인 IP는 수정할 수 있으나, 보조 ENI의 주 개인IP는 수정할 수 없습니다.
 - **보조 개인 IP:** ENI의 주IP 외에 바인딩된 보조 개인 IP는 사용자가 ENI를 생성 또는 편집 시 자체 설정할 수 있으며 바인딩 및 해제할 수 있습니다.
 - **EIP:** ENI의 개인 IP와 하나씩 바인딩해야 합니다.
 - **보안 그룹:** ENI는 하나 또는 하나 이상의 보안 그룹을 바인딩할 수 있습니다.
 - **MAC 주소:** ENI는 전역에서 유니크한 MAC 주소를 보유합니다.

## 응용 시나리오
- **내부 네트워크, 외부 네트워크, 관리 네트워크 격리**:
중요한 비즈니스를 네트워크에 배포하려면 일반적으로 데이터 전송 내부 네트워크, 외부 네트워크 및 관리 네트워크를 격리해야 하며, 서로 다른 라우팅 정책 및 보안 그룹 정책을 통해 네트워크 간의 데이터 보안 및 네트워크 격리를 보장합니다. CVM에 3개의 서로 다른 서브넷에 위치한 ENI를 바인딩하여, 물리 서버와 같이 3중 네트워크 격리를 구현할 수 있습니다.
- **신뢰도 높은 애플리케이션 배포: **
시스템 아키텍처의 주요 컴포넌트는 모두 핫 백업을 통해 시스템의 고가용성을 보장합니다. Tencent Cloud는 ENI 와 개인 IP를 자유롭게 바인딩 및 바인딩 해제하며, Keepalived의 재해 복구를 설정하여 주요 컴포넌트의 고가용성 배포를 지원합니다.

## 사용 제한

CPU와 메모리 설정에 따라 CVM이 바인딩할 수 있는 ENI 수와 단일 ENI가 바인딩할 수 있는 개인 IP 수는 크게 다르며, ENI 및 단일 ENI IP 할당 수는 아래 표와 같습니다.
> 단일 ENI의 바인딩 IP 수량은 ENI로 바인딩할 수 있는 IP 수의 최대 수량만 표시하고, 최대 수량에 따라 EIP 할당을 제공하지 않으며 계정의 EIP 할당은 EIP [사용 제한](https://intl.cloud.tencent.com/zh/document/product/213/5733)에 따라 제공됩니다.

| CVM 설정               | ENI 수| 단일 ENI가 바인딩한 개인 IP 수 |
| ------------------- | :---- | :------ |
| CPU: 싱글코어   </br>메모리: 1GB    | 2     | 2       |
| CPU: 싱글코어   </br>메모리: > 1GB   | 2     | 6       |
| CPU: 듀얼코어             | 2     | 10      |
| CPU: 쿼드코어   </br>메모리: < 16GB | 4     | 10      |
| CPU: 쿼드코어   </br>메모리: > 16GB | 4     | 20      |
| CPU: 옥타코어 - 도데카코어          | 6     | 20      |
| CPU: > 도데카코어           | 8     | 30      |


## API 개요

아래의 테이블과 같이 ENI 및 CVM 관련 API 인터페이스가 이곳에 표시됩니다. 더 자세한 ENI 관련 조작은 [ENI API개요](https://intl.cloud.tencent.com/zh/document/product/215/15755#.E5.BC.B9.E6.80.A7.E7.BD.91.E5.8D.A1.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3)를 참고하시기 바랍니다.

| 인터페이스 기능 | Action ID |  기능 설명 |
|---------|---------|---------|
| ENI 생성 | [CreateNetworkInterface](https://intl.cloud.tencent.com/zh/document/api/215/15818)  |  ENI 생성 |
| ENI 개인 IP 신청  | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/zh/document/api/215/15813) | ENI 개인 IP 신청 |
| ENI 바인딩 CVM | [AttachNetworkInterface](https://intl.cloud.tencent.com/zh/document/api/215/15819) | ENI 바인딩 CVM |
