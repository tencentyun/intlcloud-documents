본문은 Node.js를 사용한 간단하고 일반적인 고객 서비스 시나리오 Demo 개발을 예시로, WeChat 구독 계정에 Tencent Cloud IM을 통합하는 기본 프로세스를 소개합니다.
>? 예시는 참고용이며 정식 출시 전에 서버 로드 밸런싱, 인터페이스 동시성 제어, 정보 영속화 저장 등 추가 개선이 필요합니다. 이러한 최적화 작업은 본문 내용에 포함되어있지 않습니다. 개발자들은 실제 상황에 따라 자체적인 개선 작업을 진행하시기 바랍니다.

## 시나리오 흐름도 및 효과
본문에 설명된 Demo 시나리오의 기본 프로세스는 다음과 같습니다.
1. 고객이 의류 이커머스 구독 계정을 통해 "아동복 신상품은 언제쯤 나오나요?"라고 문의함.
2. 고객의 문의 메시지는 Tencent Cloud IM 시스템을 통해 해당 의류 회사의 고객서비스 상담원에게 전송됨.
3. 고객서비스 직원의 답변 메시지 "5월에 출시될 예정이오니, 많은 관심 부탁드립니다!"는 Tencent Cloud IM 시스템과 WeChat을 통해 고객에게 푸시됨.

