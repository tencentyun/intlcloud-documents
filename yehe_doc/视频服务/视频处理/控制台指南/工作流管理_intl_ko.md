## 작업 시나리오
워크플로를 설정하면 지정 Bucket과 디렉터리에 업로드된 비디오가 자동으로 비디오 처리를 트리거하며, 출력 파일은 지정 Bucket과 디렉터리에 입력됩니다. 워크플로에서 트랜스 코딩, 화면 캡처, gif, 심사, 콘텐츠 인식, 콘텐츠 분석, 워터마크 추가 등의 작업을 설정할 수 있습니다.



## 워크플로 생성 순서
1. [비디오 처리 콘솔](https://console.cloud.tencent.com/mps)에 로그인한 후, 왼쪽 메뉴에서 [워크플로 관리]를 클릭해 '워크플로 관리' 인터페이스로 이동합니다.
2. [워크플로 생성]을 클릭해 '워크플로 생성' 페이지로 이동합니다. 워크플로 생성 시 워크플로의 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 이벤트 공지와 같은 항목을 설정해야 합니다.
![](https://main.qcloudimg.com/raw/314b57f24a325fc3f4a3f4da16594006.png))
	- **워크플로 이름**
	필수 입력 항목입니다. 중국어, 영어, 숫자, 언더바(\_), 붙임표(-)만 지원되며 128자를 초과할 수 없고, 작업 플로의 이름은 중복될 수 없습니다.
	- **트리거 Bucket**
		- 필수 항목입니다. 해당 APPID에서 생성한 Bucket 중 하나를 트리거 Bucket으로 설정할 수 있습니다.
		- 워크플로를 활성화한 후 해당 Bucket에 비디오 파일을 업로드하면 자동으로 워크플로 실행이 트리거됩니다.
	- **트리거 디렉터리**
	옵션 항목입니다. 마지막에 슬래시(/)를 입력합니다. 입력하지 않을 경우 트리거 Bucket의 모든 디렉터리에 적용됩니다.
	- **출력 Bucket**
		- 필수 항목입니다. 기본값은 트리거 Bucket과 동일합니다. 해당 APPID에서 트리거 Bucket과 같은 리전의 Bucket 중 하나를 출력 Bucket으로 설정할 수 있습니다.
		- 워크플로 프로세스 완료 후 새로 생성된 비디오 파일은 해당 Bucket에 저장됩니다.
	- **출력 디렉터리**
	옵션 항목입니다. 마지막에 슬래시(/)를 입력합니다. 입력하지 않을 경우 출력 디렉터리와 트리거 디렉터리는 동일하게 유지됩니다.
	- **설정 항목**
	트랜스 코딩, 화면 캡처, gif, 심사, 콘텐츠 인식, 콘텐츠 분석 작업 중 최소 한 항목을 선택해 설정합니다. 자세한 내용은 [작업 설정 설명](#p1)을 참조하십시오.

## 이벤트 공지
### 1. CMQ를 통한 이벤트 공지
- 이벤트 공지(기본값은 비활성화)를 활성화하면, 사용자는 CMQ 모델 중 큐 모델 또는 주제 모델을 선택하고 선택 모델의 이름과 리전을 입력할 수 있습니다. 설정을 완료하면 지정한 CMQ에서 비디오 처리의 이벤트 공지를 수신하게 됩니다.

- CMQ 이벤트 공지는 사용자가 CMQ 서비스를 활성화하고 큐 모델 또는 주제 모델을 생성한 후 사용할 수 있습니다. 자세한 내용은 [CMQ](https://intl.cloud.tencent.com/document/product/406/8435)를 참조하십시오.

### 2. SCF를 통한 이벤트 공지
함수 처리 서비스를 통해 MPS의 콜백 이벤트에 대한 처리 및 작업을 신속하게 완료할 수 있습니다. 데이터 처리의 전체 흐름도는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/af522de2310535d55ea2d76dc4239696.png)
MPS 트리거를 통해 이벤트를 SCF 함수에 전송하고, 서비스 아키텍처가 없는 serverless 함수 계산을 통해 콜백 이벤트의 처리 및 응답을 제공합니다.

#### 함수 처리 시나리오 사례
CLS는 MPS 로그 트리거를 통해 로그 테마의 데이터를 SCF로 전송하여 처리함으로써 비디오의 이벤트 공지, 상태 모니터링, 알람 처리 등 응용 시나리오에 대한 기능을 제공합니다.

| 함수 처리 시나리오 | 설명 |
|---------|---------|
| 비디오 작업 콜백 COS 백업 | SCF를 통해 MPS의 콜백 작업을 즉시 COS에 백업합니다. |
| 비디오 작업 콜백 공지	 | 실시간으로 수신한 MPS 데이터 메시지를 WeChat Work, 이메일 등에 전송합니다. |

>!데이터를 SCF에 전송할 때 컴퓨팅 요금이 발생합니다. 자세한 내용은 [SCF 과금 개요](https://intl.cloud.tencent.com/document/product/583/17299)를 참조하십시오.


[](id:p1)**작업 설정 설명**

작업 유형|사전 설정 또는 사용자 정의 템플릿 지원 여부|설정을 지원하는 템플릿
-|-|-
 트랜스 코딩|트랜스 코딩 템플릿: <li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|<li>트랜스 코딩 템플릿: 생성된 템플릿 리스트에서 선택합니다. 모든 작업 설정에서 하나 이상의 트랜스 코딩 템플릿 추가를 지원합니다. 사용 목적에 맞지 않는 템플릿이 있는 경우 [템플릿 설정 - 트랜스 코딩 템플릿](https://console.cloud.tencent.com/mps/templates?tab=video)에서 새로운 템플릿을 생성할 수 있습니다. <br><li>워터마크 템플릿: 모든 트랜스 코딩 템플릿은 최대 4개의 워터마크 추가를 지원합니다. 사용 목적에 맞지 않는 워터마크가 있는 경우 [템플릿 설정 - 워터마크 템플릿](https://console.cloud.tencent.com/mps/templates?tab=watermark)에서 새로운 템플릿을 생성할 수 있습니다.
 화면 캡처|화면 캡처 템플릿: <li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|<li>화면 캡처: 시점 화면 캡처, 샘플링 화면 캡처, 스프라이트 이미지 화면 캡처를 비롯한 모든 화면 캡처 방식은 해당 방식에 설정된 템플릿만 선택할 수 있으며, 시점 화면 캡처는 시점을 선택해야 합니다. 사용 목적에 맞지 않는 템플릿이 있는 경우 [템플릿 설정 - 화면 캡처 템플릿](https://console.cloud.tencent.com/mps/templates?tab=snapshot)에서 새로운 템플릿을 생성할 수 있습니다. <br><li>워터마크 템플릿: 모든 트랜스 코딩 템플릿은 최대 4개의 워터마크 추가를 지원합니다. 사용 목적에 맞지 않는 워터마크가 있는 경우 [템플릿 설정 - 워터마크 템플릿](https://console.cloud.tencent.com/mps/templates?tab=watermark)에서 새로운 템플릿을 생성할 수 있습니다.
gif|gif 템플릿: <li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|gif 템플릿: 여러 개의 gif 템플릿 추가 및 gif 시간대 재설정을 지원합니다. 사용 목적에 맞지 않는 템플릿이 있는 경우 [템플릿 설정 - gif 템플릿](https://console.cloud.tencent.com/mps/templates?tab=gif)에서 새로운 템플릿을 생성할 수 있습니다.
심사|심사 템플릿: <li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|심사 템플릿: 하나의 심사 템플릿 추가만 지원합니다. 사용 목적에 맞지 않는 템플릿이 있는 경우 [템플릿 설정 - 심사 템플릿](https://console.cloud.tencent.com/mps/templates?tab=audit)에서 새로운 템플릿을 생성할 수 있습니다.
콘텐츠 인식|콘텐츠 인식 템플릿: <li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|콘텐츠 인식 템플릿: 하나의 콘텐츠 인식 템플릿 추가만 지원합니다. 사용 목적에 맞지 않는 템플릿이 있는 경우 [템플릿 설정 - 콘텐츠 인식 템플릿](https://console.cloud.tencent.com/mps/templates?tab=recognization)에서 새로운 템플릿을 생성할 수 있습니다.
콘텐츠 분석|콘텐츠 분석 템플릿: <li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|콘텐츠 분석 템플릿: 하나의 콘텐츠 분석 템플릿 추가만 지원합니다. 사용 목적에 맞지 않는 템플릿이 있는 경우 [템플릿 설정 - 콘텐츠 분석 템플릿](https://console.cloud.tencent.com/mps/templates?tab=analysis)에서 새로운 템플릿을 생성할 수 있습니다.



## 워크플로 관리 순서

1. [비디오 처리 콘솔](https://console.cloud.tencent.com/mps)에 로그인한 후, 왼쪽 메뉴에서 [워크플로 관리]를 클릭해 '워크플로 관리' 인터페이스로 이동합니다.
2. 워크플로 리스트에는 워크플로 이름, 트리거 Bucket, 리전, 디렉터리, 생성 시간, 활성화 상태 등의 정보가 표시됩니다. 생성 시간에 따른 정렬, 작업 플로 이름 검색, 지정 워크플로 상세 보기/편집/삭제 작업을 지원합니다.
	-  **워크플로 활성화**
		- 워크플로는 기본적으로 비활성화 상태입니다. 워크플로에 해당하는 상태 버튼을 클릭하면 워크플로를 활성화할 수 있습니다.
		- 워크플로를 활성화해야 트리거 Bucket에 업로드한 비디오 파일이 자동으로 실행됩니다.
	- **워크플로 사용 중지**
		- 워크플로에 해당하는 상태 버튼을 클릭하면 워크플로 사용을 중지할 수 있습니다.
		- 워크플로 사용을 중지하면 트리거 Bucket에 업로드한 비디오 파일은 비디오 처리 작업을 실행하지 않습니다.
	- **워크플로 편집**
		- 타깃 워크플로 작업 열의 [편집]을 클릭해 '워크플로 편집' 페이지로 이동합니다. 해당 페이지에서는 워크플로의 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 이벤트 공지와 같은 설정 항목을 변경할 수 있습니다.
		- 워크플로가 활성화 상태인 경우 편집 및 삭제 작업을 할 수 없습니다.
	- **워크플로 삭제**
		- 타깃 워크플로 작업 열의 [삭제]를 클릭해 해당 워크플로를 삭제할 수 있습니다.
		- 워크플로를 삭제하면 트리거 Bucket에 업로드한 비디오 파일은 비디오 처리 작업을 실행하지 않습니다.
		- 워크플로가 활성화 상태인 경우 편집 및 삭제 작업을 할 수 없습니다.

