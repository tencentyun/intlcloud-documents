## 배경

비디오 콘텐츠의 보안을 보장하고 비디오의 무단 다운로드 및 배포를 방지하기 위해 Cloud Object Storage(COS) 데이터 처리는 비공개로 읽을 수 있는 파일보다 더 안전한 HLS 비디오 콘텐츠를 암호화하는 기능을 제공합니다. 암호화된 비디오는 재생 권한이 없는 사용자에게 배포할 수 없습니다. 다운로드하더라도 여전히 암호화되어 악의적으로 재배포할 수 없습니다. 이렇게 하면 비디오 저작권이 침해되는 것을 방지할 수 있습니다.

[HLS 암호화](https://intl.cloud.tencent.com/document/product/436/47861) 프로세스를 기반으로 기본 키 관리 서비스를 구축하고 [Tencent Cloud VOD superplayer](https://intl.cloud.tencent.com/document/product/266/33977) COS HLS에 의해 트랜스 코딩 및 암호화된 비디오 파일을 재생합니다.

## 실행 순서

#### 1단계: 비디오 암호화

[HLS 암호화로 비디오 유출 방지](https://intl.cloud.tencent.com/document/product/436/47861)의 안내에 따라 COS 버킷의 비디오 파일을 암호화합니다.

#### 2단계: 키 서비스 설정

1. [키 API](https://console.cloud.tencent.com/api/explorer?Product=kms&Version=2019-01-18&Action=Decrypt&SignVersion=)를 호출하여 프로그래밍 언어를 기반으로 KMS API 샘플 코드를 생성합니다.

2. 다음은 Node.js를 예로 들어 Koa로 샘플 코드를 기반으로 키 서비스를 구축하고 KMS API를 호출하여 복호화 키를 가져오는 방법을 설명합니다.
```
const Koa = require('koa')
const cors = require('koa2-cors')
const app = new Koa()
const tencentcloud = require("tencentcloud-sdk-nodejs")

app.use(cors()) // CORS 구성
app.use(async (ctx) => {
  // 생성된 m3u8 파일의 URI 요청은 기본적으로 매개변수 포함
  const { Ciphertext, KMSRegion } = ctx.query

  const KmsClient = tencentcloud.kms.v20190118.Client
  const clientConfig = {
    credential: {
      // https://console.cloud.tencent.com/cam/capi에서 얻을 수 있는 계정 API 키
      secretId: "SecretId",
      secretKey: "SecretKey",
    },
    
    region: KMSRegion, // "ap-guangzhou"와 같은 리전
    profile: {
      httpProfile: {
      	endpoint: "kms.tencentcloudapi.com",
      },
    },
  };

  // KMS 객체 인스턴스 생성
  const client = new KmsClient(clientConfig);
  const params = {
  	"CiphertextBlob": Ciphertext,
  };
  
	try {
    // 복호화 키 가져오기 요청 시작
    const res = await client.Decrypt(params)
    
    // Base64 복호화 후 키를 꺼내 이진법 데이터 반환
    const plaintext = res.Plaintext
    const plainBuff = Buffer.from(plaintext, 'base64');
    ctx.body = plainBuff
  } catch (error) {
    console.log(error);
  }
  
})

// 포트 8080 수신
app.listen('8080', () => {
  console.log('127.0.0.1:8080');
})
```

#### 3단계: Web에서 암호화된 비디오 재생

1. 플레이어 양식 및 스크립트 파일을 페이지로 가져옵니다.
```
<!--플레이어 양식 파일-->
<link href="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/tcplayer.min.css" rel="stylesheet"/>
<!--Chrome 및 Firefox와 같은 최신 브라우저에서 H5를 통해 HLS 비디오를 재생하려면 tcplayer.v4.2.2.min.js을 가져오기 전에 hls.min.0.13.2m.js를 가져와야 합니다.-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/libs/hls.min.0.13.2m.js"></script>
<!--플레이어 스크립트 파일-->
<script src="https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/tcplayer.v4.2.2.min.js"></script>
```
플레이어 SDK를 사용할 때 위의 정적 리소스를 직접 배포하는 것이 좋습니다. [플레이어 리소스를 다운로드하려면 여기 클릭](https://web.sdk.qcloud.com/player/tcplayer/release/v4.2.2/release.zip)하십시오.
압축 해제 후 생성된 폴더를 배포합니다. 폴더의 디렉터리를 조정하지 마십시오. 그렇지 않으면 리소스 가져오기 예외가 발생할 수 있습니다.
2. 플레이어 컨테이너 노드 설정
플레이어를 표시할 페이지에 플레이어 컨테이너를 추가합니다. 예를 들어 index.html에 다음 코드를 추가합니다(컨테이너 ID와 너비 및 높이를 사용자 지정할 수 있음).
```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```
>?
> - 플레이어 컨테이너는 `<video>` 태그여야 합니다.
> - 예시의 `player-container-id`는 사용자 정의할 수 있는 플레이어 컨테이너의 ID입니다.
> - CSS를 통해 플레이어 컨테이너 영역의 크기를 설정하는 것이 좋습니다. CSS는 속성보다 유연하고 전체 화면에 맞추기 및 컨테이너 적응과 같은 효과를 얻을 수 있습니다.
> - 예시의 `preload` 속성은 페이지가 로딩된 후 비디오 로딩 여부를 지정하며 일반적으로 재생을 더 빨리 시작하기 위해 `auto`로 설정됩니다. 다른 옵션에는 `meta`(페이지가 로딩된 후에만 메타데이터를 로딩함) 및 `none`(페이지가 로딩된 후 비디오를 로딩하지 않음)이 있습니다. 시스템 제한으로 인해 동영상은 모바일 장치에 자동으로 로딩되지 않습니다.
> - `playsinline` 및 `webkit-playsinline` 속성은 표준 모바일 브라우저가 비디오 재생을 가로채지 않을 때 인라인 재생을 구현하는 데 사용됩니다. 여기에서는 참고용일 뿐이며 필요에 따라 사용할 수 있습니다.
> - `x5-playsinline` 속성을 설정하면 TBS 커널에서 X5 UI 플레이어가 사용됩니다.
> 
3. 버킷 리스트 페이지에서 1단계에서 암호화된 영상의 **m3u8** 파일 객체 주소를 가져옵니다.

4. 플레이어를 초기화하고 m3u8 객체 주소를 전달합니다.
```
var player = TCPlayer('player-container-id', {}); // player-container-id는 플레이어 컨테이너 ID로 html 상의 것과 일치해야 함
player.src(https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/path/example.m3u8); // m3u8 객체 주소
```

#### 4단계: 효과 보기

1. m3u8 파일과 암호 복호화 키를 성공적으로 획득했습니다.

2. 비디오가 복호화되고 성공적으로 재생됩니다.




