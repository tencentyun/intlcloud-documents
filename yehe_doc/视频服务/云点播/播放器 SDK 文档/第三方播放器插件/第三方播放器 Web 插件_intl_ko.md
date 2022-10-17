본문에서는 타사 Player Web 플러그인에 대해 설명합니다. 이 플러그인은 비디오 재생을 구현하기 위해 유연한 API를 통해 타사 Player를 VOD 기능과 빠르게 통합하는 데 도움이 됩니다. 기본 비디오 정보, 비디오 스트림 정보, 키프레임 및 썸네일 정보 획득과 독점 암호화를 지원합니다. 이 문서는 Javascript에 대한 기본 지식이 있는 개발자를 대상으로 합니다.



## SDK 통합

타사 Player Web 플러그인은 **CDN 통합** 및 **npm 통합** 두 가지 통합 방식을 제공합니다.

#### CDN 통합

비디오를 재생해야 하는 페이지로 초기화 스크립트를 가져옵니다. 스크립트는 TcAdapter 변수를 전역적으로 노출합니다.

```javascript
<script src="https://cloudcache.tencentcs.com/qcloud/video/dist/tcadapter.1.0.0.min.js"></script>
```

#### npm 통합

```javascript
// npm install
npm install tcadapter --save

// import TcAdapter
import TcAdapter from 'tcadapter';
```



## 플레이어 컨테이너 배치

플레이어를 표시해야 하는 페이지에 컨테이너를 추가합니다. TcAdapter는 비디오 재생을 위한 컨테이너만 운반하면 됩니다. 재생 스타일 및 사용자 정의 기능은 타사 플레이어 또는 사용자 자체 구현 가능합니다:

```javascript
<video id="player-container-id">
</video>
```

## SDK 사용 설명

### 개발 환경 점검

현재 환경에서 TcAdapter 지원 여부를 확인합니다.

```javascript
TcAdapter.isSupported();
```

### Adapter 초기화

Adapter를 초기화하고 Adapter 인스턴스를 생성합니다. 초기화 프로세스는 Tencent Cloud VOD 서버에서 비디오 파일 정보를 요청합니다.

**API**

```javascript
const adapter = new TcAdapter('player-container-id', {
  fileID: string,
  appID: string,
  psign: string,
  hlsConfig: {}
}, callback);
```

**매개변수 설명**

| 매개변수    | 유형                  | 설명                                             |
| --------- | --------------------- | ------------------------------------------------ |
| appID     | String                | VOD 계정의 APPID                                 |
| fileID    | String                | 재생할 비디오의 fileId                               |
| psign     | String                | Player 서명                                   |
| hlsConfig | HlsConfig             | HLS설정. `hls.js`에서 지원하는 모든 매개변수를 사용할 수 있습니다.          |
| callback  | TcAdapterCallBack | 초기화 완료를 위한 콜백. 이를 통해 기본 비디오 정보를 얻을 수 있습니다. |

> ! TcAdapter의 기본 계층은 `hls.js`를 기반으로 구현되며 미세 조정 재생을 위해 HlsConfig를 통해 `hls.js`에서 지원하는 모든 매개변수를 수신할 수 있습니다.

### 기본 비디오 정보 얻기

이 API는 비디오 정보를 가져오는 데 사용되며 초기화 후에만 적용됩니다.

**API**

```javascript
VideoBasicInfo adapter.getVideoBasicInfo();
```

**매개변수 설명**

VideoBasicInfo의 매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 설명               |
| ----------- | ------ | ------------------ |
| name        | String | 비디오 이름             |
| duration    | Float  | 비디오 길이(초)   |
| description | String | 비디오 설명             |
| coverUrl    | String | 비디오 썸네일             |

### 비디오 스트림 정보 가져오기

**API**

```javascript
List<StreamingOutput> adapter.getStreamimgOutputList();
```

**매개변수 설명**

