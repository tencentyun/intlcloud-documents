CSS는 음란물 감지를 지원합니다(화면 캡처 기반). 콘솔에서 화면 캡처 및 음란물 감지 템플릿을 구성하고 푸시 도메인에 바인딩할 수 있으며 CSS는 도메인 스트림의 화면을 캡처하고 음란물 감지를 수행합니다. 결과는 COS(Cloud Object Storage)에 저장됩니다. 푸시 도메인도 콜백 템플릿과 결합된 경우 음란물 감지가 수행된 후 Tencent Cloud가 서버에 요청을 보냅니다. 서버가 인증을 통과하면 음란물 감지 콜백이 포함된 JSON 패킷을 수신합니다.
본문은 콘솔에서 화면 캡처 및 음란물 감지 템플릿을 생성, 바인딩, 바인딩 해제, 수정 및 삭제하는 방법을 설명합니다.

다음과 같은 방법으로 화면 캡처 및 음란물 감지 템플릿을 생성할 수 있습니다.

- CSS 콘솔에서 템플릿을 만듭니다. 자세한 내용은 [화면 캡처&음란물 감지 템플릿 생성](#Screenshot)을 참고하십시오.
- API를 호출하여 템플릿을 생성합니다. 매개변수 및 요청 샘플에 대한 자세한 내용은 [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)을 참고하십시오.

## 참고 사항

- 음란물 감지 기능 외에도 음란물 감지를 수행하려면 콘솔에서 화면 캡처를 활성화해야 합니다.
- 화면 캡처 및 음란물 감지 기능의 가격은 화면 캡처 1000장당 각각 0.0176 USD 및 0.2294 USD입니다. 자세한 내용은 [스마트 음란물 감지](https://intl.cloud.tencent.com/document/product/267/39607)를 참고하십시오.  
- 화면 캡처와 음란물 감지 결과는 COS 버킷에 저장되며 COS 저장 요금이 발생합니다. 자세한 내용은 [가격Cloud Object Storage](https://intl.cloud.tencent.com/pricing/cos)를 참고하십시오.
- 오디오 전용 스트림의 경우 화면 캡처 실패가 발생하며, 이 경우 화면 캡처 요금이 발생하지 않습니다.
- **다른 계정**의 COS bucket에 데이터를 저장하려면, 먼저 해당 COS bucket에 쓸 수 있는 권한을 CSS에 부여해야 합니다. 자세한 내용은 [라이브 방송에 COS bucket 권한을 부여하여 화면 캡처 저장](https://intl.cloud.tencent.com/document/product/267/33384)을 참고하십시오.
- COS Bucket의 액세스 권한이 공개 읽기일 때, 정치적으로 민감한 내용, 음란물 또는 기타 부적절한 콘텐츠가 있는 경우 COS Bucket이 차단되지 않도록 하려면 먼저 콘텐츠를 삭제하십시오.
- 템플릿 생성 후 푸시 도메인 이름으로 바인딩할 수 있습니다. 자세한 내용은 [음란물 감지 화면 캡처 설정](https://intl.cloud.tencent.com/document/product/267/31063)을 참고하십시오. 바인딩은 약 5 - 10분 후에 적용됩니다. 
- 콘솔에서 템플릿은 도메인 레벨에서 관리됩니다. API에 의해 바인딩된 화면 캡처 규칙을 바인딩 해제하려면 [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833)을 호출하십시오.
- 템플릿 바인딩 및 수정, 바인딩 해제는 진행 중인 라이브 스트림이 아닌 새로운 라이브 스트림에만 영향을 미칩니다. 진행 중인 라이브 스트림에 변경 사항을 적용하려면 스트림을 중지하고 다시 푸시해야 합니다.

## 전제 조건
-  CSS를 활성화하고 [푸시 도메인](https://intl.cloud.tencent.com/document/product/267/35970)을 추가해야 합니다.
- COS Bucket을 생성해야 합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참고하십시오.

[](id:Screenshot)
## 화면 캡처&음란물 감지 템플릿 생성
1. CSS 콘솔에 로그인하고 왼쪽 사이드바에서 **기능 구성** > [**라이브 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh)를 선택합니다.
2. **화면 캡처 및 음란물 감지 템플릿 생성**을 클릭합니다. **처음** 수행하는 경우 지금 승인을 클릭하여 서비스 역할을 생성하고 COS에 화면 스크린샷을 저장할 수 있도록 CSS 읽기 및 쓰기 액세스 권한을 COS에 부여하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/f27be286a9f3c68d96a55544a6c25b57.png)
3. 템플릿 설정을 완료하고 **저장**을 클릭합니다.
    <img src="https://main.qcloudimg.com/raw/544c2127f7870add334eaf760f1da089.png" style="zoom:67%;" />
<table>
<thead><tr><th width="15%">구성 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>템플릿 이름</td>
<td>화면 캡처&음란물 감지 템플릿 이름입니다. 중국어, 영어, 숫자, _, - 만 지원되며, 30자를 초과할 수 없습니다. </td>
</tr><tr>
<td>템플릿 설명</td>
<td>화면 캡처&음란물 감지 템플릿에 대한 설명입니다. 중국어, 영어, 숫자, _, - 만 지원되며, 100자를 초과할 수 없습니다. </td>
</tr><tr>
<td>화면 캡처 간격</td>
<td>기본적으로 2초인 화면 캡처 간격입니다. 값 범위: 2초 - 300초.</td>
</tr><tr>
<td>스마트 음란물 감지 활성화</td>
<td>스마트 음란물 감지를 활성화할지 여부입니다. 활성화된 경우 음란물 감지 결과를 수신하기 전에 콜백 템플릿을 구성해야 합니다.</td>
</tr><tr>
<td>스토리지 계정</td>
<td><b>현재 계정</b> 또는 <b>기타 계정</b>을 선택합니다.</td>
</tr><tr>
<td>AppId</td>
<td>스토리지 계정 유형으로 <b>기타 계정</b>을 선택한 경우에만 필요합니다. 콘솔의<a href="https://console.cloud.tencent.com/developer"> 계정 정보 </a>페이지에서 계정의 APPID를 볼 수 있습니다. 다른 계정의 COS bucket에 데이터를 저장하려면 먼저 해당 버킷에 대한 CSS 읽기 및 쓰기 액세스 권한을 부여해야 합니다. 자세한 내용은 <a href=" https://intl.cloud.tencent.com/document/product/267/33384">라이브 방송에 COS bucket 권한을 부여하여 화면 캡처 저장</a>을 참고하십시오.
    </td>
</tr><tr>
<td>Bucket</td>
    <td><b>COS</b>에서 생성 및 권한 부여를 완료한 COS bucket을 선택합니다. </td>
</tr><tr>
<td>Region</td>
<td>수정할 수 없는 Bucket의 리전입니다.</td>
</tr><tr>
<td>폴더</td>
<td>선택창을 클릭하여 COS 폴더를 선택합니다. 기본값은 <code>{Year}-{Month}-{Day}/</code>입니다. <br>참고: COS 폴더 이름에는 [a-z, A-Z, 0-9]와 기호<code>-, !, _, ., *</code> 및 플레이스 홀더만 허용됩니다.</td>
</tr><tr>
<td>파일 이름</td>
<td><ul style="margin:0"><li>화면 캡처 파일 이름 형식은 사용자 정의 조합 매개변수를 조합하여 생성할 수 있습니다. 기본 설정은 <code>{StreamID}-screenshot-{Hour}-{Minute}-{Second}-{Width}x{Height}{Ext}</code>이며, 다음을 참고하십시오.
			<ul style="margin:0">
					<li>{AppName}: 푸시 AppName</li>
					<li>{PushDomain}: 푸시 도메인 이름</li>
					<li>{StreamID}: 스트림 ID</li>
					<li>{Year}: 화면 캡처 시간(년)</li>
					<li>{Month}: 화면 캡처 시간(월)</li>
					<li>{Day}: 화면 캡처 시간(일)</li>
					<li>{Hour} 화면 캡처 시간(시)</li>
					<li>{Minute}: 화면 캡처 시간(분)</li>
					<li>{Second}: 화면 캡처 시간(초)</li>
					<li>{Width}: 이미지 너비</li>
					<li>{Height}: 이미지 높이</li><li>{Ext}: 확장자(.jpg)</li>
			</ul>
		<li><b>설명: </b>[a-z, A-Z, 0-9]와 기호-, !, _, ., * 및 플레이스 홀더만 허용됩니다.</li>
    <li><b>예시: </b>입력한 파일 이름 형식이 <code> {Year}-{Month}-{Day}- {Hour}-{Ext}</code>인 경우, 2020년 01월 01일 14:00:00에 라이브 방송 화면을 자동 캡처했음을 의미하며, COS에 저장한 파일 이름: <code>2020010114.jpg</code></li></ul></td>
</tr>
</tbody></table>

[](id:conect)
## 도메인 이름 바인딩

1. CSS 콘솔에 로그인하여 왼쪽 사이드바에서 **기능 구성** > [**라이브 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh)를 선택합니다.
2. 다음 방법 중 하나로 도메인 이름 바인딩 페이지로 이동합니다.
    - **기존 템플릿에 도메인 바인딩:** 왼쪽 상단에서 **도메인 이름 바인딩**을 클릭합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/92b7542783d6d5ac59ef5faedbf53746.png)
    - **화면 캡처&음란물 감지 템플릿 생성 완료 후 도메인 이름 바인딩:** [화면 캡처&음란물 감지 템플릿 생성](#Screenshot) 완료 후 팝업 창에서 **도메인 이름 바인딩**을 클릭합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/61c40816a357ce0f79677e238a1a31ba.png)
1. **화면 캡처&음란물 감지 템플릿**과 **푸시 도메인**을 선택하고 **확인**을 클릭하면 바인딩이 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5e632f4a7712256fdd3f3a282e09a9c7.png)
>? **추가**를 클릭하여 여러 푸시 도메인을 템플릿에 바인딩할 수 있습니다.

[](id:unite)
## 도메인 이름 바인딩 해제

1. CSS 콘솔에 로그인하여 왼쪽 사이드바에서 **기능 구성** > [**라이브 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh)를 선택합니다.
2. 대상 화면 캡처&음란물 감지 템플릿을 선택하고 해제할 도메인을 찾은 다음 **바인딩 해제**를 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e8a52af13916db8d50bc4395cfc5cc8d.png)
3. 팝업 창에서 **확인**을 클릭합니다.
   ![](https://main.qcloudimg.com/raw/9182f6589885ecba5fafcea075c9184e.png)

[](id:change)
## 템플릿 수정

1. 왼쪽 사이드바에서 **기능 구성** > [**라이브 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh)를 선택합니다.
2. 화면 캡처 음란물 감지 템플릿을 선택하고 오른쪽에 있는 **편집**을 클릭하여 수정합니다.
3. **저장**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/786b4fd9630a178a0aebb65cda16a49c.png)

[](id:delete)
## 템플릿 삭제
>! 템플릿이 도메인에 바인딩된 경우 템플릿을 삭제하기 전에 [바인딩 해제](#unite)를 해야 합니다.

1. 왼쪽 사이드바에서 **기능 구성** > [**라이브 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh)를 선택합니다.
2. 화면 캡처&음란물 감지 템플릿을 선택하고 오른쪽 상단의 삭제를 클릭합니다.
3. 팝업 창에서 **확인**을 클릭하면 삭제가 완료됩니다.

![](https://main.qcloudimg.com/raw/6ae7a299517803a92776d8077ccda1d3.png)

## 관련 작업
**도메인 이름 바인딩** 및 **바인딩 해제**에 대한 자세한 내용은 [화면 캡처&음란물 감지 설정](https://intl.cloud.tencent.com/document/product/267/31063)을 참고하십시오.