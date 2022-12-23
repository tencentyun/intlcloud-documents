CSS는 화면 캡처&음란물 감지 기능을 지원합니다. 콘솔을 통해 화면 캡처&음란물 감지 템플릿을 구성하고 푸시 도메인에 연결하면, 푸시 스트림 과정에서 라이브 방송 화면을 캡처하고, 라이브 방송 캡처 또는 음란물 감지 데이터를 Tencent Cloud의 COS에 저장합니다. 해당 푸시 도메인이 콜백 설정과 연결되어 있는 경우 라이브 방송 과정에서 콜백 이벤트가 트리거되며, Tencent Cloud에서 직접 클라이언트 서버에 요청을 발송하고 클라이언트 서버에서 요청에 응답합니다. 인증을 통과하면 음란물 감지 콜백 정보가 포함된 JSON 데이터 패키지를 획득하게 됩니다.
본 문서에서는 콘솔을 통해 화면 캡처&음란물 감지 템플릿을 생성, 바인딩, 바인딩 해제, 수정 및 삭제하는 방법에 대해 소개합니다.

그 중, 화면 캡처&음란물 감지 템플릿을 생성하는 방법으로는 다음 두 가지가 있습니다.

- CSS 콘솔을 통한 템플릿 생성에 대한 자세한 방법은 [화면 캡처&음란물 감지 템플릿 생성](#Screenshot)을 참고하십시오.
- API를 통한 템플릿 생성에 대한 자세한 매개변수 및 사례는 [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)을 참고하십시오.


## 주의 사항

- 화면 캡처 기능은 단독으로 활성화하여 사용할 수 있습니다. 그러나 음란물 감지 기능은 화면 캡처 기능을 활성화해야만 사용할 수 있으며 단독으로 사용할 수 없습니다.
- 화면 캡처 및 음란물 감지는 유료 기능입니다. 활성화 후 화면 캡처 기능은 1000장당 0.0176USD의 요금이 발생하며, 음란물 감지 기능은 1000장당 0.2294USD의 요금이 발생합니다. 자세한 내용은 [스마트 음란물 감지](https://intl.cloud.tencent.com/document/product/267/39607)를 참고하십시오.  
- 화면 캡처 및 음란물 감지 이미지는 사용자의 COS에 저장되며 COS 저장 비용이 발생합니다. 자세한 내용은 [COS 제품 가격](https://intl.cloud.tencent.com/pricing/cos)을 참고하십시오.
- **다른 계정**의 COS bucket에 데이터를 저장하려면, 먼저 해당 COS bucket에 쓸 수 있는 권한을 CSS에 부여해야 합니다. 자세한 내용은 [라이브 방송에 COS bucket 권한을 부여하여 화면 캡처 저장](https://intl.cloud.tencent.com/document/product/267/33384)을 참고하십시오.
- 템플릿 생성 완료 후 푸시 도메인과 연결할 수 있으며, 관련 문서는 [음란물 감지 화면 캡처 설정](https://intl.cloud.tencent.com/document/product/267/31063)을 참고하십시오. 템플릿 연결 성공 후 약 5~10분 뒤에 적용됩니다. 
- 콘솔의 화면 캡처&음란물 감지 템플릿은 현재 도메인 차원에서 관리되며, 연결 인터페이스 생성 규칙은 취소할 수 없습니다. 화면 캡처&음란물 감지 관련 인터페이스를 통해 지정한 스트림과 연결하고 있는 경우, [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833) 호출을 통해 연결을 해제해야 합니다.
- 템플릿 바인딩 및 수정, 바인딩 해제는 업데이트 이후의 라이브 방송 스트림에만 적용되며, 현재 라이브 방송 중인 스트림은 영향을 받지 않습니다. 라이브 방송 중인 스트림을 중단하고 다시 시작해야만 새로운 규칙이 적용됩니다.

## 전제 조건
-  CSS를 활성화하고 [푸시 도메인 이름](https://intl.cloud.tencent.com/document/product/267/35970)을 추가했습니다.
- COS Bucket을 생성합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참고하십시오.

[](id:Screenshot)
## 화면 캡처&음란물 감지 템플릿 생성
1. CSS 콘솔에 로그인하여 **기능 설정** > [**라이브 방송 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. **화면 캡처 및 음란물 감지 템플릿 생성**을 클릭합니다. **처음** 수행하는 경우 COS에 스크린샷을 저장할 수 있도록 서비스 역할을 생성하고 CSS 읽기 및 쓰기 액세스 권한을 COS에 부여해야 합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f27be286a9f3c68d96a55544a6c25b57.png)
3. 템플릿 설정을 완료하고 **저장**을 클릭합니다.
    <img src="https://main.qcloudimg.com/raw/544c2127f7870add334eaf760f1da089.png" style="zoom:67%;" />
<table>
<thead><tr><th width="15%">설정 항목</th><th>설명</th></tr></thead>
<tbody><tr>
<td>템플릿 이름</td>
<td>화면 캡처&음란물 감지 템플릿 이름을 입력합니다. 템플릿 이름은 중국어, 영어, 숫자, _, - 만 지원되며, 30자를 초과할 수 없습니다. </td>
</tr><tr>
<td>템플릿 설명</td>
<td>화면 캡처&음란물 감지 템플릿에 대한 설명으로 중국어, 영어, 숫자, _, - 만 지원되며, 30자를 초과할 수 없습니다. </td>
</tr><tr>
<td>화면 캡처 간격</td>
<td>푸시 스트림 중 자동 캡처 간격은 2초로 기본 설정되어 있으며, 2초 - 300초 범위 내에서 설정 가능합니다.</td>
</tr><tr>
<td>스마트 음란물 감지 활성화</td>
<td>음란물 감지 기능 활성화 여부를 선택할 수 있으며, 스마트 음란물 감지를 활성화한 뒤, 콜백 설정을 해야 음란물 감지 결과를 받아볼 수 있습니다. </td>
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
<td>상기 Bucket이 속한 리전 정보는 수정할 수 없습니다. </td>
</tr><tr>
<td>폴더</td>
<td>선택창을 클릭하여 COS 폴더를 선택합니다. 기본 설정은 <code>{Year}-{Month}-{Day}/</code>입니다. <br>설명: COS 폴더 이름에는 [a-z，A-Z，0-9]와 기호<code>-，!，_，.，*</code> 및 자리 표시 자만 허용됩니다. </td>
</tr><tr>
<td>파일 이름</td>
<td><ul style="margin:0"><li>화면 캡처 파일 이름 형식은 사용자 정의 조합 매개변수를 조합하여 생성할 수 있습니다. 기본 설정은 <code>{StreamID}-screenshot-{Hour}-{Minute}-{Second}-{Width}x{Height}{Ext}</code>이며, 다음을 참고하십시오.
			<ul style="margin:0">
					<li>{AppName}: 푸시 스트림 AppName</li>
					<li>{PushDomain}: 푸시 도메인</li>
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
		<li><b>설명: </b>[a-z，A-Z，0-9]와 기호-，!，_，.，* 및 플레이스 홀더만 허용됩니다.</li>
    <li><b>예시: </b>입력한 파일 이름 형식이 <code> {Year}-{Month}-{Day}- {Hour}-{Ext}</code>인 경우, 2020년 01월 01일 14:00:00에 라이브 방송 화면을 자동 캡처했음을 의미하며, COS에 저장한 파일 이름: <code>2020010114.jpg</code></li></ul></td>
</tr>
</tbody></table>

[](id:conect)
## 바인딩 도메인 이름

1. CSS 콘솔에 로그인하여 **기능 설정** > [**라이브 방송 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. 다음 방법 중 하나로 도메인 이름 바인딩 페이지로 이동합니다.
    - **기존 트랜스코딩 템플릿에 도메인 이름 바인딩:** 왼쪽 상단에서 **도메인 이름 바인딩**을 클릭합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/92b7542783d6d5ac59ef5faedbf53746.png)
    - **신규 화면 캡처&음란물 감지 템플릿 생성 완료 후 도메인 연결:** [화면 캡처&음란물 감지 템플릿 생성](#Screenshot) 완료 후 안내창의 **도메인 바인딩**을 클릭합니다.
    ![](https://qcloudimg.tencent-cloud.cn/raw/61c40816a357ce0f79677e238a1a31ba.png)
1. 도메인 바인딩 창에서 바인딩할 **화면 캡처&음란물 감지 템플릿**과 **푸시 도메인**을 선택하고 **확인**을 클릭하면 바인딩이 완료됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5e632f4a7712256fdd3f3a282e09a9c7.png)
>? **추가**를 클릭하여 현재 템플릿에 여러 개의 푸시 도메인을 추가할 수 있습니다.

[](id:unite)
## 도메인 이름 바인딩 해제

1. CSS 콘솔에 로그인하여 **기능 설정** > [**라이브 방송 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. 연결되어 있는 도메인의 라이브 방송 화면 캡처&음란물 감지 템플릿을 선택하고 **바인딩 해제**를 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e8a52af13916db8d50bc4395cfc5cc8d.png)
3. 현재 연결된 도메인의 바인딩 해제 여부를 확인하고 **확인**을 클릭하면 바인딩 해제가 완료됩니다.
   ![](https://main.qcloudimg.com/raw/9182f6589885ecba5fafcea075c9184e.png)

[](id:change)
## 템플릿 수정

1. **기능 설정** > [**라이브 방송 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. 생성된 화면 캡처 음란물 감지 템플릿을 선택하고 오른쪽에 있는 **편집**을 클릭하면 템플릿 정보 수정 페이지로 이동합니다.
3. **저장**을 클릭합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/786b4fd9630a178a0aebb65cda16a49c.png)

[](id:delete)
## 템플릿 삭제
>! 템플릿이 이미 연결되어 있는 경우 먼저 [바인딩 해제](#unite)를 진행해야 삭제할 수 있습니다.

1. **기능 설정** > [**라이브 방송 화면 캡처&음란물 감지**](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. 생성된 화면 캡처&음란물 감지 템플릿을 선택하고 상단의 삭제 버튼을 클릭합니다.
3. 현재 화면 캡처 및 음란물 감지 설정 템플릿의 삭제 여부를 확인하고 **확인**을 클릭하면 삭제가 완료됩니다.

![](https://main.qcloudimg.com/raw/6ae7a299517803a92776d8077ccda1d3.png)

## 관련 작업
워터마크 템플릿의 **도메인 차원의 바인딩** 및 **바인딩 해제**화면 캡처&음란물 감지 템플릿에 대한 자세한 방법 및 관련 설명은 [음란물 감지 화면 캡처 설정](https://intl.cloud.tencent.com/document/product/267/31063)을 참고하십시오.