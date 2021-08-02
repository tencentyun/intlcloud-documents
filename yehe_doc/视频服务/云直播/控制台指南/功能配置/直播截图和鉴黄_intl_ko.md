CSS는 화면 캡처&음란물 감지 기능을 지원합니다. 콘솔을 통해 화면 캡처&음란물 감지 템플릿을 구성하고 푸시 도메인에 연결하면, 푸시 스트림 과정에서 라이브 방송 화면을 캡처하고, 라이브 방송 캡처 또는 음란물 감지 데이터를 Tencent Cloud의 COS에 저장합니다. 해당 푸시 도메인이 콜백 설정과 연결되어 있는 경우 라이브 방송 과정에서 콜백 이벤트가 트리거되며, Tencent Cloud에서 직접 클라이언트 서버에 요청을 발송하고 클라이언트 서버에서 요청에 응답합니다. 인증을 통과하면 음란물 감지 콜백 정보가 포함된 JSON 데이터 패키지를 획득하게 됩니다.
본 문서에서는 콘솔을 통해 화면 캡처&음란물 감지 템플릿을 생성, 바인딩, 바인딩 해제, 수정 및 삭제하는 방법에 대해 소개합니다.

그 중, 화면 캡처&음란물 감지 템플릿을 생성하는 방법으로는 다음 두 가지가 있습니다.

