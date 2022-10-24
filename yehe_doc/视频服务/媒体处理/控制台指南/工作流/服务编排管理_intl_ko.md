## 작업 시나리오
지정된 COS(Cloud Object Storage) Bucket에 업로드된 비디오를 자동으로 처리하고 결과를 지정된 Bucket에 저장하도록 **스키마**를 구성할 수 있습니다. 오디오/비디오 트랜스 코딩 작업, 오디오/비디오 향상 작업, 워터마크 작업, 스크린샷 작업, 애니메이션 이미지 작업, 심사 작업, 콘텐츠 인식 작업 및 콘텐츠 분석 작업을 스키마에 포함시킬 수 있습니다.

## 스키마 생성
### 스키마 생성[](id:create)
1. [MPS(Media Processing Service) 콘솔](https://console.cloud.tencent.com/mps)에 로그인하고 왼쪽 사이드바에서 [**워크플로** > **스키마 관리** > **스키마 생성**](https://console.cloud.tencent.com/mps/workflows/pipeline/add)을 클릭하여 스키마 생성 페이지로 이동합니다.
2. **서비스 스키마 생성** 페이지에서 실제 필요에 따라 설정을 완료합니다.
<table>
    <tr>
        <th width=15%>구성 항목<a id="workflow"></a></th>
        <th>필수</th>
        <th>설명</th>
    </tr>
    <tr>
        <td>스키마 이름</td>
        <td>Yes</td>
        <td>128자 이내의 중국어, 영어, 숫자, 언더바 및 하이픈<code>(_-)</code>을 조합하여 입력할 수 있습니다. 예: ‘MPS’.</td>
    </tr>
    <tr>
        <td>트리거 Bucket</td>
        <td>Yes</td>
        <td>현재 APPID로 생성된 Bucket을 선택합니다. 스키마가 활성화되면 이 Bucket에 업로드된 동영상이 자동으로 처리됩니다.</td>
    </tr>
    <tr>
        <td>트리거 디렉터리</td>
        <td>No</td>
        <td>슬래시<code>(/)</code>로 끝나는 문자열. 비워두면 선택한 트리거 Bucket 아래의 모든 디렉터리에 스키마가 적용됩니다.</td>
    </tr>
    <tr>
        <td>출력 Bucket</td>
        <td>Yes</td>
        <td>기본적으로 출력 Bucket은 트리거 Bucket과 동일합니다. 현재 APPID에서 동일한 리전의 Bucket을 선택할 수도 있습니다. 스키마가 완료된 후 처리된 비디오는 이 Bucket에 저장됩니다.</td>
    </tr>
    <tr>
        <td>출력 디렉터리</td>
        <td>No</td>
        <td>슬래시<code>(/)</code>로 끝나는 문자열. 비어 있는 경우 출력 디렉터리는 트리거 디렉터리와 동일합니다.</td>
    </tr>
</table>

3. **생성**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f10a7ed82865537c7d024e6537f1b083.png)

### 이벤트 알림 구성
이벤트 알림은 스키마의 진행 상황과 상태를 계속 업데이트합니다. MPS는 TDMQ-CMQ 콜백, HTTP 콜백 및 SCF 콜백의 세 가지 알림 유형을 지원합니다.
<table>
<tr>
<th>콜백 유형<a id="recall"></a></th>
<th>구성</th>
</tr>
<tr>
<td>TDMQ-CMQ 콜백</td>
<td><ol style="margin:0">
<li>TDMQ-CMQ 콜백을 활성화하려면 <a href="https://console.cloud.tencent.com/tdmq/cmq-queue?rid=1">Tencent Distributed Message Queue(TDMQ)</a>를 활성화하고 모델을 생성해야 합니다. MPS의 이벤트 알림은 지정한 메시지 큐로 전송됩니다.</br>
<li>스키마 생성 페이지에서 다음과 같이 콜백 설정을 완료합니다: <ul style="margin:0">
			<li>TDMQ-CMQ 모델: 큐 모델을 선택합니다.</li>
			<li>TDMQ-CMQ 리전: 광저우, 상하이, 베이징, 상하이 금융, 선전 금융, 중국홍콩, 청두, 북미 또는 미국 서부를 선택합니다.</li>
			<li>큐 이름: 사용자 지정 이름을 입력합니다.</li>
