このドキュメントはTencent Cloud View Cube Web Super Player Adapterについて紹介します。この製品はTencent Cloudの顧客がフレキシブルなインターフェースを介して、サードパーティのプレーヤーとオンデマンド機能の統合を速やかに実現し、ビデオ再生機能を実装することができます。Super Player Adapter はビデオ基本情報、ビデオストリーム情報、キーフレームとサムネイル情報等の取得をサポートすると同時に、プライベートの暗号化をサポートしています。このドキュメントは、ある程度Javascript言語の基礎がある開発者向けです。

[](id:Integrated)
## SDKの統合

Super Player Adapterは次の2つの統合方式を提供します。

#### 1. cdn統合

ビデオを再生したいページに初期化スクリプトを導入します。スクリプトはグローバルでTcAdapter変数を公開します。

```javascript
<script src="https://cloudcache.tencentcs.com/qcloud/video/dist/tcadapter.1.0.0.min.js"></script>
```

#### 2. npmの統合

```javascript
// npm install
npm install --save tcadapter

// import TcAdapter
import TcAdapter from 'tcadapter';
```


[](id:container)
## プレーヤーコンテナの配置

プレーヤーを表示したいページにコンテナを追加します。TcAdapterは再生ビデオのコンテナをロードするだけでよく、再生スタイルとカスタマイズ機能はサードパーティのプレーヤーまたは使用者自身が実装できます

```javascript
<video id="player-container-id">
</video>
```


[](id:useSDK)
## SDKの使用

#### 現在の環境がTcAdapterをサポートしているかどうかをチェックします

```javascript
TcAdapter.isSupported();
```



#### Adapterを初期化し、Adapterインスタンスを作成します

**説明**

Adapterを初期化します。初期化中にTencent Cloud VODサーバーをリクエストし、ビデオファイル情報を取得することができます。

**インターフェース**

```javascript
const adapter = new TcAdapter('player-container-id', {
  fileID: string,
  appID: string,
  psign: string,
  hlsConfig: {}
}, callback);
```

**パラメータの説明**

| パラメータ名    | タイプ                  | 説明                                             |
| --------- | --------------------- | ------------------------------------------------ |
| appID     | String                | VODアカウントのappID                                  |
| fileID    | String                | 再生したいビデオfileId                               |
| psign     | String                | Super Player署名                                   |
| hlsConfig | HlsConfig             | hls関連設定。hls.jsがサポートする任意のパラメータを使用することができます          |
| callback  | TcAdapterCallBack | 初期化完了コールバック。この方法の後、ビデオ基本情報を取得することができます|

>?TcAdapter低層はhls.jsをもとに実装されており、HlsConfigを介して、hls.jsがサポートする再生動作を微調整するためのパラメータを受信することができます。



#### ビデオの基本情報を取得

**説明**

ビデオ情報の取得を有効にするには、初期化する必要があります。

**インターフェース**

```javascript
VideoBasicInfo adapter.getVideoBasicInfo();
```

**パラメータの説明**

VideoBasicInfo：パラメータは次のとおりです

| パラメータ名      | タイプ   | 説明                 |
| ----------- | ------ | -------------------- |
| name        | String | ビデオ名。           |
| duration    | Float  | ビデオの長さ。単位：秒。 |
| description | String | ビデオの説明。           |
| coverUrl    | String | ビデオカバー。           |



#### ビデオストリーム情報を取得

**説明**

**インターフェース**

```javascript
List<StreamingOutput> adapter.getStreamimgOutputList();
```

**パラメータの説明**

StreamingOutput

| パラメータ名     | タイプ   | 説明                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| drmType    | String | アダプティブビットレートストリーミング保護タイプ。現在、設定値にはplainとsimpleAESがあります。plainは非暗号化を表し、simpleAESはHLSのノーマルな暗号化を表します。 |
| playUrl    | String | 再生URL。                                                   |
| subStreams | List   | アダプティブビットレートストリーミングサブストリーム情報。タイプはSubStreamInfoです。                   |

SubStreamInfo

