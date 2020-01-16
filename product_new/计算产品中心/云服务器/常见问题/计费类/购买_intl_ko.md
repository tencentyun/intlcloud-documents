### CVM는 어떻게 구매합니까?

모든 사용자는 Tencent Cloud의 공식 웹 사이트에서 클라우드 서비스를 구매할 수 있습니다. 과금 방식에 따라 다르며, 종량제(초 단위에 따라 청구, 시간별 결제) 방식의 CVM이 있습니다. 자세한 내용은 [과금 방식](https://intl.cloud.tencent.com/document/product/213/2180)을 참조하십시오.
종량제 유형의 구매 과정에 대한 자세한 내용은 [구매 방식](https://intl.cloud.tencent.com/document/product/213/506)을 참조하십시오.

### CVM의 리전과 가용존의 종류와 선택 방법은 무엇이 있습니까?

CVM에서 선택 가능한 리전과 가용존에 대한 자세한 내용은 [리전과 가용존](https://intl.cloud.tencent.com/document/product/213/6091)을 참조하십시오.
리전과 가용존 선택에 대한 자세한 내용은 [리전과 가용존 선택 방법](https://intl.cloud.tencent.com/document/product/213/6091)을 참조하십시오.

### CVM는 현재 어떤 호스트 유형을 제공합니까?

CVM는 여러 인스턴스 사양을 제공하며, 자세한 내용은 [인스턴스 사양](https://intl.cloud.tencent.com/document/product/213/11518)을 참조하십시오. 사용자의 서비스 요구에 따라 적합한 인스턴스 유형을 선택할 수 있습니다.
- 갑자기 발생하는 서비스 피크에 대해 종량제 과금 방식를 선택할 수 있습니다. 인스턴스를 언제든 활성화 또는 폐기하여 인스턴스 실제 사용량에 따라 요금을 지불합니다. 요금 청구를 초 단위로 정확히 하여 비용을 최소화합니다. 

### CVM 구성 방안은 어떻게 선택합니까?

- 입문형: 개인 블로그 등의 소규모 웹 사이트와 같은 시작 단계의 개인 웹 사이트가 사용하기에 적합합니다.
- 기본형: 대규모 기업의 공식 사이트, 소규모 전자 상거래 웹 사이트 등의 일정한 액세스량이 있는 웹 사이트 또는 애플리케이션에 적합합니다.
- 보급형: 포털 사이트, SaaS 소프트웨어, 소규모 App과 같이 자주 사용하는 클라우드 컴퓨팅처럼 일정한 양의 컴퓨팅이 필요할 때 적합합니다.
- 응용형: 대규모 포털, 전자 상거래 웹 사이트, 게임 App과 같이 동시 접속 요구가 높은 애플리케이션 또는 CVM 네트워크 및 컴퓨팅 기능이 꼭 필요한 응용 시나리오에 적합합니다.

추천 사양이 부족한 경우 [모델 선택](https://buy.cloud.tencent.com/cvm?tabIndex=1)에서 실제 필요에 따라 구성 방안들을 비교할 수 있습니다. 또한, CVM를 구매한 후 필요에 따라 수시로 [인스턴스 구성 조정](https://intl.cloud.tencent.com/document/product/213/2178)을 진행할 수 있습니다.
> Windows CVM는 [공용망 게이트웨이](https://intl.cloud.tencent.com/document/product/215/4972)로 이용할 수 없으며, 공용망 게이트웨이 사용자는 [Linux CVM로 빠른 구성](https://cloud.tencent.com/doc/product/213/2936)을 참조하십시오.
>

### Windows Server 2003 CVM를 구매할 수 있습니까?

Microsoft가 2015년 7월 14일부터 Windows Server 2003과 Windows Server 2003 R2에 대한 확장 지원 서비스 제공을 중단함으로써 Tencent Cloud도 더 이상 Windows Server 2003 서버를 제공하지 않으므로 구매할 수 없습니다.

### 스토리지를 선택하는 방법은 무엇입니까?

신뢰성에 대한 요구가 높은 데이터의 경우 [CBS](https://intl.cloud.tencent.com/document/product/213/33000)를 사용하길 추천합니다. 데이터의 지속적인 스토리지 신뢰성을 보장하고자 한다면 [로컬 디스크](https://cloud.tencent.com/doc/product/213/5798)를 선택하지 마십시오.
액세스가 빈번하고 용량이 불안정한 데이터베이스의 경우 [Tencent CDB](https://cloud.tencent.com/product/cdb-overview)를 사용하길 추천합니다.

### 종량제 CVM에 대한 제한 사항은 무엇입니까?

구매 제한과 관련된 내용은 [인스턴스 구매 제한](https://intl.cloud.tencent.com/document/product/213/2664)을 참조하십시오.

### CVM 구매 방식에는 어떤 종류가 있습니까?

CVM는 공식 웹 사이트 구매 및 API 구매로 제공되는 두 가지 방식으로 구매할 수 있습니다.

### 호스트를 구매한 후 얼마 동안 사용할 수 있습니까?

구매한 CVM를 시스템에 설치 완료한 후, 서버가 **실행 중** 상태일 때 즉시 로그인해 사용할 수 있습니다.

### CVM 생성에 성공하지 못할 경우 어떻게 처리합니까?

서버 생성 프로세스가 오래 걸릴 경우 조금만 기다리며 성공 여부를 확인해 주십시오. 만약 생성이 실패했을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)로 발생한 문제를 보고하여 엔지니어의 도움으로 문제를 해결하십시오.

### CVM가 전송을 실패할 경우 어떻게 폐기합니까?

[티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 고객서비스로 연락하여 머신 정보에 대한 화면 캡처와 폐기할 수 없는 상황에 대한 화면 캡처를 제공해 주십시오. **전송 실패**로 명시할 경우 문제처리에 도움이 됩니다.