고객측에 나타나는 효과:
![](https://main.qcloudimg.com/raw/4e6c7a4dc41c2691c40cdb448b69c78d.png)
고객서비스 상담원측에 나타나는 효과:
![](https://main.qcloudimg.com/raw/f2798df649830b2deca22a7449c7eb97.png)
시나리오 흐름도:
![](https://main.qcloudimg.com/raw/086439320c042ba4f03322b825ec38d1.jpg)

## 주의 사항
- 메시지 전송 링크가 길면 메시지 송수신에 시간이 많이 소요될 수 있습니다.
- 개인이 등록한 구독 계정은 WeChat 공식 계정 플랫폼의 [고객 서비스 메시지] API를 사용하여 구독자에게 메시지를 푸시할 수 없습니다.

## 전제 조건

- Node.js를 실행할 수 있는 공용 네트워크 개발 서버 또는 CVM을 준비합니다.
- WeChat 구독 계정 또는 서비스 계정을 [등록](https://mp.weixin.qq.com/cgi-bin/registermidpage?action=index&lang=zh_CN&token=)합니다.
- [WeChat 공식 계정 플랫폼 개발 문서](https://developers.weixin.qq.com/doc/offiaccount/Basic_Information/Access_Overview.html)를 자세히 읽습니다.
- [IM 애플리케이션 생성](https://intl.cloud.tencent.com/document/product/1047/34577)을 완료합니다.
- IM 사용자 계정을 [단일 계정 가져오기](https://intl.cloud.tencent.com/document/product/1047/34953) 또는 [여러 계정 가져오기](https://intl.cloud.tencent.com/document/product/1047/34954) 합니다.(예: user0 및 user1).

## 참고 문서

- [REST API 소개](https://intl.cloud.tencent.com/document/product/1047/34620)
- [서드 파티 콜백 소개](https://intl.cloud.tencent.com/document/product/1047/34354)
- [WeChat 공식 계정 플랫폼 개발 개요](https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Overview.html)
- [Express 프레임워크 튜토리얼](https://expressjs.com/zh-cn/)

## 작업 절차

### 1단계: 개발 프로젝트 생성 및 종속성 설치

```javascript
npm init -y

// express 프레임워크
npm i express@latest --save 

// 암호화 모듈
npm i crypto@latest --save

// xml 파서
npm i xml2js@latest --save

// http 요청 발송
npm i axios@latest --save

// userSig 계산
npm i tls-sig-api-v2@latest --save
```

### 2단계: IM 애플리케이션 정보 입력 및 UserSig 계산

<pre><code><span class="hljs-comment">// ------------ IM ------------</span>
<span class="hljs-keyword">const</span> IMAxios = axios.create({
  <span class="hljs-attr">timeout</span>: <span class="hljs-number">10000</span>,
  <span class="hljs-attr">headers</span>: {
    <span class="hljs-string">'Content-Type'</span>: <span class="hljs-string">'application/x-www-form-urlencoded;charset=UTF-8'</span>,
  },
});

<span class="hljs-comment">// IM 계정 시스템 사용자 ID 매핑 테이블 가져오기 완료, 비영속화 저장. 빠른 Demo 검색에만 사용. 프로덕션 환경에는 다른 기술 솔루션을 사용하십시오.</span>
<span class="hljs-keyword">const</span> importedAccountMap = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Map</span>();
<span class="hljs-comment">// IM 애플리케이션 및 App 관리자 정보. <a href="https://console.cloud.tencent.com/im">IM 콘솔</a>에 로그인하여 가져오기 하십시오.</span>
<span class="hljs-keyword">const</span> SDKAppID = <span class="hljs-number">0</span>; <span class="hljs-comment">// IM 애플리케이션의 SDKAppID 입력</span>
<span class="hljs-keyword">const</span> secrectKey = <span class="hljs-string">''</span>; <span class="hljs-comment">// IM 애플리케이션 키 입력</span>
<span class="hljs-keyword">const</span> AppAdmin = <span class="hljs-string">'user0'</span>; <span class="hljs-comment">// user0을 App 관리자 계정으로 설정</span>
<span class="hljs-keyword">const</span> kfAccount1 = <span class="hljs-string">'user1'</span>; <span class="hljs-comment">// user1을 고객 서비스 상담원 계정으로 설정</span>
<span class="hljs-comment">// UserSig 계산. REST API 호출 시 사용. 자세한 작업은  <a href="https://github.com/tencentyun/tls-sig-api-v2-node">Github를 참고하십시오.</a></span>
<span class="hljs-keyword">const</span> api = <span class="hljs-keyword">new</span> TLSSigAPIv2.Api(SDKAppID, secrectKey);
<span class="hljs-keyword">const</span> userSig = api.genSig(AppAdmin, <span class="hljs-number">86400</span>*<span class="hljs-number">180</span>);
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'userSig:'</span>, userSig);</code></pre>

### 3단계: URL 및 Token 설정
>? 본문은 WeChat 공식 계정 플랫폼 개발 가이드를 참고하여 작성되었으며, 변경 사항이 있을 경우 [액세스 가이드](https://mp.weixin.qq.com/wiki)를 참고하시기 바랍니다.

1. 구독 계정 관리 백엔드에 로그인합니다.
2. [기본 설정]을 선택하고 프로토콜을 클릭하여 개발자가 됩니다.
3. [설정 변경]을 클릭하고 관련 정보를 입력합니다.
 -URL: 서버 주소. WeChat 메시지 및 이벤트 수신을 위한 인터페이스 URL. 필수 입력 매개변수.
 -Token : 임의로 입력할 수 있으며, 서명 생성에 사용됨. 해당 Token은 인터페이스 URL에 포함된 Token과 비교하여 보안성을 검증합니다. 필수 입력 매개변수.
 -EncodingAESKey: 수동으로 입력하거나 임의로 생성. 메시지 본문 암호화/복호화에 사용. 선택 입력 매개 변수.

### 4단계: Web 서비스 수신 포트를 실행하고 WeChat에서 보낸 Token 인증에 올바르게 응답

<pre><code><span class="hljs-keyword">const</span> express = <span class="hljs-keyword">require</span>(<span class="hljs-string">'express'</span>); <span class="hljs-comment">// express 프레임워크 </span>
<span class="hljs-keyword">const</span> crypto =  <span class="hljs-keyword">require</span>(<span class="hljs-string">'crypto'</span>); <span class="hljs-comment">// 암호화 모듈</span>
<span class="hljs-keyword">const</span> util = <span class="hljs-keyword">require</span>(<span class="hljs-string">'util'</span>);
<span class="hljs-keyword">const</span> xml2js = <span class="hljs-keyword">require</span>(<span class="hljs-string">'xml2js'</span>); <span class="hljs-comment">// xml 파서</span>
<span class="hljs-keyword">const</span> axios = <span class="hljs-keyword">require</span>(<span class="hljs-string">'axios'</span>); <span class="hljs-comment">// http 요청 발송</span>
<span class="hljs-keyword">const</span> TLSSigAPIv2 = <span class="hljs-keyword">require</span>(<span class="hljs-string">'tls-sig-api-v2'</span>); <span class="hljs-comment">// userSig 계산</span>

<span class="hljs-comment">// ------------ Web 서비스 ------------</span>
<span class="hljs-keyword">var</span> app = express();
<span class="hljs-comment">// Token은 [구독 계정 관리 백엔드]&gt;[기본 설정]에서 설정</span>

<span class="hljs-comment">// 포트 80에 진입하는 모든 get 요청 처리</span>
app.get(<span class="hljs-string">'/'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(req, res)</span> </span>{
  <span class="hljs-comment">// ------------ WeChat 공식 계정 플랫폼 액세스 ------------</span>
  <span class="hljs-comment">// 자세한 내용은 <a href="https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Overview.html">WeChat 공식 문서를 참고하십시오.</a> </span>
  <span class="hljs-comment">// WeChat 서버의 Get 요청 매개변수 signature, timestamp, nonce, echostr 가져오기</span>
  <span class="hljs-keyword">var</span> signature = req.query.signature; <span class="hljs-comment">// WeChat 암호화 서명</span>
  <span class="hljs-keyword">var</span> timestamp = req.query.timestamp; <span class="hljs-comment">// 타임스탬프</span>
  <span class="hljs-keyword">var</span> nonce = req.query.nonce; <span class="hljs-comment">// 랜덤 숫자</span>
  <span class="hljs-keyword">var</span> echostr = req.query.echostr; <span class="hljs-comment">// 랜덤 문자열</span>

  <span class="hljs-comment">// token, timestamp, nonce 3개 매개변수를 사전식 순서로 정렬</span>
  <span class="hljs-keyword">var</span> <span class="hljs-keyword">array</span> = [myToken, timestamp, nonce];
  <span class="hljs-keyword">array</span>.sort();

  <span class="hljs-comment">//  3개의 매개변수 문자열을 하나의 문자열로 연결하여 sha1 암호화 진행</span>
  <span class="hljs-keyword">var</span> tempStr = <span class="hljs-keyword">array</span>.join(<span class="hljs-string">''</span>);
  <span class="hljs-keyword">const</span> hashCode = crypto.createHash(<span class="hljs-string">'sha1'</span>); <span class="hljs-comment">// 암호화 유형 생성 </span>
  <span class="hljs-keyword">var</span> resultCode = hashCode.update(tempStr,<span class="hljs-string">'utf8'</span>).digest(<span class="hljs-string">'hex'</span>); <span class="hljs-comment">// 전달된 문자열 암호화 진행</span>

  <span class="hljs-comment">// 암호화된 문자열을 얻은 후, 개발자는 이를 서명과 비교하고, 해당 요청이 WeChat에서 온 것임을 표시</span>
  <span class="hljs-keyword">if</span> (resultCode === signature) {
    res.send(echostr);
  } <span class="hljs-keyword">else</span> {
    res.send(<span class="hljs-string">'404 not found'</span>);
  }
});

<span class="hljs-comment">// 80포트 수신</span>
app.listen(<span class="hljs-number">80</span>);</code></pre>

### 5단계: 개발자 서버측 비즈니스 로직 구현

- WeChat이 푸시한 팔로우 이벤트 수신 시, [단일 계정 가져오기](https://intl.cloud.tencent.com/document/product/1047/34953) 또는 [여러 계정 가져오기](https://intl.cloud.tencent.com/document/product/1047/34954) API를 호출하여 계정 시스템으로 계정을 가져옵니다.
- WeChat이 푸시한 팔로우 이벤트 수신 시, 메시지에 수동적으로 응답합니다.
- WeChat이 푸시한 언팔로우 이벤트 수신 시, [계정 삭제](https://intl.cloud.tencent.com/document/product/1047/34955) API를 호출하여 계정 시스템에서 계정을 삭제합니다.
- WeChat이 푸시한 일반 이벤트 수신 시 [1:1 채팅 메시지 발송](https://intl.cloud.tencent.com/document/product/1047/34919) API를 호출하여 고객서비스 계정에 1:1 채팅 메시지를 발송합니다.

```javascript
const genRandom = function() {
  return  Math.floor(Math.random() * 10000000);
}

// wx 텍스트 응답 xml 생성
const genWxTextReplyXML = function(to, from, content) {
  let xmlContent = '<xml><ToUserName><![CDATA[' + to + ']]></ToUserName>'
  xmlContent += '<FromUserName><![CDATA[' + from + ']]></FromUserName>'
  xmlContent += '<CreateTime>' + new Date().getTime() + '</CreateTime>'
  xmlContent += '<MsgType><![CDATA[text]]></MsgType>'
  xmlContent += '<Content><![CDATA[' + content + ']]></Content></xml>';

  return xmlContent;
}

/**
 * IM 계정 시스템에 사용자 가져오기
 * @param {String} userID 가져오기할 사용자 ID
 */
const importAccount = function(userID) {
  console.log('importAccount:', userID);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/im_open_login_svc/account_import?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('importAccount url:', url);
    IMAxios({
      url: url,
      data: {
        "Identifier": userID
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('importAccount ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('importAccount failed.', error);
      reject(error);
    })
  });
}

/**
 * IM 계정 시스템에서 사용자 삭제
 * @param {String} userID 삭제할 사용자 ID
 */
const deleteAccount = function(userID) {
  console.log('deleteAccount', userID);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/im_open_login_svc/account_delete?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('deleteAccount url:', url);
    IMAxios({
      url: url,
      data: {
        "DeleteItem": [
          {
            "UserID": userID,
          },
        ]
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('deleteAccount ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('deleteAccount failed.', error);
      reject(error);
    })
  });
}

/**
 * 1:1 채팅 메시지 발송
 */
const sendC2CTextMessage = function(userID, content) {
  console.log('sendC2CTextMessage:', userID, content);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/openim/sendmsg?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('sendC2CTextMessage url:', url);
    IMAxios({
      url: url,
      data: {
        "SyncOtherMachine": 2, // 메시지는 발신자측에 동기화되지 않습니다. 메시지를 From_Account에 동기화하려면 SyncOtherMachine에 1을 입력합니다.
        "To_Account": userID,
        "MsgLifeTime":60, // 메시지 60초 동안 저장
        "MsgRandom": 1287657,
        "MsgTimeStamp": Math.floor(Date.now() / 1000), // 단위: 초. 정수이어야 함.
        "MsgBody": [
          {
            "MsgType": "TIMTextElem",
            "MsgContent": {
              "Text": content
            }
          }
        ]
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('sendC2CTextMessage ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('sendC2CTextMessage failed.', error);
      reject(error);
    });
  });
}

// WeChat의 post 요청 처리
app.post('/', function(req, res) {
  var buffer = [];
  // data 이벤트 수신. 데이터 수신에 사용.
  req.on('data', function(data) {
    buffer.push(data);
  });
  // end 이벤트 수신. 수신 완료된 데이터 처리에 사용.
  req.on('end', function() {
    const tmpStr = Buffer.concat(buffer).toString('utf-8');
    xml2js.parseString(tmpStr, { explicitArray: false }, function(err, result) {
      if (err) {
        console.log(err);
        res.send("success");
      } else {
        if (!result) {
          res.send("success");
          return;
        }
        console.log('wx post data:', result.xml);
        var wxXMLData = result.xml;
        var toUser = wxXMLData.ToUserName; // 수신자측 WeChat
        var fromUser = wxXMLData.FromUserName;// 발신자측 WeChat
        if (wxXMLData.Event) {  // 이벤트 유형 처리
          switch (wxXMLData.Event) {
            case "subscribe": // 구독 계정 팔로우
              res.send(genWxTextReplyXML(fromUser, toUser, '팔로우해주셔서 감사합니다. XX는 언제나 최선을 다해 최고의 서비스를 제공합니다!''));
              importAccount(fromUser).then(() => {
                // 가져오기한 사용자 ID를 기록합니다.
                importedAccountMap.set(fromUser, 1);
              });
              break;
            case "unsubscribe": // 팔로우 취소
              deleteAccount(fromUser).then(() => {
                importedAccountMap.delete(fromUser);
              });
              res.send("success");
              break;
          }
        } else { // 메시지 유형 처리
          switch (wxXMLData.MsgType) {
            case "text":
              // 텍스트 메시지 처리
              sendC2CTextMessage(kfAccount1, 'WeChat 구독 계정에서 온 문의:' + wxXMLData.Content).then(() => {
                console.log('C2C 메시지 발송 성공');
              }).catch((error) => {
                console.log('C2C 메시지 발송 실패');
              });
              break;
            case "image":
              // 이미지 메시지 처리
              break;
            case "voice":
              // 음성 메시지 처리
              break;
            case "video":
              // 영상 메시지 처리
              break;
            case "shortvideo":
              // 쇼트 비디오 메시지 처리
              break;
            case "location":
              // 지리적 위치 발송 처리
              break;
            case "link":
              // 링크 메시지 처리
              break;
            default:
              break;  
          }
          res.send(genWxTextReplyXML(fromUser, toUser, '고객 서비스 상담원에게 연결하는 중입니다. 잠시만 기다려 주십시오.'));
        }
      }
    })
  });
});
```

### 6단계: IM 서드 파티 콜백 등록 및 처리

<pre><code><span class="hljs-comment">// IM 서드 파티에서 호출한 post 요청 처리</span>
app.post(<span class="hljs-string">'/imcallback'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">req, res</span>) </span>{
  <span class="hljs-keyword">var</span> buffer = [];
  <span class="hljs-comment">// data 이벤트 수신. 데이터 수신에 사용.</span>
  req.on(<span class="hljs-string">'data'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">data</span>) </span>{
    buffer.push(data);
  });
  <span class="hljs-comment">// end 이벤트 수신. 수신된 데이터 처리에 사용</span>
  req.on(<span class="hljs-string">'end'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-keyword">const</span> tmpStr = Buffer.concat(buffer).toString(<span class="hljs-string">'utf-8'</span>);
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'imcallback'</span>, tmpStr);
    <span class="hljs-keyword">const</span> imData = <span class="hljs-built_in">JSON</span>.parse(tmpStr);
    <span class="hljs-comment">// kfAccount1가 발송한 메시지를 고객에 푸시</span>
    <span class="hljs-keyword">if</span> (imData.From_Account === kfAccount1) {
      <span class="hljs-comment">// 메시지를 패키징하여 WeChat의 [고객서비스 메시지] API를 통해 지정된 사용자에게 푸시</span>
      <span class="hljs-comment">// 참고: 개인이 등록한 구독 계정은 이 API를 사용할 수 없습니다. 자세한 내용은 <a href="https://developers.weixin.qq.com/doc/offiaccount/Message_Management/Service_Center_messages.html">고객서비스 메시지를 참고하십시오.</a></span>
    }

    res.send({
      <span class="hljs-string">"ActionStatus"</span>: <span class="hljs-string">"OK"</span>,
      <span class="hljs-string">"ErrorInfo"</span>: <span class="hljs-string">""</span>,
      <span class="hljs-string">"ErrorCode"</span>: <span class="hljs-number">0</span> <span class="hljs-comment">// 0: 발언 허용. 1: 발언 금지</span>
    });
  });
});</code></pre>

