## 작업 시나리오
본 문서는 Media Processing Service(MPS)를 빠르게 이해하고 도입하는 데 도움을 줄 수 있습니다.MPS를 사용하는 주요 단계는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/aed6a4e4f8b3bb99187e0d899ac05338.png)

## 작업 순서
### 순서1:가입 및 로그인
1. [Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)을 통해 계정을 생성하고 실명 인증을 완료합니다.
2. Tencent Cloud 공식 홈페이지에 로그인한 후 [클라우드 서비스]>[비디오 서비스]>[[MPS]](https://console.cloud.tencent.com/mps)를 선택하여 비디오 처리 콘솔로 진입합니다.

### 순서2:권한 관리
MPS는 COS 버킷에 업로드된 파일에 다운로드, 트랜스 코딩, 업로드 등의 읽기 및 쓰기 작업을 수행해야 하므로, 서비스 역할을 생성하고 MPS에 COS 관련 작업 권한을 부여해야 합니다.

[MPS 콘솔](https://console.cloud.tencent.com/mps)로 이동한 후, 아직 권한 부여를 진행하지 않은 경우 [CAM으로 이동]을 클릭하여 콘솔의 통합 권한 관리 페이지로 이동, 권한 부여 작업을 진행합니다.
![]![](https://main.qcloudimg.com/raw/a3204a6470d3a9740a081849fc7324f3.png)

>!권한 부여가 완료되지 않은 경우, MPS 콘솔에서 다른 작업을 수행할 수 없습니다.



### 순서3:Bucket 생성
MPS는 COS에 업로드한 비디오 파일에 트랜스 코딩, 화면 캡처 등 처리를 진행하는 서비스이므로 COS 콘솔에서 버킷(Bucket)을 생성해야 합니다.

[COS 콘솔](https://console.cloud.tencent.com/cos5)의 버킷 관리 페이지로 이동 후 [버킷 생성] 버튼을 클릭하여 한 개의 Bucket을 생성하고, 해당 Bucket에 폴더를 생성하고 파일을 업로드합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참고하십시오.

 

### 순서4:워크플로 생성
워크플로는 생성된 템플릿을 통해 Bucket에 새로 업로드된 비디오 파일을 자동으로 처리합니다.워크플로에서 트랜스 코딩 작업, 화면 캡처 작업 및 gif작업 등을 설정할 수 있습니다.
1. [MPS 콘솔](https://console.cloud.tencent.com/mps)에 로그인한 후, [워크플로 관리]를 클릭해 '워크플로 관리' 페이지로 이동합니다.
2. [워크플로 생성]을 클릭하여 워크플로 생성 페이지로 이동합니다. 워크플로 이름, 트리거 Bucket, 트리거 디렉터리, 출력 Bucket, 출력 디렉터리, 구성 항목 및 이벤트 알림을 설정해야 합니다. 구체적인 구성 방법은 [워크플로 구성 설명](#workflow)을 참고하십시오.
![](https://main.qcloudimg.com/raw/a2b3e7b0e7e41b68221ea1d2b874b06e.png)
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
<td>아니오</td>
<td>마지막에 슬래시<code>（/）</code>를 입력합니다. 입력하지 않을 경우 트리거 Bucket의 모든 디렉터리에 적용됩니다.</td>
</tr><tr>
<td>출력 Bucket</td>
<td>네</td>
<td>기본값은 트리거 Bucket과 동일합니다. 이 APPID에서 트리거 Bucket과 같은 리전의 Bucket 중 하나를 출력 Bucket으로 설정할 수 있습니다. 워크플로 프로세스 완료 후 새로 생성된 비디오 파일은 해당 Bucket에 저장됩니다.</td>
</tr><tr>
<td>출력 디렉터리</td>
<td>아니오</td>
<td>마지막에 슬래시<code>（/）</code>를 입력합니다. 입력하지 않을 경우 출력 디렉터리와 트리거 디렉터리는 동일하게 유지됩니다.</td>
</tr><tr>
<td>이벤트 알림 활성화</td>
<td>아니오</td>
<td><ul style="margin:0"><li>기본 설정: 비활성화.이벤트 알림이 활성화된 경우, 구체적인 설정 방법은 <a href="#recall"> 콜백 방식 유형 설정</a>을 참고하십시오.</li><li>CMQ 이벤트 알림을 활성화 해야 할 경우, <a href="https://console.cloud.tencent.com/cmq">CMQ</a>로 이동하여 서비스를 활성화하고 템플릿을 생성하십시오.이벤트 알림 활성화 후, 지정된 CMQ는 MPS 이벤트 알림을 수신합니다.</li></ul></td>
</tr><tr>
<td>설정 항목</td>
<td>네</td>
<td>트랜스 코딩 작업, 화면 캡처 작업, gif 작업, 심사 작업, 콘텐츠 식별 작업 및 콘텐츠 분석 작업 중 하나 이상을 선택하여 설정할 수 있습니다. 자세한 내용은 <a href="https:// intl.cloud.tencent.com/document/product/1041/33485#p1">작업 설정 설명</a>을 참고하십시오.</td>
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


### 순서5:워크플로 활성화
1. 워크플로가 생성되면 "워크플로가 성공적으로 생성되었습니다"라는 안내가 표시됩니다.[워크플로 관리]를 클릭하여, [워크플로 관리](https://intl.cloud.tencent.com/document/product/1041/33485)로 이동합니다.
![](https://main.qcloudimg.com/raw/81ae87468f4c99773278fd6487e39bd4.png)
2. 워크플로는 기본적으로 비활성화 상태입니다. 워크플로가 위치한 행을 클릭하면 워크플로를 활성화할 수 있습니다.워크플로가 활성화된 경우에만 트리거 Bucket에 비디오 업로드 후 워크플로의 자동 실행이 트리거 됩니다.

 

### 순서6:비디오 업로드
1. 워크플로 활성화 후, [COS 콘솔](https://console.cloud.tencent.com/cos5) 왼쪽 메뉴에서 [버킷 리스트]를 클릭하여 ‘버킷 리스트’ 페이지로 이동합니다.
2. 워크플로에서 설정한 트리거 Bucket을 찾아 해당 버킷 이름을 클릭하면 ‘파일 목록’ 페이지로 들어가게 되며, 처리해야 하는 비디오 파일을 업로드하면 MPS가 워크플로 설정에 따라 새로 업로드된 비디오를 자동으로 처리합니다.
>? 워크플로의 자동 실행은 워크플로가 활성화된 후 트리거 Bucket에 새로 업로드된 비디오 파일에 대해서만 적용되며, 이전에 트리거 Bucket에 저장된 파일은 처리되지 않습니다. 


### 순서7:처리 완료된 비디오 보기
1. 비디오 처리가 완료되면 [COS 콘솔](https://console.cloud.tencent.com/cos5)로 이동하여 왼쪽 메뉴의 [버킷 리스트]를 클릭하여 ‘버킷리스트’ 페이지로 이동합니다.
2. 워크플로 설정 항목에서 설정된 출력 Bucket을 찾아 해당 버킷 이름을 클릭하면 ‘파일 목록’ 페이지로 들어가게 되며, 작업 설정에 따라 처리 완료된 비디오 파일을 볼 수 있습니다.





