데이터 구독 Kafka 버전은 사용자가 여러 개의 소비자 그룹을 만들어 다지점 소비를 할 수 있도록 지원합니다. 소비자 그룹을 여러 개 만들면 사용자가 여러 번 소비할 수 있기 때문에 소비 채널은 늘리고 사용 비용은 줄임과 동시에 소비 데이터 속도를 향상시킬 수 있습니다.

## 전제 조건
[데이터 구독 Kafka 버전](https://intl.cloud.tencent.com/document/product/571/39531)이 생성되어 있어야 합니다.
>?데이터 구독 리스트에서 'kafka 버전' 마크가 있는 구독은 데이터 구독 Kafka 버전으로, 다음 이미지와 같습니다.

## 주의사항
- 데이터 구독 작업의 상태는 항상 실행 중이어야 합니다.
- 하나의 데이터 구독 작업은 최대 10개의 소비자 그룹을 생성할 수 있습니다.
- 하나의 소비자 그룹에 있을 수 있는 소비할 소비자의 수는 한 명입니다.

## 작업 순서
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/dss)에 로그인한 뒤 왼쪽 메뉴에서 [데이터 구독]을 선택해 데이터 구독 페이지로 이동합니다.
2. 데이터 구독 리스트에서 원하는 데이터 구독을 선택한 후 구독 이름 또는 '작업'열의 [구독 상세 보기]를 클릭해 구독 관리 페이지로 이동합니다.
3. 구독 관리 페이지에서 [소비자 관리] 페이지를 선택해 [신규 소비자 그룹]을 클릭합니다.
4. 팝업된 창의 소비 생성 대화 상자에서 소비자 그룹 정보를 설정해 [생성]을 클릭합니다.
 - 소비자 그룹 명칭: 실제 상황에 맞춰 소비자 그룹 명칭을 설정하면 사용과 식별이 용이합니다.
 - 계정: 소비자 그룹 계정을 설정합니다.
 - 비밀번호: 소비자 그룹 계정의 비밀번호를 설정합니다.
 - 비밀번호 확인: 동일한 비밀번호를 다시 한 번 입력합니다.
 - 비고: 비고 정보를 설정하면 기록이 편리합니다.

