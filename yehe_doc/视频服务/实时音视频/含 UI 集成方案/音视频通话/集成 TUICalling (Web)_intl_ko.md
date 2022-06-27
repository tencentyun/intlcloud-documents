## 컴포넌트 개요
TUICalling은 오픈 소스 오디오/비디오 컴포넌트입니다. **영상 통화** 기능을 데스크톱 브라우저에 빠르게 통합하는 데 도움이 되며 온라인 의료 상담, 온라인 고객 서비스 및 원격 보험 청구와 같은 시나리오에 적합합니다.
<table class="tablestyle">
<tbody><tr>
<td style="vertical-align: top;"><img src="https://qcloudimg.tencent-cloud.cn/raw/a2b6bdc19d17d4e105b1d04a53d67957.png"></td>
</tr>
</tbody></table>


#### 기타 플랫폼
Web용 TUICalling 외에도 Android, iOS, Flutter 및 Uniapp 플랫폼용 소스 코드도 제공합니다. TUICalling은 Android 및 iOS에서 ‘수신 전화 알림’ 기능도 지원합니다.

>?
>- **Web용 TUICalling 외에도 Android, iOS, Flutter 및 Uniapp 플랫폼용 소스 코드도 제공합니다. TUICalling은 Android 및 iOS에서 ‘수신 전화 알림’ 기능도 지원합니다.** 
>- 질문이나 제안 사항이 있으면 [고객센터](https://intl.cloud.tencent.com/contact-us)로 연락하십시오.

## 컴포넌트 통합

[](id:step1)
### 1단계: SdkAppId 및 서명 키 가져오기
- Tencent Cloud 계정이 없으시다면 회원 가입 후 [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629)를 완료해 주십시오. 그런 다음 TRTC 콘솔의 [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) 페이지로 이동합니다.
- 애플리케이션 목록이 비어 있는 경우 **애플리케이션 생성**을 클릭하여 애플리케이션을 생성할 수 있습니다. **애플리케이션 정보**를 클릭하여 애플리케이션 관리 페이지로 이동하고 **빠른 시작** 탭을 선택하여 다음 콘텐츠를 확인합니다.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png" width="700">
- **SDKAppID**: 비즈니스 격리에 사용되는 TRTC 애플리케이션 ID. 즉, SDKAppID 값이 다른 호출은 상호 연결할 수 없습니다.
- **Secretkey**: TRTC의 승인된 사용을 위한 인증 자격 증명 UserSig를 생성하기 위해 SDKAppID와 함께 사용해야 하는 TRTC 애플리케이션 키입니다. 5단계에서 사용됩니다.

[](id:step2)
### 2단계: TRTCCalling 컴포넌트 다운로드 및 통합
[GitHub](https://github.com/tencentyun/TUICalling)으로 이동하여 코드를 복제 또는 다운로드하고 Web 디렉터리를 참고하여 코드를 구현합니다.

>?
>- v0.6.0부터 종속성 [trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk), [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk) 및 [tsignaling](https://www.npmjs.com/package/tsignaling)을 수동으로 설치해야 합니다.
>- trtc-calling-js.js의 크기를 줄이고 trtc-calling-js.js와 이미 사용 중인 trtc-js-sdk, tim-js-sdk, tsignaling 간의 버전 충돌을 방지하기 위해 trtc-calling-js.js에 trtc-js-sdk, tim-js-sdk, tsignaling이 외부 종속으로 패키징되어 있습니다. 사용 전 수동으로 설치해야 합니다.

<dx-codeblock>
::: javascript javascript
// npm 설치
  npm install trtc-js-sdk --save

  npm install tim-js-sdk --save

  npm install tsignaling --save

  npm install trtc-calling-js --save
:::
</dx-codeblock>

<dx-codeblock>
::: html html
// script로 trtc-calling-js를 사용해야 하는 경우 순서에 따라 다음 리소스를 수동으로 가져와야 합니다.

<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tsignaling.js"></script>
<script src="./trtc-calling-js.js"></script>
:::
</dx-codeblock>

[](id:step3)
### 3단계: TRTCCalling 객체 생성
TRTCCalling 객체를 생성하고 SDKAppID를 애플리케이션의 SDKAppID로 설정합니다.
```javascript
// Web/src/trtc-calling/index.js 참고
import TRTCCalling from 'trtc-calling-js';

let options = {
	SDKAppID: 0, // 액세스 시 0을 사용자의 SDKAppID로 대체해야 합니다.
	// v0.10.2부터 tim 매개변수가 추가되었습니다.
	// tim 매개변수는 TIM 인스턴스의 고유성을 보장하기 위해 비즈니스의 기존 TIM 인스턴스에 적용됩니다.
	tim: tim
};
const trtcCalling = new TRTCCalling(options);
```

[](id:step4)
### 4단계: 컴포넌트 로그인 및 이벤트 수신 대기
```javascript
// Web/src/components/login/index.vue 참고
trtcCalling.login({
	userID,
	userSig,
});

// Web/src/App.vue 참고

export default {
	name: "App",
	components: {
	},
	async created() {
		this.initListener();
	},
	data() {
		return {};
	},
	destroyed() {
		this.removeListener();
	},
	methods: {
		initListener: function() {
			// 원격 사용자 호출
			trtcCalling.on(trtcCalling.EVENT.INVITED, this.handleNewInvitationReceived);
			// 원격 사용자 호출 수신
			trtcCalling.on(trtcCalling.EVENT.USER_ACCEPT, this.handleUserAccept);
			// 원격 사용자 호출 거부
			trtcCalling.on(trtcCalling.EVENT.REJECT, this.handleInviteeReject);
			// ...
		},
		removeListener: function() {
			trtcCalling.off(trtcCalling.EVENT.INVITED, this.handleNewInvitationReceived);
			trtcCalling.off(trtcCalling.EVENT.USER_ACCEPT, this.handleUserAccept);
			trtcCalling.off(trtcCalling.EVENT.REJECT, this.handleInviteeReject);
		},
		handleNewInvitationReceived: async function(payload) {
		},
		handleUserAccept: function() {
		},
		handleInviteeReject: function() {
		}
	}
}
```

[](id:step5)
### 5단계: 1v1 통화
- **발신자: 사용자 호출**
```javascript
// Web/src/components/video-call/index.vue 또는 Web/src/components/audio-call/index.vue 참고
trtcCalling.call({
  userID,  //사용자 ID
  type: 2, //통화 유형, 0-알 수 없음, 1-음성 통화, 2-영상 통화
  timeout  //시간 초과 임계값(초)
});
```
- **수신자: 통화 초대 처리**
```javascript
// Web/src/App.vue handleAcceptCall 메소드 참고
// 수신
trtcCalling.accept();
// 거부
trtcCalling.reject()
```
- **로컬 카메라 켜기**
```javascript
trtcCalling.openCamera()
```
- **원격 사용자의 비디오 재생**
```javascript
trtcCalling.startRemoteView({
  userID, //원격 사용자 ID
  videoViewDomID //사용자 데이터는 이 DOM 노드에서 렌더링됩니다.
})
```
- **로컬 비디오 미리보기 표시**
```javascript
trtcCalling.startLocalView({
  userID, //로컬 사용자 ID
  videoViewDomID //사용자 데이터는 이 DOM 노드에서 렌더링됩니다.
})
```
- **통화 종료**
```javascript
trtcCalling.hangup()
```

## FAQ

### 사용자에게 연결할 수 없는 이유는 무엇입니까? 강제 오프라인되는 이유는 무엇입니까?
컴포넌트는 여러 인스턴스의 로그인 또는 **오프라인 신호**를 지원하지 않습니다. 현재 로그인이 고유한지 확인하십시오.
> ?
> - **다중 인스턴스**: 사용자가 동일한 계정으로 여러 번 또는 다른 장치에 로그인하여 신호를 방해합니다.
> - **오프라인 신호**: 온라인 인스턴스만 메시지를 수신할 수 있습니다. 오프라인 인스턴스로 전송된 메시지는 인스턴스가 온라인 상태가 되면 다시 전송되지 않습니다.

### 환경 요구 사항은 무엇입니까?
Chrome의 데스크톱 버전은 TRTC Web SDK의 기능에 대한 더 나은 지원을 제공합니다. 따라서 데모에는 Chrome을 권장합니다.

TRTCCalling은 방화벽의 얼로우리스트에 추가되어야 하는 데이터 전송을 위해 다음 포트와 도메인 이름을 사용합니다. 구성 후 [공식 Demo](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html)를 사용하여 구성이 적용되었는지 확인하십시오.
- **TCP 포트**: 8687
- **UDP 포트**: 8000, 8080, 8800, 843, 443, 16285
- **도메인**: qcloud.rtc.qq.com. 자세한 내용은 [방화벽 제한 대응 관련 질문](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하십시오.
- **지원되는 플랫폼**: 현재 이 솔루션은 다음 플랫폼을 지원합니다.
<table>
<thead><tr><th>OS</th><th>브라우저</th><th>최소 브라우저 버전 요구 사항</th></tr></thead>
<tbody><tr>
<td>Mac OS</td>
<td>Safari 브라우저(데스크톱)</td>
<td>11+</td>
</tr><tr>
<td>Mac OS</td>
<td>Chrome 브라우저(데스크톱)</td>
<td>56+</td>
</tr><tr>
<td>Mac OS</td>
<td>데스크톱 Firefox 브라우저</td>
<td>56+</td>
</tr><tr>
<td>Mac OS</td>
<td>데스크톱 Edge 브라우저</td>
<td>80+</td>
</tr><tr>
<td>Windows</td>
<td>Chrome 브라우저(데스크톱)</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>QQ 브라우저(데스크톱, WebKit 코어)</td>
<td>10.4+</td>
</tr><tr>
<td>Windows</td>
<td>Firefox 브라우저(데스크톱)</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>Edge 브라우저(데스크톱)</td>
<td>80+</td>
</tr>
</tbody></table>

>? 브라우저 호환성에 대한 자세한 내용은 [지원되는 브라우저](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)를 참고하십시오. [TRTC 호환성 확인 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 사용하여 온라인 테스트를 실행할 수도 있습니다.

- **URL 프로토콜 지원:**:
<table>
<thead><tr><th>시나리오</th><th>프로토콜</th><th>수신(재생)</th><th>발송(게시)</th><th>화면 공유</th><th>비고</th></tr></thead>
<tbody><tr>
<td>프로덕션 환경</td>
<td>HTTPS 프로토콜</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
<td>권장</td>
</tr><tr>
<td>프로덕션 환경</td>
<td>HTTP 프로토콜</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
<td>-</td>
</tr><tr>
<td>로컬 개발 환경</td>
<td>http://localhost</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
<td>권장</td>
</tr><tr>
<td>로컬 개발 환경</td>
<td>http://127.0.0.1</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
<td>-</td>
</tr><tr>
<td>로컬 개발 환경</td>
<td>http://[로컬IP]</td>
<td>지원</td>
<td>미지원</td>
<td>미지원</td>
<td>-</td>
</tr><tr>
<td>로컬 개발 환경</td>
<td align="left">file:///</td>
<td>지원</td>
<td>지원</td>
<td>지원</td>
<td>-</td>
</tr>
</tbody></table>

### 더 많은 FAQ
[TRTCCalling Web 관련 FAQ](https://intl.cloud.tencent.com/document/product/647/43096)를 참고하십시오.
