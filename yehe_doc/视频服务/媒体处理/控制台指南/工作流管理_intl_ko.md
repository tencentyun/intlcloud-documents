## 작업 시나리오
워크플로 설정 후, 지정 Bucket과 디렉터리에 업로드된 비디오가 자동으로 MPS를 트리거하며, 출력 파일은 지정 Bucket과 디렉터리에 입력됩니다.워크플로에서 트랜스 코딩 작업, 화면 캡처 작업, gif 변환 작업, 심사 작업, 콘텐츠 식별 작업, 콘텐츠 분석 작업 및 워터마크 추가 작업 등을 설정할 수 있습니다.



## 워크플로 생성 순서
1. [MPS 콘솔](https://console.cloud.tencent.com/mps)에 로그인한 후, 왼쪽 메뉴에서 [워크플로 관리]를 클릭해 '워크플로 관리' 페이지로 이동합니다.
2. [워크플로 생성]을 클릭하여 워크플로 생성 페이지로 이동합니다. 워크플로 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 설정 항목 및 이벤트 알림을 설정해야 합니다. 구체적인 설정 방법은 [워크플로 설정 설명](#workflow)을 참고하십시오.
![](https://main.qcloudimg.com/raw/314b57f24a325fc3f4a3f4da16594006.png)
워크플로 생성 페이지에서 설정해야 하는 정보는 다음과 같습니다.
<table>
<tr><th>설정 항목<a id="workflow"></a></th><th>필수 작성 여부</th><th>설정 설명</th></tr>
<tr>
<td>워크플로</td>
<td>네</td>
<td>128자 이내의 중국어, 영어, 숫자, 언더바 및 붙임표<code>（_-）</code>를 조합하여 입력할 수 있습니다. 예: ‘MPS’.</td>
</tr><tr>
<td>트리거 Bucket</td>
<td>네</td>
<td>이 APPID에서 생성한 Bucket 중 하나를 트리거 Bucket으로 설정할 수 있습니다.워크플로 활성화 후 이 Bucket에 비디오 파일을 업로드하면 자동으로 워크플로 실행을 트리거할 수 있습니다.</td>
</tr><tr>
<td>트리거 디렉터리</td>
<td>아니요</td>
<td>마지막에 슬래시<code>（/）</code>를 입력합니다. 입력하지 않을 경우 트리거 Bucket의 모든 디렉터리에 적용됩니다.</td>
</tr><tr>
<td>출력 Bucket</td>
<td>네</td>
<td>기본값은 트리거 Bucket과 동일합니다. 이 APPID에서 트리거 Bucket과 같은 리전의 Bucket 중 하나를 출력 Bucket으로 설정할 수 있습니다. 워크플로 프로세스 완료 후 새로 생성된 비디오 파일은 해당 Bucket에 저장됩니다.</td>
</tr><tr>
<td>출력 디렉터리</td>
<td>아니요</td>
<td>마지막에 슬래시<code>（/）</code>를 입력합니다. 입력하지 않을 경우 출력 디렉터리와 트리거 디렉터리는 동일하게 유지됩니다.</td>
</tr><tr>
<td>이벤트 알림 활성화</td>
<td>아니요</td>
<td><ul style="margin:0"><li>기본 설정: 비활성화.이벤트 알림이 활성화된 경우, 구체적인 설정 방법은 <a href="#recall"> 콜백 메소드 유형 설정</a>을 참고하십시오.</li><li>CMQ 이벤트 알림을 활성화해야 할 경우, <a href="https://console.cloud.tencent.com/cmq">CMQ</a>로 이동하여 서비스를 활성화하고 템플릿을 생성하십시오.이벤트 알림 활성화 후, 지정된 CMQ는 MPS 이벤트 알림을 수신합니다.</li></ul></td>
</tr><tr>
<td>설정 항목</td>
<td>네</td>
<td>트랜스 코딩 작업, 화면 캡처 작업, gif 변환 작업, 심사 작업, 콘텐츠 식별 작업, 콘텐츠 분석 작업에서 최소 한 항목을 선택해 설정합니다. 자세한 내용은<a href="#p1">작업 설정 설명</a>을 참고하십시오.</td>
</tr></table>
<table>
<tr><th>콜백 방식 유형<a id="recall"></a></th><th>설정 설명</th></tr>
<tr>
<td>CMQ 콜백</td>
<td><ul style="margin:0"><li>CMQ 모델:큐 모델 선택 기본 설정. </li><li>CMQ 단지:광저우, 상하이, 베이징, 상하이 금융, 선전 금융, 중국 홍콩, 청두, 북미 리전 또는 미국 서부를 선택할 수 있습니다.</li><li>큐 이름:사용자 정의.</li></ul></td>
</tr><tr>
<td>SCF 콜백</td>
<td>[SCF 작업으로 이동]을 클릭하여 설정 작업을 진행할 수 있습니다. 구체적인 설정 방법은 <a href="https://intl.cloud.tencent.com/document/product/1041/40337">비디오 작업 콜백 알림</a>을 참고하십시오. <br>SCF 콜백 설정은 모든 워크플로를 대상으로 하며, 현재의 워크플로는 해당 설정 상태를 저장하지 않습니다.</td>
</tr></table>

## 이벤트 알림
### 1. CMQ를 통한 이벤트 알림
- 이벤트 알림(기본값은 비활성화)을 활성화하면, 사용자는 CMQ 모델 중 큐 모델 또는 주제 모델을 선택하고 선택 모델의 이름과 리전을 입력할 수 있습니다.설정을 완료하면 지정한 CMQ에서 MPS의 이벤트 알림을 수신하게 됩니다.

- CMQ 이벤트 알림은 사용자가 CMQ 서비스를 활성화하고 큐 모델 또는 주제 모델을 생성한 후 사용할 수 있습니다. 자세한 내용은 [CMQ](https://intl.cloud.tencent.com/document/product/406/8435)를 참고하십시오.

### 2. ### 2. SCF를 통한 이벤트 알림
함수 처리 서비스를 통해 MPS의 콜백 이벤트에 대한 처리 및 작업을 신속하게 완료할 수 있습니다. 데이터 처리의 전체 흐름도는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/02656fefa8e2f61f71252727747b7a02.png)
MPS 트리거를 통해 이벤트를 SCF 함수에 전송하고, 서비스 아키텍처가 없는 serverless 함수 계산을 통해 콜백 이벤트의 처리 및 응답을 제공합니다.

#### 함수 처리 시나리오 사례
CLS는 MPS 로그 트리거를 통해 로그 테마의 데이터를 SCF로 전송하여 처리함으로써 비디오의 이벤트 알림, 상태 모니터링, 알람 처리 등 응용 시나리오에 대한 기능을 충족시킬 수 있습니다.

| 함수 처리 시나리오 | 설명 |
|---------|---------|
| 비디오 작업 콜백 COS 백업 | SCF를 통해 MPS의 콜백 작업을 즉시 COS에 백업합니다. |
| 비디오 작업 콜백 알림 | 실시간으로 수신한 MPS 데이터 메시지를 이메일 등에 푸시합니다. |

>!데이터를 SCF에 전송할 때 컴퓨팅 요금이 발생합니다. 자세한 내용은 [SCF 과금 개요](https://intl.cloud.tencent.com/document/product/583/17299)를 참고하십시오.


[](id:p1)**작업 설정 설명**

작업 유형|사전 설정 또는 사용자 정의 템플릿 지원 여부|설정을 지원하는 템플릿
-|-|-
 트랜스 코딩 작업|트랜스 코딩 템플릿:<li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|<li>트랜스 코딩 템플릿:생성된 템플릿 목록에서 선택하십시오. 각 작업 설정은 한 개 이상의 트랜스 코딩 템플릿 추가를 지원합니다.기존 템플릿이 사용 요구 조건을 충족시키지 못하는 경우 [템플릿 설정 - 트랜스 코딩 템플릿](https://console.cloud.tencent.com/mps/templates?tab=video)에서 새 템플릿을 다시 생성할 수 있습니다.<br><li>워터마크 템플릿:각 트랜스 코딩 템플릿은 최대 4개의 워터마크를 추가할 수 있습니다.기존 워터마크가 사용 요구 조건을 충족하지 못하는 경우 [템플릿 설정 - 워터마크 템플릿](https://console.cloud.tencent.com/mps/templates?tab=watermark)에서 새 템플릿을 다시 생성할 수 있습니다.
 화면 캡처 작업|화면 캡처 템플릿:<li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|<li>화면 캡처 템플릿:시점 화면 캡처, 샘플링 화면 캡처, 스프라이트 이미지 화면 캡처의 화면 캡처 방법을 포함하며, 각 스크린샷 방법은 해당 방법에서 설정 완료된 템플릿만 선택할 수 있습니다. 시점 화면 캡처는 시점을 선택해야 합니다.기존 템플릿이 사용 요구 조건을 충족하지 못하는 경우 [템플릿 설정 - 화면 캡처 템플릿](https://console.cloud.tencent.com/mps/templates?tab=snapshot)에서 새 템플릿을 다시 생성할 수 있습니다.<br><li>워터마크 템플릿:각 트랜스 코딩 템플릿은 최대 4개의 워터마크를 추가할 수 있습니다.기존 워터마크가 사용 요구 조건을 충족하지 못하는 경우 [템플릿 설정 - 워터마크 템플릿](https://console.cloud.tencent.com/mps/templates? tab=watermark)에서 새 템플릿을 다시 생성할 수 있습니다.
gif 작업|gif 템플릿<li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|gif 템플릿:여러 gif 템플릿 추가 및 gif 시간대 재설정을 지원합니다.기존 템플릿이 사용 요구 조건을 충족하지 못하는 경우 [템플릿 설정 - gif 템플릿](https://console.cloud.tencent.com/mps/templates?tab=gif)에서 새 템플릿을 다시 생성할 수 있습니다.
심사 작업|심사 템플릿:<li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|심사 템플릿:1개의 심사 템플릿 추가만 지원됩니다.기존 템플릿이 사용 요구 조건을 충족하지 못하는 경우 [템플릿 설정 - 심사 템플릿](https://console.cloud.tencent.com/mps/templates?tab=audit)에서 새 템플릿을 다시 생성할 수 있습니다.
컨텐츠 식별 작업|컨텐츠 식별 템플릿:<li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|컨텐츠 식별 템플릿:1개의 콘텐츠 식별 템플릿 추가만 지원됩니다.기존 템플릿이 사용 요구 조건을 충족하지 못하는 경우 [템플릿 설정 - 컨텐츠 식별 템플릿](https://console.cloud.tencent.com/mps/templates?tab=recognization)에서 새 템플릿을 다시 생성할 수 있습니다.
컨텐츠 분석 작업|컨텐츠 분석 템플릿:<li>사전 설정 템플릿 지원<br><li>사용자 정의 템플릿 지원|컨텐츠 분석 템플릿:1개의 콘텐츠 분석 템플릿 추가만 지원됩니다.기존 템플릿이 사용 요구 조건을 충족하지 못하는 경우 [템플릿 설정 - 컨텐츠 분석 템플릿](https://console.cloud.tencent.com/mps/templates?tab=analysis)에서 새 템플릿을 다시 생성할 수 있습니다.



## 워크플로 관리 순서

1. [MPS 콘솔](https://console.cloud.tencent.com/mps)에 로그인한 후, 왼쪽 메뉴에서 [워크플로 관리]를 클릭해 '워크플로 관리' 인터페이스로 이동합니다.
2. 워크플로 리스트에는 워크플로 이름, 트리거 Bucket, 리전, 디렉터리, 생성 시간 및 활성화 상태 등의 정보가 표시됩니다.생성 시간에 따른 정렬, 워크플로 이름 검색, 지정 워크플로 상세 보기/편집/삭제 작업을 지원합니다.
	-  **워크플로 활성화**
		- 워크플로는 기본적으로 비활성화 상태입니다. 워크플로에 해당하는 상태 버튼을 클릭하면 워크플로를 활성화할 수 있습니다.
		- 워크플로를 활성화해야 트리거 Bucket에 업로드한 비디오 파일이 자동으로 실행됩니다.
	- **워크플로 사용 중지**
		- 해당 워크플로에 상응하는 상태 버튼을 클릭하면 워크플로 사용을 중지할 수 있습니다.
		- 워크플로 사용을 중지하면 트리거 Bucket에 업로드한 비디오 파일은 MPS 작업을 실행하지 않습니다.
	- **워크플로 편집**
		- 타깃 워크플로 작업 열의 [편집]을 클릭해 '워크플로 편집' 페이지로 이동합니다. 해당 페이지에서는 워크플로의 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 이벤트 알림과 같은 설정 항목을 수정할 수 있습니다.
		- 워크플로가 활성화 상태인 경우 편집 및 삭제 작업을 할 수 없습니다.
	- **워크플로 삭제**
		- 타깃 워크플로 작업 열의 [삭제]를 클릭해 해당 워크플로를 삭제할 수 있습니다.
		- 워크플로를 삭제하면 트리거 Bucket에 업로드한 비디오 파일은 MPS 작업을 실행하지 않습니다.
		- 워크플로가 활성화 상태인 경우 편집 및 삭제 작업을 할 수 없습니다.

