
## 소개
CLS는 Ckafka 인스턴스를 통해 로그 토픽 데이터를 소비할 수 있습니다. 다음은 로그 토픽 Ckafka 소비 기능을 사용하는 방법에 대한 자세한 설명입니다.

## 전제 조건

Tencent Cloud 메시지 대기열(CKafka)을 활성화하고 Ckafka 소비 인스턴스 및 메시지 대기열 토픽이 로그 토픽의 지역 내 생성되었습니다.

>?Ckafka 인스턴스 생성하기는 [Ckafka 인스턴스 생성](https://cloud.tencent.com/document/product/597/30931)을 참조하십시오. Ckafka 사용 방법은 [Ckafka 시작 가이드](https://cloud.tencent.com/document/product/597/10112)를 참조하십시오.

## 작업 절차

1. [CLS 콘솔](https://console.cloud.tencent.com/cls)에 로그인합니다.
2. 왼쪽 탐색 모음에서 [로그 집합 관리]를 클릭합니다.
3. Ckafka 소비를 구성할 로그 집합 ID/이름을 클릭하여 로그 집합 세부 정보 페이지로 이동합니다.
4. 소비하고자 하는 로그 토픽을 찾아 오른쪽의 [구성 관리] > [실시간 소비]를 클릭하여 Ckafka 소비 구성 페이지로 들어갑니다.
![1](https://main.qcloudimg.com/raw/85294af3a9d71265e5cc535b17a58057.png)
5. 페이지의 오른쪽에서 [편집]을 클릭하여 Ckafka 소비 구성 페이지로 들어갑니다.
6. Ckafka 소비 스위치를 켜고 소비할 Ckafka 인스턴스와 해당 메시지 대기열 토픽을 선택합니다.
![2](https://main.qcloudimg.com/raw/ebfac8224553db1011d0d14a3a812cb3.png)
7. Ckafka 소비를 시작하려면 [저장]을 클릭합니다. Ckafka 소비 상태가 "활성화됨"으로 표시되면 시동이 성공했음을 의미합니다.
![](https://main.qcloudimg.com/raw/1ac6ee333d54e068451a68fbcf71af18.png)