- CSS 콘솔을 통한 템플릿 생성에 대한 자세한 방법은 [화면 캡처&음란물 감지 템플릿 생성](#Screenshot)을 참고하십시오.
- API를 통한 템플릿 생성에 대한 자세한 매개변수 및 사례는 [화면 캡처 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/30834)을 참고하십시오.



##  주의 사항

- 화면 캡처 기능은 단독으로 활성화하여 사용할 수 있습니다. 그러나 음란물 감지 기능은 화면 캡처 기능을 활성화해야만 사용할 수 있으며 단독으로 사용할 수 없습니다.
- 화면 캡처 및 음란물 감지는 유료 기능입니다. 활성화 후 화면 캡처 기능은 1000장당 0.0176USD의 요금이 발생하며, 음란물 감지 기능은 1000장당 0.2294USD의 요금이 발생합니다. 자세한 내용은 [스마트 성인물 감지](https://intl.cloud.tencent.com/document/product/267/39607)를 참고하십시오.  
- 화면 캡처 및 음란물 감지 이미지는 사용자의 COS에 저장되며 COS 저장 비용이 발생합니다. 자세한 내용은 [COS 제품 가격](https://intl.cloud.tencent.com/pricing/cos)을 참고하십시오.
- 화면 캡처 기능을 활성화하려면 먼저 COS bucket에서 CSS 서비스의 데이터 쓰기 권한을 설정해야 합니다. 자세한 내용은 [라이브 방송에 COS bucket 권한을 부여하여 화면 캡처 저장](https://intl.cloud.tencent.com/document/product/267/33384)을 참고하십시오.
- 템플릿 생성 완료 후 푸시 도메인과 연결할 수 있으며, 관련 문서는 [화면 캡처&음란물 감지 설정](https://intl.cloud.tencent.com/document/product/267/31063)을 참고하십시오. 템플릿 연결 성공 후 약 5~10분 뒤에 적용됩니다. 
- 콘솔의 화면 캡처&음란물 감지 템플릿은 현재 도메인 차원에서 관리되며, 연결 인터페이스 생성 규칙은 취소할 수 없습니다. 화면 캡처&음란물 감지 관련 인터페이스를 통해 지정한 스트림과 연결하고 있는 경우, [화면 캡처 규칙 삭제](https://intl.cloud.tencent.com/document/product/267/30833) 호출을 통해 연결을 해제해야 합니다.
- 템플릿 바인딩 및 수정, 바인딩 해제는 업데이트 이후의 라이브 방송 스트림에만 적용되며, 현재 라이브 방송 중인 스트림은 영향을 받지 않습니다. 라이브 방송 중인 스트림을 중단하고 다시 시작해야만 새로운 규칙이 적용됩니다.



## 전제 조건

- Tencent Cloud CSS 서비스를 활성화하고 [푸시 도메인](https://intl.cloud.tencent.com/document/product/267/35970)이 추가된 상태여야 합니다.
- COS Bucket이 생성되어 있고 COS Bucket을 통해 CSS에 권한을 부여해야 합니다. 자세한 내용은 [라이브 방송에 COS bucket 권한을 부여하여 화면 캡처 저장](https://intl.cloud.tencent.com/document/product/267/33384)을 참고하십시오.



<span id="Screenshot"></span>
## 화면 캡처&음란물 감지 템플릿 생성

1. CSS 콘솔에 로그인하여 [기능 설정]>[[라이브 방송 화면 캡처&음란물 감지]](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. [화면 캡처&음란물 감지 템플릿 생성]을 클릭하고 설정 항목을 입력한 뒤 [저장]을 클릭합니다.
![](https://main.qcloudimg.com/raw/544c2127f7870add334eaf760f1da089.png)
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
<td>푸시 스트림 중 자동 캡처 간격은 2초로 기본 설정되어 있으며, 2초-300초 범위 내에서 설정 가능합니다.
<td>스마트 성인물 감지 활성화</td>
<td>음란물 감지 기능 활성화 여부를 선택할 수 있으며, 스마트 성인물 감지를 활성화한 뒤, 콜백 설정을 해야 음란물 감지 결과를 받아볼 수 있습니다. </td>
</tr><tr>
<td>스토리지 계정</td>
<td>『현재 계정』 또는 『다른 계정』을 선택할 수 있습니다. </td>
</tr><tr>
<td>AppId</td>
<td>스토리지 계정 유형을 『다른 계정』으로 선택한 경우에만 입력이 필요하며, APPID 정보는 다른 계정의 <a href="https://console.cloud.tencent.com/developer">[계정 정보]</a>에서 얻을 수 있습니다. </td>
</tr><tr>
<td>Bucket</td>
<td>[COS]에서 생성 및 권한 부여를 완료한 COS bucket을 선택합니다. </td>
</tr><tr>
<td>Region</td>
<td>상기 Bucket이 속한 리전 정보는 수정할 수 없습니다. </td>
</tr><tr>
<td>폴더</td>
<td>선택창을 클릭하여 COS 폴더를 선택합니다. 기본 설정은 <code>{Year}-{Month}-{Day}/</code>입니다. <br>설명: COS 폴더 이름에는 [a-z，A-Z，0-9]와 기호<code>-，!，_，.，*</code> 및 자리 표시 자만 허용됩니다. </td>
</tr><tr>
<td>파일 이름</td>
<td>화면 캡처 파일 이름 형식은 사용자 정의 조합 매개변수를 조합하여 생성할 수 있습니다. 기본 설정은 <code>{StreamID}-screenshot-{Hour}-{Minute}-{Second}-{Width}x{Height}{Ext}</code>이며, 다음을 참고하십시오.
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
    </ul>설명: [a-z，A-Z，0-9]와 기호-，!，_，.，* 및 자리 표시 자만 허용됩니다.
    <br>예시: 입력한 파일 이름 형식이 <code> {Year}-{Month}-{Day}- {Hour}-{Ext}</code>인 경우, 2020년 01월 01일 14:00:00에 라이브 방송 화면을 자동 캡처했음을 의미하며, COS에 저장한 파일 이름은 2020010114.jpg입니다.</td>
</tr>
</tbody></table>


<span id="conect"></span>
## 도메인 연결

1. CSS 콘솔에 로그인하여 [기능 설정]>[[라이브 방송 화면 캡처&음란물 감지]](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. 다음과 같은 방식으로 도메인 바인딩 창으로 이동합니다.
    - **도메인 직접 연결:** 왼쪽 상단에 있는 [도메인 바인딩]을 클릭합니다.
    ![](https://main.qcloudimg.com/raw/20490c4aa318f5b5253d0b82c1672087.png)
    - **신규 화면 캡처&음란물 감지 템플릿 생성 완료 후 도메인 연결: **[화면 캡처&음란물 감지 템플릿 생성](#Screenshot) 완료 후 안내창의 [도메인 바인딩]을 클릭합니다.
    ![](https://main.qcloudimg.com/raw/727b1d25f256a655478312ee45814a32.png)
1. 도메인 바인딩 창에서 바인딩할 **화면 캡처&음란물 감지 템플릿**과 **푸시 도메인**을 선택하고 [확인]을 클릭하면 바인딩이 완료됩니다.
![](https://main.qcloudimg.com/raw/5612913bcbb6ac1cb5207dcc03e997c4.png)
> ? [추가]를 클릭하여 현재 템플릿에 여러 개의 푸시 도메인을 바인딩할 수 있습니다.


<span id="unite"></span>
## 바인딩 해제

1. CSS 콘솔에 로그인하여 [기능 설정]>[[라이브 방송 화면 캡처&음란물 감지]](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. 연결되어 있는 도메인의 라이브 방송 화면 캡처&음란물 감지 템플릿을 선택하고 [바인딩 해제]를 클릭합니다.
   ![](https://main.qcloudimg.com/raw/fd20557cc393cc483d9a36dd0ddb6652.png)
3. 현재 연결된 도메인의 바인딩 해제 여부를 확인하고 [확인]을 클릭하면 바인딩 해제가 완료됩니다.
   ![](https://main.qcloudimg.com/raw/9182f6589885ecba5fafcea075c9184e.png)


<span id="change"></span>
## 템플릿 수정

1. [기능 설정]>[[라이브 방송 화면 캡처&음란물 감지]](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. 생성된 화면 캡처&음란물 감지 템플릿을 선택하고 오른쪽에 있는 [편집]을 클릭하면 템플릿 정보 수정 페이지로 이동합니다.
3. [저장]을 클릭합니다.

![](https://main.qcloudimg.com/raw/0ec0dcb3dc35571e1aab74b20d533c35.png)


<span id="delete"></span>
## 템플릿 삭제

>! 템플릿이 이미 연결되어 있는 경우 먼저 [바인딩 해제](#unite)를 진행해야 삭제할 수 있습니다.

1. [기능 설정]>[[라이브 방송 화면 캡처&음란물 감지]](https://console.cloud.tencent.com/live/config/jtjh) 페이지로 이동합니다.
2. 생성된 화면 캡처&음란물 감지 템플릿을 선택하고 상단의 삭제 버튼을 클릭합니다.
3. 현재 화면 캡처&음란물 감지 설정 템플릿의 삭제 여부를 확인하고 [확인]을 클릭하면 삭제가 완료됩니다.

![](https://main.qcloudimg.com/raw/6ae7a299517803a92776d8077ccda1d3.png)



## 관련 작업
워터마크 템플릿의 **도메인 차원의 바인딩** 및 **바인딩 해제**화면 캡처&음란물 감지 템플릿에 대한 자세한 방법 및 관련 설명은 [음란물 감지 화면 캡처 설정](https://intl.cloud.tencent.com/document/product/267/31063)을 참고하십시오.