StreamingOutput 매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 설명                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| drmType    | String | 어댑티브 비트스트림 보호 유형, 유효 값: plain(암호화 없음), simpleAES(HLS 공통 암호화) |
| playUrl    | String | 재생 URL                                                     |
| subStreams | List   | [SubStreamInfo](#SubStreamInfo) 유형의 어댑티브 비트스트림 서브스트림 정보 |

SubStreamInfo 의 매개변수는 다음과 같습니다: [](id:SubStreamInfo)

| 매개변수         | 유형   | 설명                                 |
| -------------- | ------ | ------------------------------------ |
| type           | String | 서브스트림 유형. 유효 값: video |
| width          | Int    | 서브스트림 비디오 너비(px)               |
| height         | Int    | 서브스트림 비디오 높이(px)               |
| resolutionName | String | 플레이어에 표시되는 서브스트림 비디오 사양 이름       |

### 키 프레임 타임스탬프 정보 가져오기

**API**

```java
List<KeyFrameDescInfo> adapter.getKeyFrameDescInfo();
```

**매개변수 설명**

KeyFrameDescInfo의 매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 설명          |
| ---------- | ------ | ------------- |
| timeOffset | Float  | 1.1           |
| content    | String | ‘지금 시작...’ |

### 썸네일 정보 가져오기

**API**

```javascript
ImageSpriteInfo adapter.getImageSpriteInfo();
```

**매개변수 설명**

ImageSpriteInfo의 매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 설명                               |
| --------- | ------ | ---------------------------------- |
| imageUrls | List   | String 유형의 썸네일 다운로드 URL 배열 |
| webVttUrl | String | 썸네일 VTT 파일 다운로드 URL            |

### 이벤트 수신

플레이어는 초기화에서 반환된 객체를 통해 이벤트 수신을 수행할 수 있습니다. 예를 들면 다음과 같습니다.

```javascript
const adapter = TcAdapter('player-container-id', options);
adapter.on(TcAdapter.TcAdapterEvents.Error, function(error) {
  // do something
});
```

여기서 type은 이벤트 유형입니다. 지원되는 이벤트에는 HLS의 기본 이벤트와 다음 이벤트가 포함됩니다. 이벤트 이름은 `TcAdapter.TcAdapterEvents`에서 액세스할 수 있습니다.

| 이름           | 설명                                                         |
| :------------- | :----------------------------------------------------------- |
| LOADEDMETADATA | 해당 영상 정보는 playcgi를 통해 얻은 것이며, 이 이벤트 콜백을 통해 관련 영상 정보를 얻을 수 있습니다. |
| HLSREADY       | hls 인스턴스가 생성되었습니다. 이 시점에서 hls 인스턴스 객체의 다양한 속성과 메소드를 호출할 수 있습니다 |
| ERROR | 이 이벤트는 오류가 발생하면 트리거됩니다. 콜백 매개변수에 따라 특정 실패 원인을 볼 수 있습니다. |


### Hls 인스턴스 가져오기
adapter의 기본 계층은 hls.js를 기반으로 구현됩니다. adapter 인스턴스를 통해 HLS 인스턴스와 해당 속성 및 메소드에 액세스하여 재생 프로세스를 미세하게 제어할 수 있습니다.

```javascript
adapter.on('hlsready', () => {
  const hls = adapter.hls;
  // ...
})
```

> ? 자세한 내용은 [hls.js](https://github.com/video-dev/hls.js/)를 참고하십시오.



## 예시

### 예1: React에서 TcAdapter 사용 

자세한 예시는 [GitHub](https://github.com/tcplayer/tcadapter-combine-video)을 참고하십시오.

```javascript
import { useEffect, useRef } from 'react';
import TcAdapter from 'tcadapter';

function App() {
  if (!TcAdapter.isSupported()) {
    throw new Error('current environment can not support TcAdapter');
  }

  const videoRef = useRef(null);
  useEffect(() => {
    const adapter = new TcAdapter(videoRef.current, {
      appID: '1500002611',
      fileID: '5285890813738446783',
      psign: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAwMjYxMSwiZmlsZUlkIjoiNTI4NTg5MDgxMzczODQ0Njc4MyIsImN1cnJlbnRUaW1lU3RhbXAiOjE2MTU5NTEyMzksImV4cGlyZVRpbWVTdGFtcCI6MjIxNTY1MzYyMywicGNmZyI6ImJhc2ljRHJtUHJlc2V0IiwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiMjIxNTY1MzYyMyJ9fQ.hRrQYvC0UYtcO-ozB35k7LZI6E3ruvow7DC0XzzdYKE',
      hlsConfig: {},
    }, () => {
      console.log('basicInfo', adapter.getVideoBasicInfo());
    });

    adapter.on(TcAdapter.TcAdapterEvents.HLSREADY, () => {
      const hls = adapter.hls;
			// ...
    })
  }, []);
  

  const play = () => {
    videoRef.current.play();
  }

  return (
    <div>	
      <div>
        <video id="player" ref={ videoRef }></video>
      </div>
      <button onClick={play}>play</button>
    </div>
  );
}

export default App;

```

### 예2: TcAdapter와 videojs 결합

자세한 예시는 [GitHub](https://github.com/tcplayer/tcadapter-combine-videojs)을 참고하십시오.

```javascript
// 1. hls를 통한 videojs 재생은 @videojs/http-streaming을 사용하므로 tcadapter로 재생하기 위한 정책 세트를 개발하여 원래 로직을 재정의합니다(@videojs/http-streaming의 내부 로직을 직접 수정할 수도 있습니다).

// src/js/index.js
import videojs from './video';
import '@videojs/http-streaming';
import './tech/tcadapter'; // 로직 추가
export default videojs;


// src/js/tech/tcadapter.js
import videojs from '../video.js';
import TcAdapter from 'tcadapter';

class Adapter {
  constructor(source, tech, options) {
    const el = tech.el();
    // 매개변수를 가져오기 및 인스턴스 초기화
    const adapter = new TcAdapter(el, {
      appID: '1500002611',
      fileID: '5285890813738446783',
      psign: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTUwMDAwMjYxMSwiZmlsZUlkIjoiNTI4NTg5MDgxMzczODQ0Njc4MyIsImN1cnJlbnRUaW1lU3RhbXAiOjE2MTU5NTEyMzksImV4cGlyZVRpbWVTdGFtcCI6MjIxNTY1MzYyMywicGNmZyI6ImJhc2ljRHJtUHJlc2V0IiwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiMjIxNTY1MzYyMyJ9fQ.hRrQYvC0UYtcO-ozB35k7LZI6E3ruvow7DC0XzzdYKE',
      hlsConfig: {},
    });
    adapter.on(TcAdapter.TcAdapterEvents.LEVEL_LOADED, this.onLevelLoaded.bind(this));
  }

  dispose() {
    this.hls.destroy();
  }

  onLevelLoaded(event) {
    this._duration = event.data.details.live ? Infinity : event.data.details.totalduration;
  }

}

let hlsTypeRE = /^application\/(x-mpegURL|vnd\.apple\.mpegURL)$/i;
let hlsExtRE = /\.m3u8/i;

let HlsSourceHandler = {
  name: 'hlsSourceHandler',
  canHandleSource: function (source) {
    // skip hls fairplay, need to use Safari resolve it.
    if (source.skipHlsJs || (source.keySystems && source.keySystems['com.apple.fps.1_0'])) {
      return '';
    } else if (hlsTypeRE.test(source.type)) {
      return 'probably';
    } else if (hlsExtRE.test(source.src)) {
      return 'maybe';
    } else {
      return '';
    }
  },

  handleSource: function (source, tech, options) {
    if (tech.hlsProvider) {
      tech.hlsProvider.dispose();
      tech.hlsProvider = null;
    } else {
      // hls 자동 로딩 비활성화 후 리소스를 수동으로 로딩해야 합니다
      if (options.hlsConfig && options.hlsConfig.autoStartLoad === false) {
        tech.on('play', function () {
          if (!this.player().hasStarted()) {
            this.hlsProvider.hls.startLoad();
          }
        });
      }
    }
    tech.hlsProvider = new Adapter(source, tech, options);
    return tech.hlsProvider;
  },
  canPlayType: function (type) {
    if (hlsTypeRE.test(type)) {
      return 'probably';
    }
    return '';
  }
};

function mountHlsProvider(enforce) {
  if (TcAdapter && TcAdapter.isSupported() || !!enforce) {
    try {
      let html5Tech = videojs.getTech && videojs.getTech('Html5');
      if (html5Tech) {
        html5Tech.registerSourceHandler(HlsSourceHandler, 0);
      }
    } catch (e) {
      console.error('hls.js init failed');
    }
  } else {
    // tcadapter를 가져오지 않았거나, MSE를 사용할 수 없거나, x5 커널을 사용할 수 없습니다
  }
}
mountHlsProvider();
export default Adapter;

```
