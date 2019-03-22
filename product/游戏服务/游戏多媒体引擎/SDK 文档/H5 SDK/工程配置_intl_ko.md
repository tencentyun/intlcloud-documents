H5 개발자가 Tencent Cloud GME 제품 API를 디버깅하고 연결하는 데 도움이 되도록 여기에 H5 개발에 적합한 준비 작업을 소개합니다.

##  H5 SDK에서 지원되는 플랫폼
<table>
   <tr>
      <td>운영 체제</td>
      <td>브라우저/webview</td>
      <td>버전 요구 사항</td>
      <td>비고</td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>Safari</td>
      <td>11.1.2</td>
      <td>Apple Safari에는 가끔 버그가 있기 때문에 Apple이 해결할 때까지 제품화 계획을 포기하고 기다리는 것이 좋습니다.</td>
   </tr>
   <tr>
      <td rowspan="2">Android</td>
      <td>TBS(Wechat 및 Mobile QQ의 기본 Webview)</td>
      <td>43600</td>
      <td>WeChat 및 Mobile QQ가 내장된 기본 브라우저 커널은 <a href="https://x5.tencent.com/">TBS </a>입니다.</td>
   </tr>
   <tr>
      <td>Chrome</td>
      <td>60+</td>
      <td>H264를 지원해야 함.</td>
   </tr>
   <tr>
      <td rowspan="2">Mac</td>
      <td>Chrome</td>
      <td>47+</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Safari</td>
      <td>11+</td>
      <td>-</td>
   </tr>
   <tr>
      <td rowspan="2">Windows(PC)</td>
      <td>Chrome</td>
      <td>52+</td>
      <td>-</td>
   </tr>
   <tr>
      <td><a href="https://browser.qq.com/">QQ 브라우저</a></td>
      <td>10.2</td>
      <td>-</td>
   </tr>
</table>

## SDK 준비
다음의 방식으로 SDK를 획득할 수 있습니다.
1. [다운로드 가이드](https://cloud.tencent.com/document/product/607/18521)를 참조하고 관련 Sample Code 및 SDK를 다운로드하십시오.
2. 인터페이스에서 H5 버전의 SDK 리소스를 찾습니다.
3. 페이지에서 [다운로드]를 클릭하여 작업을 완료합니다.


## 예비 작업
### 1. 포트 개방
네트워크에 방화벽이 있는 경우 다음 포트가 열려 있는지 확인하십시오.

| 프로토콜 | 포트 번호            |
| ---- | ----------------- |
| TCP  | 8687              |
| UDP  | 8000, 8800, 443 |

CDN을 사용하여 SDK를 가져옵니다.

###  2. WebRTCAPI.min.js 가져오기

```
html
<script src="https://sqimg.qq.com/expert_qq/webrtc/3.0/WebRTCAPI.min.js"></script>
```

### 3. H5 인증 설정
### 프로그램 다운로드
당사가 준비한 authBuffer 예시 프로그램을 [다운로드](https://main.qcloudimg.com/raw/b1d8e4d8e7321fd67250069d07bf2016.zip)하십시오. 이 프로그램은 지정된 sdkappid의 인증 정보에 서명할 수 있습니다.

### 관련 수정
signdemo 디렉터리로 이동하여 config.js 파일을 수정합니다. config.js 파일을 열고 기본 구성을 삭제한 다음 코드가 삭제된 위치에서 appidMap 함수를 호출합니다. 매개변수는 Tencent Cloud 백 엔드에서 신청된 SDKAppID와 해당 인증 키입니다.

```
const AuthBufferConfig = function () {
    this.appidMap = {};
    this.appidMap["1400089356"] = "1cfbfd2a1a03a53e";
};
//1400089356을 Tencent Cloud 백 엔드에서 신청된 sdkAppID로 변경하고 1cfbfd2a1a03a53e를 해당 sdkAppID의 인증 key로 변경합니다.
```

>!  AuthKey는 반드시 사용자 sdkAppID에 해당해야 합니다.

#### npm 패키지 설치 및 실행
authBuffer 예시 프로그램 디렉터리로 이동하여 다음 이구를 실행하고 관련 종속성을 설치하십시오.

```
npm i
```

그 다음에 스크립트 node index.js를 실행하고 서명 서비스를 실행하십시오.

>!async 구문을 사용하므로 node 버전이 8 이상인지 확인하십시오. 명령행에서 node -v를 실행하여 버전을 확인하십시오.


#### 테스트
명령행에서 다음 명령을 사용하여 테스트할 수 있습니다(시스템에 curl 명령어가 있는지 확인하십시오).

```
//userSig 생성:
curl "http://127.0.0.1:10005/" --data "sdkappid=1400089356&roomid=1234123&openid=1234567"
```

#### 참조로 돌아가기

```
{"userSig":"AqhHE7QHLFYPfV/zfyrdRYHfuUn6eOA8g/J6GMjVy//Shr5ByJPTi8hzR2KyXMvn","errorCode":0}
```
