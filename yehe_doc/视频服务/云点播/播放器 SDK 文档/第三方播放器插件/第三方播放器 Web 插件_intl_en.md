This document describes the Player Adapter for web, which helps you quickly integrate third-party players with VOD capabilities through flexible APIs to implement video playback. It supports the acquisition of basic video information, video stream information, and keyframe and thumbnail information as well as private encryption. This document is intended for developers with a basic knowledge of JavaScript.



## SDK Integration

Player Adapter for web supports **integration via CDN** and **npm**.

#### Integration via CDN

Import the initialization script to the page where videos need to be played back. The script will expose TcAdapter variables globally.

```javascript
<script src="https://cloudcache.tencentcs.com/qcloud/video/dist/tcadapter.1.0.0.min.js"></script>
```

#### Integration via npm

```javascript
// npm install
npm install tcadapter --save

// import TcAdapter
import TcAdapter from 'tcadapter';
```



## Placing Player Container

Add the container to the page where the player needs to be displayed. TcAdapter only needs to carry the container for video playback. The playback styles and custom features can be implemented by third-party players or yourself.

```javascript
<video id="player-container-id">
</video>
```

## SDK Use Instructions

### Checking the development environment

Check whether the current environment supports TcAdapter.

```javascript
TcAdapter.isSupported();
```

### Initializing Adapter

This API is used to initialize Adapter and create an Adapter instance. The initialization process will request the video file information from the Tencent Cloud VOD server.

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
| appID     | String                | The `APPID` of the VOD account.                                 |
| fileID    | String                | The `fileId` of the video to be played back.                             |
| psign     | String                | The player signature.                                   |
| hlsConfig | HlsConfig             | HLS settings. Any parameters supported by `hls.js` can be used. |
| callback  | TcAdapterCallBack | Callback for initialization completion. Basic video information can be obtained after this method is used. |

> ! The underlying layer of TcAdapter is implemented based on `hls.js`, and it can receive any parameters supported by `hls.js` through `HlsConfig` to fine-tune playback.

### Getting the basic video information

This API is used to get the video information and will take effect only after initialization.

**API**

```javascript
VideoBasicInfo adapter.getVideoBasicInfo();
```

**Parameter description**

The parameters of `VideoBasicInfo` are as follows:

| Parameter | Type | Description |
| ----------- | ------ | ------------------ |
| name        | String | The video name.           |
| duration | Float | Video duration in seconds. |
| description | String | The video description.           |
| coverUrl    | String | The video thumbnail.           |

### Getting video stream information

**API**

```javascript
List<StreamingOutput> adapter.getStreamimgOutputList();
```

**Parameter description**

The parameters of `StreamingOutput` are as follows:

| Parameter | Type | Description |
| ---------- | ------ | ------------------------------------------------------------ |
| drmType    | String | The adaptive bitstream protection type. Valid values: `plain` (no encryption), `simpleAES` (HLS common encryption). |
| playUrl | String | Playback URL |
| subStreams | List   | The adaptive bitrate substream information of the [SubStreamInfo](#SubStreamInfo) type. |

The parameters of `SubStreamInfo` are as follows:[](id:SubStreamInfo)

| Parameter | Type | Description |
| -------------- | ------ | ------------------------------------ |
| type | String | Substream type. Valid values: `video` |
| width | Int | The substream video width in px. |
| height | Int | The substream video height in px. |
| resolutionName | String | The name of the substream video displayed in the player. |

### Getting keyframe timestamp information

**API**

```java
List<KeyFrameDescInfo> adapter.getKeyFrameDescInfo();
```

**Parameter description**

The parameters of `KeyFrameDescInfo` are as follows:

| Parameter | Type | Description |
| ---------- | ------ | ------------- |
| timeOffset | Float  | 1.1           |
| content    | String | "Beginning now..." |

### Getting thumbnail information

**API**

```javascript
ImageSpriteInfo adapter.getImageSpriteInfo();
```

**Parameter description**

The parameters of `ImageSpriteInfo` are as follows:

| Parameter | Type | Description |
| --------- | ------ | ---------------------------------- |
| imageUrls | List | Array of thumbnail download URLs of `String` type. |
| webVttUrl | String | Thumbnail VTT file download URL. |

### Listening on events

The player can perform event listening through the objects returned by the initialization, for example:

```javascript
const adapter = TcAdapter('player-container-id', options);
adapter.on(TcAdapter.TcAdapterEvents.Error, function(error) {
  // do something
});
```

Here, `type` is the event type. Supported events include HLS' native events and the following events. Event names can be accessed from `TcAdapter.TcAdapterEvents`:

| Name | Description |
| :------------- | :----------------------------------------------------------- |
| LOADEDMETADATA | The corresponding video information was obtained through `playcgi`. Relevant video information can be obtained through this event callback. |
| HLSREADY       | An HLS instance was created. At this point, you can call the various attributes and methods of the HLS instance object. |
| ERROR | This event will be triggered when an error occurs. You can view the specific failure cause according to the callback parameters. |


### Getting an HLS instance
The underlying layer of Adapter is implemented based on HLS.js. You can access an HLS instance and its attributes and methods through an Adapter instance to achieve fine control over the playback process.

```javascript
adapter.on('hlsready', () => {
  const hls = adapter.hls;
  // ...
})
```

> ? For more information, see [hls.js](https://github.com/video-dev/hls.js/).



## Samples

### Sample 1. Using TcAdapter in React 

For the specific sample, see [tcplayer/tcadapter-combine-video](https://github.com/tcplayer/tcadapter-combine-video).

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

### Sample 2. Combining TcAdapter with Video.js

For the specific sample, see [tcplayer/tcadapter-combine-videojs](https://github.com/tcplayer/tcadapter-combine-videojs).

```javascript
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

```
