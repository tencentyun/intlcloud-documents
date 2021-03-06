LVB는 라이브 방송 화면 녹화 및 파일을 VOD에 저장하는 서비스를 제공하며, 이를 통해 녹화한 비디오 파일을 다운로드 하고 미리보기 등의 처리를 할 수 있습니다. 본 문서에서는 녹화 템플릿의 생성, 바인딩, 바인딩 해제, 수정, 삭제 방법에 대해 소개합니다.
녹화 템플릿을 생성하는 방법으로는 다음 두 가지 방식이 있습니다.
- LVB 콘솔을 통한 녹화 템플릿 생성에 대한 자세한 방법은 [녹화 템플릿 생성](#C_record)을 참조하십시오.
- API를 통한 녹화 템플릿 생성에 대한 자세한 방법 및 사례는 [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/30845)을 참조하십시오.

## 주의 사항
- 녹화한 비디오 파일은 기본적으로 [VOD](https://console.cloud.tencent.com/vod/overview) 콘솔에 저장되며, 먼저 VOD 서비스를 활성화하고 VOD 서비스가 연체되어 중단되지 않도록 사전에 VOD 관련 리소스 패키지를 선택하시기 바랍니다. 자세한 내용은 [VOD 시작하기](https://intl.cloud.tencent.com/document/product/266/8757)를 참조하십시오.
- 녹화 기능을 활성화한 후에는 VOD 서비스의 정상 사용 상태를 유지해야 합니다. VOD 서비스를 활성화하지 않거나 계정이 연체되어 VOD 서비스가 중단되는 경우 라이브 방송을 녹화할 수 없으며, 해당 기간 동안에는 녹화 파일 및 녹화 비용이 발생하지 않습니다.
- 라이브 방송 중 녹화 종료 후 대략 5분 정도 후에 해당 녹화 파일을 획득할 수 있습니다. 예를 들어 라이브 방송에서 12:00에 녹화를 시작했다면 12:35 정도에 12:00~12:30의 섹션 파일을 획득할 수 있으며, 이와 같이 계속해서 생성해 나갑니다.
- 인코딩 유형은 멀티미디어 파일 포맷(FLV/MP4/HLS)으로 제한되며, 비디오 인코딩 유형은 H.264, 오디오 인코딩 유형은 ACC를 지원합니다.
- 녹화 템플릿 생성 완료 후 푸시 스트리밍 도메인과 연결할 수 있으며, 관련 문서는 [녹화 설정](https://intl.cloud.tencent.com/document/product/267/34224)을 참조하십시오. 연결 완료 후 약 5~10분 뒤에 적용됩니다.
- 생성된 녹화 파일 이름 생성 규칙은 [녹화 템플릿 매개변수-VodFileName](https://intl.cloud.tencent.com/document/product/267/30767#RecordParam)를 참조하십시오.
- 템플릿 바인딩 및 수정, 바인딩 해제는 업데이트 이후의 라이브 방송 스트리밍에만 적용되며, 현재 라이브 방송 중인 스트리밍에는 적용되지 않습니다. 라이브 방송 중인 스트리밍을 중단하고 다시 시작해야만 새로운 규칙이 적용됩니다.


## 전제 조건
- Tencent Cloud LVB 서비스를 활성화하고 [푸시 스트리밍 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가된 상태여야 합니다.
- [VOD 서비스](https://intl.cloud.tencent.com/document/product/266/8757#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E5.BC.80.E9.80.9A.E4.BA.91.E7.82.B9.E6.92.AD)를 활성화한 상태여야 합니다.

<span id="C_record"></span>
## 녹화 템플릿 생성
1. LVB 콘솔에 로그인하여 [Function Configuration]>[LVB Recording](https://console.cloud.tencent.com/live/config/record) 페이지로 이동합니다.
2. [+]를 클릭하여 다음과 같이 기본 정보를 설정합니다.
![](https://main.qcloudimg.com/raw/93c0660fe1c5eaf8bfc2a72e7c7944dc.png)
   <table>
   <thead><tr><th>설정 항목</th><th>설정 설명</th></tr></thead>
   <tbody><tr>
   <td>기본 템플릿</td>
   <td>라이브 방송 녹화 파일의 기본 템플릿 유형으로 FLV, MP4, HLS 세 가지 중 하나를 선택할 수 있습니다.</td>
   </tr><tr>
   <td>템플릿 이름</td>
   <td>라이브 방송 녹화 템플릿 이름을 설정(중문, 영문, 숫자, _, -만 지원)할 수 있습니다.</td>
   </tr><tr>
   <td>템플릿 설명</td>
   <td>라이브 방송 녹화 템플릿 소개를 설정(중문, 영문, 숫자, _, -만 지원)할 수 있습니다.</td>
   </tr><tr>
   <td>녹화 파일 유형</td>
   <td>비디오 녹화는 라이브 방송 원본 비트레이트에 맞춰 녹화되며 HLS, MP4, FLV, AAC 네 가지 출력 포맷이 있습니다. 이 중, AAC는 순수 오디오 녹화 파일 포맷입니다.</td>
   </tr><tr>
   <td>단일 파일 녹화 시간(분)</td>
   <td><ul style="margin-bottom:0px">
       <li>HLS 포맷 녹화 시 단일 파일 최장 길이에 제한이 없으며, 지속 녹화 만료 시간을 초과하는 경우 새로운 파일이 생성되고 계속 녹화가 이루어집니다.</li>
       <li>MP4, FLV 또는 AAC 포맷 녹화 시 단일 파일 최장 길이는 5~120분으로 제한됩니다.</li>
       </ul></td>
   </tr><tr>
   <td>파일 저장 기간(일)</td>
   <td>단일 녹화 파일의 최대 저장 기간은 약 1080일이며, 파일 저장 기간을 0으로 설정하면 영구 보관합니다.</td>
   </tr><tr>
   <td>지속 녹화 만료 시간(초)</td>
   <td>HLS 포맷에서만 파일의 푸시 스트리밍 중단 지속 녹화를 지원하며 지속 녹화 만료 시간은 0s~1800s로 설정할 수 있습니다.</td>
   </tr><tr>
   <td>서브 애플리케이션에 녹화</td>
   <td>VOD의 지정 <a href="https://console.cloud.tencent.com/vod/app-manage">서브 애플리케이션</a>에 녹화할 수 있으며, 기본적으로는 계정의 메인 애플리케이션에 녹화됩니다. 쓰기 상태가 활성화된 서브 애플리케이션에만 녹화할 수 있습니다.</td>
   </tr>
   </tbody></table>
3. [Save]를 클릭합니다.


<span id="conect"></span>
## 도메인 연결
1. LVB 콘솔에 로그인하여 [Function Configuration]>[LVB Recording](https://console.cloud.tencent.com/live/config/record) 페이지로 이동합니다.
	- **도메인 직접 연결:** 왼쪽 상단에 있는 [Bind Domain Name]을 클릭합니다.
	![](https://main.qcloudimg.com/raw/bcb6c5da46a3455f94d441134e49825a.png)
	- **신규 녹화 템플릿 생성 완료 후 도메인 연결: **[녹화 템플릿 생성](#C_record) 완료 후 안내창의 [Bind Domain Name]을 클릭합니다.
	![](https://main.qcloudimg.com/raw/7f26a83d95d0f08ceda1b10e93e30389.png)
1. 도메인 바인딩 창에서 바인딩할 **녹화 템플릿**과 **푸시 스트리밍 도메인**을 선택하고 [Confirm]을 클릭하면 바인딩이 완료됩니다.
![](https://main.qcloudimg.com/raw/a9411818457b4e708fd624f970d92ab6.png)

>? [추가]를 클릭하여 현재 템플릿에 여러 개의 푸시 스트리밍 도메인을 추가할 수 있습니다.

<span id="unite"></span>
## 바인딩 해제

1. LVB 콘솔에 로그인하여 [Function Configuration]>[LVB Recording](https://console.cloud.tencent.com/live/config/record) 페이지로 이동합니다.
2. 연결되어 있는 도메인의 녹화 템플릿을 선택하고 [Unbind]을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/e8fe04a68c90675cc038ebd51b2d99f5.png)
3. 현재 연결된 도메인의 바인딩 해제 여부를 확인하고 [Confirm]을 클릭하면 바인딩 해제가 완료됩니다.
  ![](https://main.qcloudimg.com/raw/a666387f882584860eaf2c229c2b4769.png)

>? 
>- 녹화 템플릿 바인딩을 해제해도 현재 라이브 방송 중인 스트리밍에는 영향을 주지 않습니다.
>- 바인딩 해제 적용이 필요한 경우, 해제 후 스트리밍을 중단하고 다시 푸시 스트리밍 라이브 방송을 시작하면 새로운 라이브 방송부터는 녹화 파일이 생성되지 않습니다.


<span id="change"></span>
## 템플릿 수정
1. [Feature Configuration]>[LVB Recording](https://console.cloud.tencent.com/live/config/record) 페이지로 이동합니다.
2. 생성된 녹화 템플릿을 선택하고 오른쪽에 있는 [Edit]를 클릭하면 템플릿 정보 수정 페이지로 이동합니다.
3. [Save]를 클릭합니다.

![](https://main.qcloudimg.com/raw/68f4dd1a6452a3e97e7ff4dea6493d7b.png)

<span id="delete"></span>
## 템플릿 삭제
1. [기능 설정]>[라이브 방송 녹화] 페이지로 이동합니다.
2. 생성된 녹화 템플릿을 선택하고 상단에 있는 삭제 버튼![](https://main.qcloudimg.com/raw/220ada95a4b631349543cc8cde96226e.png)을 클릭합니다.
3. 현재 녹화 템플릿의 삭제 여부를 확인하고 [확인]을 클릭하면 삭제가 완료됩니다.
![](https://main.qcloudimg.com/raw/e25f0566348f69e8c6afb64439c5e40f.png)

>! 
>- 템플릿이 이미 연결되어 있는 경우 먼저 [바인딩 해제](#unite)를 진행한 후 삭제할 수 있습니다.
>- 콘솔의 템플릿 관리에서는 현재 도메인 차원에서 연결 인터페이스 생성 규칙을 취소할 수 없습니다. 녹화 관리 인터페이스를 통해 지정한 스트림과 연결하고 있는 경우, [녹화 규칙 삭제](https://intl.cloud.tencent.com/document/product/267/30843) 를 참조하여 연결을 해제해야 합니다. 


## 관련 작업
녹화 템플릿에 대한 **도메인 차원의 바인딩** 및 **바인딩 해제**의 자세한 방법 및 관련 설명은 [녹화 설정](https://intl.cloud.tencent.com/document/product/267/34224)을 참조하십시오.


## 관련 문제
<span id="que1"></span>
#### 라이브 방송 녹화 후 생성되는 비디오 이름은 어떤 규칙으로 생성됩니까?
콘솔에서 생성한 녹화 템플릿의 콜백 후 생성되는 녹화 파일은 기본 조합 방식으로 이름이 생성되며 형식은 다음과 같습니다.
`{StreamID}*{StartYear}-{StartMonth}-{StartDay}-{StartHour}-{StartMinute}-{StartSecond}*{EndYear}-{EndMonth}-{EndDay}-{EndHour}-{EndMinute}-{EndSecond} `

**다음을 참고하십시오.**

| 항목             | 의미          |
| ------------------ | ------------- |
| {StreamID}         | 스트리밍 ID          |
| {StartYear}        | 시작 시간-년   |
| {StartMonth}       | 시작 시간-월   |
| {StartDay}         | 시작 시간-일   |
| {StartHour}        | 시작 시간-시 |
| {StartMinute}      | 시작 시간-분 |
| {StartSecond}      | 시작 시간-초   |
| {EndYear}          | 종료 시간-년   |
| {EndMonth}         | 종료 시간-월   |
| {EndDay}           | 종료 시간-일   |
| {EndHour}          | 종료 시간-시 |
| {EndMinute}        | 종료 시간-분 |
| {EndSecond}        | 종료 시간-초   |
