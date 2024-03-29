COSBrowser 모바일 버전의 데이터 개요 기능은 지난 30일 동안의 Cloud Object Storage(COS) 데이터 사용량을 표시하며 총 트래픽, 총 읽기 및 쓰기 요청, 스토리지 추세, 트래픽 추세(공용 네트워크 다운스트림 트래픽, 사설 네트워크 트래픽, CDN Origin-pull 트래픽), 요청 수 추세, 유효 요청 비율 추세, 검색된 스탠다드 IA 데이터량 및 검색된 아카이브 데이터량이 표시됩니다.

>? 
> - 현재 모바일 버전에서는 서브 계정으로 데이터를 볼 수 없습니다. [데이터 개요 조회](https://intl.cloud.tencent.com/document/product/436/36542)의 안내에 따라 서브 계정에 로그인하여 콘솔에서 데이터를 볼 수 있습니다.
> - 이 기능의 데이터는 실시간이 아니며 약 2시간의 지연이 있으므로 참고용입니다. [데이터 개요 조회](https://intl.cloud.tencent.com/document/product/436/36542)에 안내된 대로 콘솔에서 보다 정확한 청구 및 사용 데이터를 볼 수 있습니다.
> 

<span id="UsageOverview"></span>
## 사용량 개요
COSBrowser는 객체 수, 스토리지 사용량, 요청 수 및 트래픽을 볼 수 있는 스토리지 데이터 개요 페이지를 제공합니다.


<span id="BucketMonitoring"></span>
## 버킷 모니터링

COSBrowser는 버킷별 데이터 개요를 제공합니다. 다음 두 가지 방법으로 버킷 모니터링 데이터를 볼 수 있습니다.

1. 하단의 **홈**을 탭하고 **사용자 개요**를 탭하여 버킷 간에 전환하여 모니터링 데이터를 봅니다.

2. 하단의 **리소스**를 탭하고 대상 버킷 오른쪽의 **더 보기**를 탭합니다. 팝업된 작업 리스트에서 **모니터링**을 탭하여 버킷 페이지로 이동합니다.


<span id="TheWidget"></span>
## 위젯
COSBrowser는 홈 화면에 위젯으로 추가할 수 있어 COSBrowser를 열지 않고도 언제 어디서나 모니터링 데이터를 볼 수 있습니다.

### 위젯 추가

1. iPhone에 iOS용 COSBrowser를 다운로드하여 설치합니다. 그런 다음 App이 흔들릴 때까지 홈 스크린의 빈 영역을 길게 터치하고 왼쪽 상단 모서리의 <b>+</b>를 탭합니다.

2. COSBrowser를 찾아서 탭합니다.

3. 레이아웃을 선택하고 하단의 위젯 추가를 탭합니다.




### 표시된 데이터 사용자 정의
위젯을 사용하면 표시할 데이터 범위를 사용자 지정할 수 있습니다. 추적 및 모니터링을 위해 특정 버킷 또는 스토리지 클래스를 지정할 수 있습니다. 표시할 수 있는 스토리지 클래스는 스탠다드, 스탠다드 IA 및 아카이브입니다.

구체적인 작업 순서는 다음과 같습니다.
1. iOS용 COSBroswer를 열고 **Me** > **설정** > **위젯 구성**을 탭하여 위젯 설정 페이지로 들어갑니다.

2. 구성 항목을 다음과 같이 설정합니다.

 - **버킷 선택**: 버킷을 선택하지 않은 경우 현재 계정의 모든 버킷에 대한 개요 데이터가 표시됩니다. 버킷을 선택하면 개요 데이터가 표시됩니다.
 - **스토리지 유형 선택**: 위젯은 기본적으로 스탠다드 스토리지 유형의 모니터링 데이터를 표시합니다. 스탠다드 IA 및 아카이브와 같은 다른 스토리지 유형을 수동으로 선택할 수 있습니다.

>? 구성된 버킷 및 스토리지 유형을 빠르게 재설정하려면 재설정을 탭하기만 하면 됩니다. 그러면 현재 계정의 스탠다드 스토리지 유형에 있는 모든 버킷의 모니터링 데이터가 표시됩니다.
>

### 위젯 제거

위젯을 길게 터치하고 위젯 제거를 탭합니다.