| パラメータ名         | タイプ   | 説明                                   |
| -------------- | ------ | -------------------------------------- |
| type | String | サブストリームのタイプ。現在設定可能な値はvideoのみです。 |
| width          | Int    | サブストリームのビデオの幅。単位：px。               |
| height         | Int    | サブストリームのビデオの高さ。単位：px。               |
| resolutionName | String | プレーヤーで表示するサブストリームのビデオの仕様名。       |



#### キーフレームキーモーメント情報を取得

**説明**

**インターフェース**

```java
List<KeyFrameDescInfo> adapter.getKeyFrameDescInfo();
```

**パラメータの説明**

KeyFrameDescInfo

| パラメータ名     | タイプ   | 説明          |
| ---------- | ------ | ------------- |
| timeOffset | Float  | 1.1           |
| content    | String | 「オープニングスタート...」 |



#### サムネイル情報を取得

**説明**

**インターフェース**

```javascript
ImageSpriteInfo adapter.getImageSpriteInfo();
```

**パラメータの説明**

ImageSpriteInfo

| パラメータ名    | タイプ   | 説明                                  |
| --------- | ------ | ------------------------------------- |
| imageUrls | List   | サムネイルダウンロードURLアレイ。タイプはString。|
| webVttUrl | String | サムネイルVTTファイルダウンロードURL 。            |



#### 監視イベント

**説明**：プレーヤーは返されたオブジェクトを初期化することでイベントを監視できます。事例：

```javascript
const adapter = TcAdapter('player-container-id', options);
adapter.on(TcAdapter.TcAdapterEvents.Error, function(error) {
  // do something
});
```

typeはイベントタイプです。サポートされるイベントにはhlsネイティブのイベントおよび以下のイベントがあり、TcAdapter.TcAdapterEventsからイベント名にアクセスすることができます：

| 名称           | 説明                                                         |
| :------------- | :----------------------------------------------------------- |
| LOADEDMETADATA | playcgiを介して対応するビデオ情報を取得しました。このイベントコールバック中にビデオ関連情報を取得することができます |
| HLSREADY       | hlsインスタンスの作成が完了しました。このタイミングでhlsインスタンスオブジェクトの各種属性と方法を呼び出すことができます |
| ERROR | エラー発生時にトリガーされます。コールバックパラメータからエラーの具体的な原因を確認することができます |


#### Hlsインスタンスを取得

**説明**：adapter下位層は、hls.jsをもとに実装されており、adapterインスタンスを介して、再生手順の詳細な管理を実現するためのhlsインスタンスおよびインスタンスの属性と方法にアクセスすることができます。

```javascript
adapter.on('hlsready', () => {
  const hls = adapter.hls;
  // ...
})
```

>?[hls.js](https://github.com/video-dev/hls.js/)リンクをご参照ください。

<dx-tabs>
::: 事例1：\sReact\sで\sTcAdapterを使用 
<dx-alert infotype="explain" title="">
詳細については[事例](https://github.com/tcplayer/tcadapter-combine-video)をご参照ください。
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
::: 事例2:\stcadapter\sと\svideojs\sの組み合わせ
<dx-alert infotype="explain" title="">
詳細については[事例](https://github.com/tcplayer/tcadapter-combine-videojs)をご参照ください。
</dx-alert>
<dx-codeblock>
:::  javascript
// 1. videojs再生hlsは、@videojs/http-streamingを使用できることから、tcadapter再生を使用するポリシーを開発し、もとのロジックをカバーしました（@videojs/http-streamingの内部ロジックを直接修正することも可能です）

// src/js/index.js
import videojs from './video';
import '@videojs/http-streaming';
import './tech/tcadapter'; // ロジックの追加
export default videojs;


// src/js/tech/tcadapter.js
import videojs from '../video.js';
import TcAdapter from 'tcadapter';

class Adapter {
  constructor(source, tech, options) {
    const el = tech.el();
    // パラメータを取得し、インスタンスを初期化します
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
      // hlsが自動ロードをオフにした後、手動でリソースをロードする必要があります
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
    //tcadapterが導入されていないか、MSEが使用できないか、x5カーネルが無効になっています
  }
}
mountHlsProvider();
export default Adapter;
:::
</dx-codeblock>

:::
</dx-tabs>


