MPS를 통해 MPS로 생성되는 콜백 작업을 SCF를 사용해 즉시 COS에 백업하는 표준 솔루션이며, MPS가 SCF에 템플릿을 설정해 사용자가 사용할 수 있도록 제공하는 시나리오입니다. 이 시나리오는 MPS와 SCF를 사용하며, 여기서 MPS는 비디오 처리 작업에 사용되고 SCF는 콜백 메시지 처리를 제공하며 COS는 단말에 영구적인 스토리지 성능을 제공합니다.

## 작업 단계
### 1단계: SCF 생성
1. [SCF 콘솔](https://console.cloud.tencent.com/scf/list)에 로그인하고 페이지의 왼쪽 사이드바에서 **[함수 서비스](https://console.cloud.tencent.com/scf/list)**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d19e5af310ff9e75498bba4f7d63abc4.png)
2. 함수 서비스 페이지 상단에서 **베이징** 리전을 선택하고 **생성**을 클릭해 함수 생성 페이지로 이동합니다.
3. 아래 매개변수 정보를 다음 이미지와 같이 설정합니다.
  - **생성 방식**: 템플릿 생성을 선택합니다.
  - **퍼지 검색**: 'CLS 메시지 COS에 덤프'를 입력하고 검색합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8b25b3314ee4ad6040a888b48e0ab889.png)
>? 템플릿의 **상세 보기**를 클릭하면 ‘템플릿 상세 정보’ 창이 팝업되고 관련 정보를 확인할 수 있으며, 다운로드 작업을 지원합니다.
4. **다음 단계**를 클릭하여 함수 설정 페이지로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/daf1fa4f6c4bb4f402a3db5826b46c9a.png)
5. 기본 설정을 유지하고 **완료**를 클릭하면 함수 생성이 완료됩니다.

### 2단계: MPS 트리거 설정
1. **[SCF 콘솔](https://console.cloud.tencent.com/scf)** 페이지의 왼쪽 사이드바에서 **[함수 서비스](https://console.cloud.tencent.com/scf/list)**를 선택하고 해당하는 함수 이름을 클릭하면 해당 함수의 상세 페이지로 이동합니다.
2. **트리거 관리**>**트리거 생성**을 클릭하면 트리거 생성 창이 팝업됩니다. 트리거 방식은 'MPS 트리거'를 선택합니다.
주요 매개변수 정보는 다음과 같습니다. 기타 설정 항목은 기본값을 유지하십시오.
  - **이벤트 유형**: MPS 트리거는 계정 차원의 이벤트 유형으로 Event를 전송합니다. 현재 워크플로 작업(WorkflowTask)과 비디오 편집 작업(EditMediaTask)의 두 가지 이벤트 유형 트리거를 지원합니다.
>?
>- 처음 MPS 트리거를 생성하면 관련 서비스 역할 상태가 오류로 표시됩니다. 안내에 따라 해당 서비스 **SCF_QcsRole**, **MPS_QcsRole**을 클릭하여 권한을 부여하십시오.
- MPS 트리거는 서비스 차원에서 발생하는 이벤트를 이벤트 소스로 하며 리전, 리소스 등의 속성을 구분하지 않습니다. 각 계정은 두 가지 이벤트만 단일 함수에 바인딩할 수 있으며, 다수의 함수를 동시에 처리해야 하는 작업은 [함수 간 호출](https://intl.cloud.tencent.com/document/product/583/32747)을 참고하십시오.
3. **제출**을 클릭하면 MPS 트리거 설정이 완료됩니다.


### 3단계: 함수 테스트 기능
1. **[MPS 콘솔](https://console.cloud.tencent.com/mps)**에서 MPS의 비디오 처리 워크플로를 실행합니다.
2. **[SCF 콘솔](https://console.cloud.tencent.com/scf/list?rid=8&ns=default)**로 전환하여 실행 결과를 확인합니다.
함수 상세 페이지에서 **로그 조회** 탭을 선택하면 아래 이미지와 같이 출력된 로그 정보를 확인할 수 있습니다.
3. [COS 콘솔](https://console.cloud.tencent.com/cos5)로 전환하여 데이터 덤프 및 가공 결과를 확인합니다.

>?필요에 따라 구체적인 데이터 가공 처리 방법을 작성할 수 있습니다.
