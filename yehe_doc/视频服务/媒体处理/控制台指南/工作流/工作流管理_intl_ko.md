>!MPS(Media Processing Service) 콘솔의 ‘워크플로 관리’ 섹션은 더 쉽고 유연한 설정을 제공하는 ‘스키마 관리’로 대체되었습니다. 스키마를 구성하려면 스키마 관리로 이동합니다.


## 작업 시나리오
워크플로를 설정한 후 지정된 Bucket 및 디렉터리에 업로드된 미디어 파일은 자동으로 처리되고 결과는 지정된 Bucket 및 디렉터리에 업로드됩니다. 워크플로에는 트랜스 코딩, 스크린샷 찍기, 애니메이션 스크린샷 생성, 심사, 콘텐츠 인식, 콘텐츠 분석 및 워터마크와 같은 작업이 포함될 수 있습니다.

## 워크플로 생성[](id:create)
1. [MPS 콘솔](https://console.cloud.tencent.com/mps)에 로그인하고 왼쪽 사이드바에서 **워크플로 관리**를 선택합니다.
2. **워크플로 생성**을 클릭하여 워크플로 생성 페이지로 이동하고, 워크플로 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 이벤트 알림 및 작업을 설정합니다. 자세한 지침은 [워크플로 구성](#workflow)을 참고하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/e46b738c267c5b34715abd01cc577b2d.png)

워크플로 생성 페이지에서 설정해야 하는 정보는 다음과 같습니다.
<table>
<tr><th width=15%>항목<a id="workflow"></a></th><th>필수</th><th>설명</th></tr>
<tr>
<td>워크플로 이름</td>
<td>Yes</td>
<td>128자 이내의 중국어, 영어, 숫자, 언더바 및 하이픈<code>(_-)</code>을 지원합니다. 예: ‘MPS’.</td>
</tr><tr>
<td>트리거 Bucket</td>
<td>Yes</td>
<td>현재 APPID로 생성된 Bucket을 선택합니다. 워크플로가 활성화되면 이 Bucket에 업로드된 동영상이 자동으로 처리됩니다.</td>
</tr><tr>
<td>트리거 디렉터리</td>
<td>No</td>
<td>슬래시<code>(/)</code>로 끝나는 문자열. 비워 두면 선택한 트리거 Bucket 아래의 모든 디렉터리에 워크플로가 적용됩니다.</td>
</tr><tr>
<td>출력 Bucket</td>
<td>Yes</td>
<td>기본적으로 출력 Bucket은 트리거 Bucket과 동일합니다. 동일한 APPID에서 동일한 리전의 Bucket을 선택할 수도 있습니다. 워크플로가 실행된 후 처리된 비디오는 이 Bucket에 저장됩니다.</td>
</tr><tr>
<td>출력 디렉터리</td>
<td>No</td>
<td>슬래시<code>(/)</code>로 끝나는 문자열. 비어 있는 경우 출력 디렉터리는 트리거 디렉터리와 동일합니다.</td>
</tr><tr>
<td>이벤트 알림 활성화</td>
<td>No</td>
<td>
<ul style="margin:0"><li>기본적으로 비활성화되어 있습니다. 이벤트 알림을 구성하는 방법에 대한 자세한 지침은 아래 <a href="#recall">콜백 구성</a>을 참고하십시오. </li><li>TDMQ-CMQ 이벤트 알림을 활성화하려면 <a href="https://console.cloud.tencent.com/tdmq/cmq-queue?rid=1">Tencent Distributed Message Queue(TDMQ)</a>를 활성화하고 모델을 생성해야 합니다. TDMQ-CMQ 이벤트 알림이 활성화된 후 지정된 메시지 큐는 동영상 처리 이벤트에 대한 알림을 받습니다.</li></ul></td>
</tr><tr>
<td>설정 항목</td>
<td>Yes</td>
<td>트랜스 코딩, 스크린샷 촬영, 애니메이션 이미지 생성, 심사, 콘텐츠 인식 및 콘텐츠 분석에서 구성할 작업을 하나 이상 선택합니다. 자세한 내용은 <a href="#p1">작업 구성</a>을 참고하십시오.</td>
</tr></table>
<table>
<tr><th>콜백 방식 유형<a id="recall"></a></th><th>설정 설명</th></tr>
<tr>
<td>TDMQ-CMQ 콜백</td>
<td>
<ul style="margin:0">
<li>TDMQ-CMQ 모델: 큐 모델 또는 주제 모델을 선택합니다.</li>
<li>TDMQ-CMQ 리전: 광저우, 상하이, 베이징, 상하이 금융, 선전 금융, 중국홍콩, 청두, 북미 또는 미국 서부를 선택합니다.</li>
<li>큐 이름/주제 이름: 사용자 지정 이름을 입력합니다.</li>
</ul>
</td>
</tr>
<tr>
<td>HTTP 콜백</td>
<td>알림 구성 API <a href="https://intl.cloud.tencent.com/document/product/1041/33690#TaskNotifyConfig">TaskNotifyConfig</a>를 호출할 때, NotifyType을 URL로, NotifyUrl을 HTTP 콜백 주소로 설정합니다.
</td>
</tr>
<tr>
<td>SCF(Serverless Cloud Function) 콜백</td>
<td><a href="https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default&keyword=mps">SCF 콘솔로 이동</a>을 클릭하여 SCF 콘솔에서 기능을 구성할 수 있습니다. 자세한 지침은 <a href="https://intl.cloud.tencent.com/document/product/1041/40337">MPS 작업 콜백 알림</a>을 참고하십시오. <br>SCF 콜백 구성은 모든 워크플로에 적용되며 현재 워크플로에 대해 특별히 저장되지 않습니다.</td>
</tr>
</table>


## 이벤트 알림[](id:event)
### CMQ를 통해 이벤트 알림 수신
- 이벤트 알림은 기본적으로 비활성화되어 있습니다. CMQ를 통해 알림을 받으려면 이벤트 알림 활성화 옆에 있는 토글을 클릭하고 CMQ 모델에 대한 큐 또는 주제 모델을 선택하고 모델 이름과 리전을 설정합니다. MPS 이벤트 알림은 지정된 큐 또는 주제로 전송됩니다.
- CMQ 이벤트 알림은 사용자가 CMQ 서비스를 활성화하고 큐 모델 또는 주제 모델을 생성한 후 사용할 수 있습니다. 자세한 내용은 [CMQ](https://intl.cloud.tencent.com/document/product/406/8435)를 참고하십시오.

### SCF를 통해 이벤트 알림 수신
SCF를 사용하면 MPS에서 생성된 이벤트 알림을 빠르게 처리할 수 있습니다. 아래 그림은 데이터 흐름을 보여줍니다.
<img src="https://main.qcloudimg.com/raw/02656fefa8e2f61f71252727747b7a02.png" style="zoom: 67%;" />
이벤트는 MPS 트리거에 의해 SCF로 푸시되고 serverless 기능에 의해 처리됩니다.

#### 함수 처리 시나리오 사례
CLS는 MPS 로그 트리거를 통해 로그 테마의 데이터를 SCF로 전송하여 처리함으로써 비디오의 이벤트 알림, 상태 모니터링, 알람 처리 등 응용 시나리오에 대한 기능을 충족시킬 수 있습니다.

| 함수 처리 시나리오         | 설명                                                |
| -------------------- | ------------------------------------------------------- |
| COS에 비디오 작업 백업 | MPS의 콜백 작업을 SCF를 통해 COS에 적시에 백업.          |
| 비디오 작업 콜백 알림     | MPS 데이터 메시지를 실시간으로 수신하고 WeCom 또는 이메일을 통해 사용자에게 메시지를 보냅니다. |

>!데이터를 SCF에 전송할 때 컴퓨팅 요금이 발생합니다. 자세한 내용은 [SCF 과금 개요](https://intl.cloud.tencent.com/document/product/583/17299)를 참고하십시오.

## 워크플로 관리[](id:manage)
1. [MPS 콘솔](https://console.cloud.tencent.com/mps)에 로그인하고, 왼쪽 사이드바에서 **워크플로 관리**를 선택합니다.
2. 워크플로 리스트에는 워크플로 이름, 트리거 Bucket, 리전, 디렉터리, 생성 시간, 활성화 상태 등의 정보가 표시됩니다. 생성 시간에 따른 정렬, 작업 플로 이름 검색, 지정 워크플로 상세 보기/편집/삭제 작업을 지원합니다.
	-  **워크플로 활성화**
		- 워크플로는 기본적으로 비활성화 상태입니다. 워크플로에 해당하는 상태 버튼을 클릭하면 워크플로를 활성화할 수 있습니다.
		- 워크플로를 활성화해야 트리거 Bucket에 업로드한 비디오 파일이 자동으로 실행됩니다.
	- **워크플로 사용 중지**
		- 해당 워크플로에 상응하는 상태 버튼을 클릭하면 워크플로 사용을 중지할 수 있습니다.
		- 워크플로 사용을 중지하면 트리거 Bucket에 업로드한 미디어 파일은 MPS 작업을 실행하지 않습니다.
	- **워크플로 편집**
		- 타깃 워크플로 작업 열의 **편집**을 클릭해 ‘워크플로 편집’ 페이지로 이동합니다. 해당 페이지에서는 워크플로의 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 이벤트 알림과 같은 설정 항목을 수정할 수 있습니다.
		- 워크플로가 활성화 상태인 경우 편집 및 삭제 작업을 할 수 없습니다.
	- **워크플로 삭제**
		- 타깃 워크플로 작업 열의 **삭제**를 클릭해 해당 워크플로를 삭제할 수 있습니다.
		- 워크플로를 삭제하면 트리거 Bucket에 업로드한 미디어 파일은 MPS 작업을 실행하지 않습니다.
		- 워크플로가 활성화 상태인 경우 편집 및 삭제 작업을 할 수 없습니다.