</ul></ul></td>
</tr>
<tr>
<td>HTTP 콜백
</td>
<td>알림 구성 API <a href="https://intl.cloud.tencent.com/document/product/1041/33690#TaskNotifyConfig">TaskNotifyConfig</a>를 호출할 때, NotifyType을 URL로, NotifyUrl을 HTTP 콜백 주소로 설정합니다.</td>
</tr>
<tr>
<td>SCF 콜백</td>
<td><ol style="margin:0">
	<li>SCF(Serverless Cloud Function)를 사용하면 MPS에서 생성된 이벤트 알림을 빠르게 처리할 수 있습니다. 아래 그림은 데이터 흐름을 보여줍니다.</br>
	<img src="https://main.qcloudimg.com/raw/02656fefa8e2f61f71252727747b7a02.png" /></li>
	<li>이벤트 알림은 MPS 트리거에 의해 SCF로 푸시되고 serverless 기능에 의해 처리됩니다.</li>
	<li>‘SCF 콘솔로 이동’을 클릭하여 SCF 콘솔에서 기능을 구성할 수 있습니다. 자세한 지침은 <a href="https://intl.cloud.tencent.com/document/product/1041/40337">MPS 작업 콜백 알림</a>을 참고하십시오. 참고: <ul style="margin:0">
	<li>SCF 콜백 구성은 모든 스키마에 적용되며 현재 스키마에 저장되지 않습니다.</li>
	<li>SCF로 데이터를 전송하면 수수료가 발생합니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/583/17299"> 과금 개요</a>를 참고하십시오.</li>
</ul></ul></td>
</tr>
</table>


### 작업 구성
MPS는 스키마에 대한 작업을 구성할 수 있는 시각적 툴을 제공합니다.
1. **+**를 클릭하고 추가할 작업 유형을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ddf9374ff8d1acf88c100830b7401e8b.png)
2. 선택한 유형의 작업이 워크플로에 추가됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8b65909d7defe9860bea78b84d97ec2d.png)
3. **편집** 아이콘을 클릭합니다. 팝업 창에서 작업의 세부 사항과 출력 정보를 지정합니다. 여기서 출력 정보를 지정하지 않으면 스키마에 대해 지정된 출력 정보가 사용됩니다.
>! 작업 구성 페이지는 작업 유형에 따라 다릅니다. 아래 그림은 ‘오디오/비디오 트랜스 코딩’ 작업에 대한 구성 페이지를 보여줍니다.

![](https://qcloudimg.tencent-cloud.cn/raw/f36828df241814cd2a529991325c7b8a.png)

## 스키마 관리
1. [**MPS 콘솔**](https://console.cloud.tencent.com/mps)에 로그인한 후 왼쪽 사이드바에서 [**워크플로** > **스키마 관리**](https://console.cloud.tencent.com/mps/workflows/pipeline)를 선택합니다. **스키마 관리** 페이지에서 스키마 **활성화**, **비활성화**, **편집**, **삭제** 및 **세부 정보 보기**를 수행할 수 있습니다.
2. 스키마 리스트에는 스키마 이름, 트리거 Bucket, 리전, 트리거 디렉터리, 생성 시간, 스키마 상태를 포함한 정보가 표시됩니다. 생성 시간을 기준으로 스키마를 정렬하고, 이름으로 스키마를 검색하고, 스키마의 세부 정보를 편집, 삭제 또는 볼 수 있습니다.
   -  **스키마 활성화**
      - 스키마는 기본적으로 비활성화되어 있습니다. **활성화** 열에서 스위치를 켜서 스키마를 활성화할 수 있습니다.
      - 스키마가 활성화되면 트리거 Bucket에 업로드된 동영상에 대해 자동으로 실행됩니다.
   -  **스키마 비활성화**
      - **활성화** 열에서 스위치를 해제하여 스키마를 비활성화할 수 있습니다.
      - 스키마가 비활성화되면 트리거 Bucket에 업로드된 비디오에서 더 이상 자동으로 실행되지 않습니다.
   -  **스키마 편집**
      - 작업 열에서 **편집**을 클릭하여 스키마 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 이벤트 알림 설정 또는 작업을 수정합니다.
      - 활성화된 스키마는 편집하거나 삭제할 수 없습니다.
   -  **스키마 삭제**
      - 작업 열에서 **삭제**를 클릭하여 스키마를 삭제합니다.
      - 스키마가 삭제된 후에는 트리거 Bucket에 업로드된 비디오에서 더 이상 자동으로 실행되지 않습니다.
      - 활성화된 스키마는 편집하거나 삭제할 수 없습니다.