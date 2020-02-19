### ENI란 무엇입니까?

[ENI](https://intl.cloud.tencent.com/product/eni)(Elastic Network Interface)는 VPC 내의 CVM을 바인딩하는 일종의 탄력적 네트워크 인터페이스로서 여러 CVM 사이에서 자유롭게 마이그레이션할 수 있습니다. ENI는 관리 네트워크 구성 및 신뢰성 높은 네트워크 솔루션 구축에 큰 도움이 됩니다.

ENI는 VPC, 가용존 및 서브넷 속성을 갖고 있어 동일한 가용존의 CVM만 바인딩할 수 있습니다. 1대의 CVM는 여러 ENI를 바인딩할 수 있으며 구체적인 바인딩 수량은 CVM 규격에 따라 결정됩니다.

### CVM가 ENI를 사용할 경우 어떤 제한을 받습니까?

이용 제한에 대한 자세한 내용은 [ENI 관련 제한](https://intl.cloud.tencent.com/document/product/213/15379) 부분을 참조하십시오.

### ENI의 기본 정보는 무엇입니까?

자세한 내용은 [ENI 소개](https://intl.cloud.tencent.com/document/product/213/6514) **관련 개념**부분을 참조하십시오.

### ENI를 어떻게 생성합니까?

[ENI 생성](https://intl.cloud.tencent.com/document/product/576/18534)을 참조하십시오.

### ENI를 어떻게 조회합니까?

[ENI 조회](https://intl.cloud.tencent.com/document/product/576/18533)를 참조하십시오.

### ENI를 CVM 인스턴스에 바인딩하려면 어떻게 해야 합니까?

[CVM 바인딩 및 구성](https://intl.cloud.tencent.com/document/product/576/18535)을 참조하십시오.

### CVM 인스턴스 내의 ENI를 어떻게 구성합니까?

[CVM 바인딩 및 구성](https://intl.cloud.tencent.com/document/product/576/18535)을 참조하십시오.

### ENI의 개인 IP를 수정 및 사용자 정의 어떻게 합니까?

VPC 내의 CVM는 ENI개인 IP를 수정 및 사용자 정의할 수 있으며 콘솔 작업 순서는 다음과 같습니다.

1. [VPC 콘솔](https://console.cloud.tencent.com/vpc/vpc?rid=1)에 로그인하십시오.
2. 왼쪽 사이드바에서 [IP 및 ENI]>[ENI]를 클릭하고 ENI 리스트 페이지로 진입하십시오.
3. ENI의[ ID/이름]을 클릭하고 ENI 상세 페이지로 진입해 ENI 정보를 조회하십시오.
4. [IPv4 주소 관리]페이지 탭을 선택하고 [개인 IP 할당]을 클릭하십시오.
5. 팝업 창에서 IP 할당 방식으로 **수동 입력**을 선택하고 수정할 IP 주소를 입력하십시오.
6. [확인]을 클릭하고 작업을 완료하십시오.

콘솔을 수정한 후, ENI의 구성 파일을 동기화 및 수정해야 하므로 자세한 내용은 [CVM 바인딩 및 구성](https://intl.cloud.tencent.com/document/product/576/18535)을 참조하십시오.
