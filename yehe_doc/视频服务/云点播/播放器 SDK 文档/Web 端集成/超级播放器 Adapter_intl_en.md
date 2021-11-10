This document describes the Tencent Cloud RT-Cube Superplayer Adapter for web, which helps you quickly integrate third-party players with VOD capabilities through flexible APIs to implement video playback. It supports the acquisition of basic video information, video stream information, and keyframe and thumbnail information as well as proprietary encryption. This document is intended for developers with a basic knowledge of JavaScript.

[](id:Integrated)
## Integrating SDK

Superplayer Adapter can be integrated in the following two ways:

#### 1. Integration through CDN

Import the initialization script to the page where videos need to be played back. The script will expose TcAdapter variables globally.

```javascript
<script src="https://cloudcache.tencentcs.com/qcloud/video/dist/tcadapter.1.0.0.min.js"></script>
```

#### 2. Integration through npm

```javascript
// npm install
npm install --save tcadapter

// import TcAdapter
import TcAdapter from 'tcadapter';
```


[](id:container)
## Placing Player Container

Add the container to the page where the player needs to be displayed. TcAdapter only needs to carry the container for video playback. The playback styles and custom features can be implemented by third-party players or yourself.

```javascript
<video id="player-container-id">
</video>
```


[](id:useSDK)
## Using SDK

#### Checking whether the current environment supports TcAdapter

```javascript
TcAdapter.isSupported();
```



#### Initializing Adapter and creating Adapter instance

**Description**

This API is used to initialize Adapter. The initialization process will request the video file information from the Tencent Cloud VOD server.

**API**

```javascript
const adapter = new TcAdapter('player-container-id', {
  fileID: string,
  appID: string,
  psign: string,
  hlsConfig: {}
}, callback);
```

**Parameter description**

| Parameter | Type | Description |
| --------- | --------------------- | ------------------------------------------------ |
| appID     | String                | `appID` of the VOD account                                 |
| fileID    | String                | `fileId` of the video to be played back                               |
| psign     | String                | Superplayer signature                                   |
| hlsConfig | HlsConfig             | HLS settings. Any parameters supported by HLS.js can be used          |
| callback  | TcAdapterCallBack | Callback for initialization completion. Basic video information can be obtained after this method is used |

>?The underlying layer of TcAdapter is implemented based on HLS.js, and it can receive any parameters supported by HLS.js through `HlsConfig` for fine-tuning playback.



#### Getting basic video information

**Description**

This API is used to get the video information and will take effect only after initialization.

**API**

```javascript
VideoBasicInfo adapter.getVideoBasicInfo();
```

**Parameter description**

The parameters of `VideoBasicInfo` are as follows:

| Parameter | Type | Description |
| ----------- | ------ | -------------------- |
| name | String | Video name |
| duration | Float | Video duration in seconds |
| description | String | Video description |
| coverUrl | String | Video cover |



#### Getting video stream information

**Description**

**API**

```javascript
List<StreamingOutput> adapter.getStreamimgOutputList();
```

**Parameter description**

StreamingOutput

| Parameter | Type | Description |
| ---------- | ------ | ------------------------------------------------------------ |
| drmType | String | Adaptive bitstream protection type. Valid values: `plain` (no encryption), `simpleAES` (HLS common encryption) |
| playUrl | String | Playback URL |
| subStreams | List | Adaptive bitstream substream information of the `SubStreamInfo` type |

SubStreamInfo

| Parameter | Type | Description |
| -------------- | ------ | -------------------------------------- |
| type | String | Substream type. Valid values: `video` |
| width | Int | Substream video width in px |
| height | Int | Substream video height in px |
| resolutionName | String | Specification name of the substream video displayed in the player |



#### Getting keyframe timestamp information

**Description**

**API**

```java
List<KeyFrameDescInfo> adapter.getKeyFrameDescInfo();
```

**Parameter description**

KeyFrameDescInfo

| Parameter | Type | Description |
| ---------- | ------ | ------------- |
| timeOffset | Float  | 1.1           |
| content    | String | "Beginning now..." |



#### Getting thumbnail information

**Description**

**API**

```javascript
ImageSpriteInfo adapter.getImageSpriteInfo();
```

**Parameter description**

ImageSpriteInfo

| Parameter | Type | Description |
| --------- | ------ | ------------------------------------- |
| imageUrls | List | Array of thumbnail download URLs of `String` type |
| webVttUrl | String | Thumbnail VTT file download URL |



#### Listening on event

**Description**: the player can perform event listening through the objects returned by the initialization, for example:

```javascript
const adapter = TcAdapter('player-container-id', options);
adapter.on(TcAdapter.TcAdapterEvents.Error, function(error) {
  // do something
});
```

Here, `type` is the event type. Supported events include HLS' native events and the following events. Event names can be accessed from `TcAdapter.TcAdapterEvents`:

| Name | Description |
| :------------- | :----------------------------------------------------------- |
| LOADEDMETADATA | The corresponding video information was obtained through `playcgi`. Relevant video information can be obtained through this event callback |
| HLSREADY       | An HLS instance was created. At this point, you can call the various attributes and methods of the HLS instance object |
| ERROR | This event will be triggered when an error occurs. You can view the specific failure cause according to the callback parameters |


#### Getting HLS instance

**Description**: the underlying layer of Adapter is implemented based on HLS.js. You can access an HLS instance and its attributes and methods through an Adapter instance to achieve fine control over the playback process.

```javascript
adapter.on('hlsready', () => {
  const hls = adapter.hls;
  // ...
})
```

>?Please see [hls.js](https://github.com/video-dev/hls.js/).

<dx-tabs>
::: Sample 1. Use \sTcAdapter in \sReact\s 
<dx-alert infotype="explain" title="">
Please see more [samples](https://github.com/tcplayer/tcadapter-combine-video).
</dx-alert>

<dx-codeblock>
:::  javascript
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
:::
</dx-codeblock>

:::
::: Sample 2. Combine \stcadapter\s and \svideojs\s
<dx-alert infotype="explain" title="">
Please see more [samples](https://github.com/tcplayer/tcadapter-combine-videojs).
</dx-alert>
<dx-codeblock>
:::  javascript
// 1. Video.js playback over HLS uses `@videojs/http-streaming`, so we have developed a set of policies for playback with TcAdapter to override the original logic (you can also directly modify the internal logic of `@videojs/http-streaming`)

// src/js/index.js
import videojs from './video';
import '@videojs/http-streaming';
import './tech/tcadapter'; // Add logic
export default videojs;


// src/js/tech/tcadapter.js
import videojs from '../video.js';
import TcAdapter from 'tcadapter';

class Adapter {
  constructor(source, tech, options) {
    const el = tech.el();
    // Get parameters and initialize the instance
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
      // After automatic loading is disabled for HLS, you need to manually load resources
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
    // TcAdapter is not imported, MSE is not available, or X5 kernel is disabled
  }
}
mountHlsProvider();
export default Adapter;
:::
</dx-codeblock>

:::
</dx-tabs>


