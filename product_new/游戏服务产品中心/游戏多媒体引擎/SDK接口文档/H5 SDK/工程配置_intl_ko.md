H5 개발자가 원활히 테스트하고 Tencent Cloud Game Multimedia Engine(GME) API를 액세스하는데 도움을 드리고자, 하기 H5 개발자의 준비 작업에 대해 안내드립니다.

## H5 SDK 지원 플랫폼
<table>
   <tr>
      <td>조작시스템 플랫폼</td>
      <td>브라우저/웹뷰</td>
      <td>버전 사양</td>
      <td>비고</td>
   </tr>
   <tr>
      <td>iOS</td>
      <td>Safari</td>
      <td>11.1.2</td>
      <td>애플 Safari에 종종 버그가 나타나므로, 제품화한 방안을 제외해주시고, 애플측에서 관련 상황을 해결하면 다시 사용하시기를 추천드립니다.
   </tr>
   <tr>
      <td rowspan="2">Android</td>
      <td>TBS(위챗, 모바일QQ 기본 웹 뷰)</td>
      <td>43600</td>
      <td>위챗과 모바일QQ에 기본적으로 내장된 브라우저 커널 <a href="https://x5.tencent.com/">TBS</a></td>
   </tr>
   <tr>
      <td>Chrome</td>
      <td>60+</td>
      <td>H264 지원이 필요합니다</td>
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
      <td>-</td>
      <td>-</td>
   </tr>
   <tr>
      <td><a href="https://browser.qq.com/">QQ 브라우저</a></td>
      <td>10.2</td>
      <td>-</td>
   </tr>
</table>

## SDK 준비
다음 프로세스를 통해 SDK를 획득할 수 있습니다
1. [다운로드 매뉴얼](https://intl.cloud.tencent.com/document/product/607/18521)웹 페이지에 접속합니다.
2. 인터페이스에서 H5 버전용 SDK 리소스를 확인합니다.
3. 웹 페이지에서 [다운로드]를 클릭하여 조작을 완료합니다.


## 사전 준비 작업
### 1. 포트 번호 오픈
혹 이용하시는 네트워크에 방화벽이 설치되었다면, 다음 포트를 오픈하세요: 

| 프로토콜 | 포트 번호            |
| ---- | ----------------- |
| TCP  | 8687              |
| UDP  | 8000, 8800, 443 |

CDN을 사용하여 SDK를 추가합니다.

### 2. WebRTCAPI.min.js 인용

```
html
<script src="https://sqimg.qq.com/expert_qq/webrtc/3.0/WebRTCAPI.min.js"></script>
```

###  3. H5 인증 설정
#### 다운로드 프로그램
authBuffer 예시 프로그램을 [다운로드](https://main.qcloudimg.com/raw/b1d8e4d8e7321fd67250069d07bf2016.zip)하세요. 이 프로그램은 지정 sdkappid의 인증 메시지에 사인할 수 있습니다.

#### 수정 사항
signdemo 목록에 접속하여 config.js 파일을 수정합니다. config.js 파일을 오픈하여 기본 설정을 삭제하며, 코드를 삭제한 곳에서 appidMap 함수를 호출합니다. 파라미터는 Tencent Cloud 백그라운드에서 신청한 SDKAppid와 대응하는 인증키입니다.

```
const AuthBufferConfig = function () {
    this.appidMap = {};
    this.appidMap["1400089356"] = "1cfbfd2a1a03a53e";
};
//1400089356을 Tencent Cloud 백그라운드에서 신청한 sdkAppid로 변경합니다. 1cfbfd2a1a03a53e는 대응하는 sdkAppid의 인증키로 변경합니다.
```

>AuthKey는 sdkAppid와 매칭해야 합니다.

#### npm 패킷 설치, 작동
uthBuffer 예시 프로그램 목록에 접속하여 다음 문구를 실행 및 관련 의존을 설치합니다.

```
npm i
```

다음으로 node index.js 스크립트를 실행하고 사인 서비스를 적용합니다.

>async 문법을 사용하므로 node 버전은 8 이상으로 적용하십시오. 버전을 조회하려면 커맨드행에서 node -v를 실행하십시오.


#### 테스트
커맨드행에서 다음 커맨드로 테스트할 수 있습니다(시스템에 cur1 명령이 포함되었음을 확인합니다): 

```
//userSig 생성: 
curl "http://127.0.0.1:10005/" --data "sdkappid=1400089356&roomid=1234123&openid=1234567"
```

#### 리턴 참고
시그니처 프로그램을 실행하면 시그니처 프로그램은 인증 메시지를 리턴하며, 다음과 같이 리턴 참고합니다.

```
{"userSig":"AqhHE7QHLFYPfV/zfyrdRYHfuUn6eOA8g/J6GMjVy//Shr5ByJPTi8hzR2KyXMvn","errorCode":0}
```
