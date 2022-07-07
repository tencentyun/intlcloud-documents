## シーンのペインポイントとソリューション
画面共有などのユースケースでは、システムオーディオを相互に共有してください。Electronを使用してMacアプリケーションをパッケージ化する場合、Macコンピュータのデフォルトのサウンドカードはシステムオーディオのキャプチャをサポートしていないため、Macコンピューターでシステムオーディオを共有することは困難です。これに基づいて、TRTCは、このシーンのニーズを満たすためにMac側でシステムオーディオをレコーディングする機能を提供します。具体的なアクセス手順は次のとおりです。

[](id:step1)
### 手順1：システム音声のキャプチャを開始します

[startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback)インターフェースを呼び出して、システム音声のキャプチャを開始し、アップリンクオーディオストリームに混合します。インターフェースが実行された後、成功または失敗の結果は[onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError)を介してコールバックされます。
```javascript
import TRTCCloud, { TRTCAudioQuality } from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
function onSystemAudioLoopbackError(errCode) {
  if(errCode === 0) {
    console.log(‘起動成功');
  }
  if (errCode === -1330) {
    console.log('システム音声のレコーディングを有効にできませんでした。たとえば、オーディオドライバプラグインが利用できません');
  }
  if (errCode === -1331) {
    console.log('オーディオドライバプラグインのインストールが許可されていません');
  }
  if (errCode === -1332) {
    console.log('オーディオドライバプラグインのインストールに失敗しました');
  }
}

trtcCloud.on('onSystemAudioLoopbackError', onSystemAudioLoopbackError);
trtcCloud.startLocalAudio(TRTCAudioQuality.TRTCAudioQualityDefault);
trtcCloud.startSystemAudioLoopback();


```

>! startSystemAudioLoopbackを最初に呼び出すと、root権限が取得され（下図を参照）、ユーザーが**OK**をクリックすると、仮想サウンドカードプラグインが自動的にインストールされます。  

[](id:step2)

### 手順2：システム音声のキャプチャを停止します 
[stopSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSystemAudioLoopback)インターフェースを呼び出して、システム音声のキャプチャを終了します。
```javascript
trtcCloud.stopSystemAudioLoopback();
```

[](id:step3)
### 手順3：システム音声のキャプチャボリュームを設定します
[setSystemAudioLoopbackVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSystemAudioLoopbackVolume)インターフェースを呼び出して、システム音声のキャプチャボリュームを設定します。

```javascript
trtcCloud.setSystemAudioLoopbackVolume(60);
```

## 統合のまとめ
Mac側では、TRTCは仮想サウンドカードプラグイン`TRTCAudioPlugin.driver`を使用してシステムオーディオをレコーディングします。この仮想サウンドカードプラグインをシステムディレクトリ`/Library/Audio/Plug-Ins/HAL`にコピーし、オーディオサービスを再起動して有効にする必要があります。仮想サウンドカードプラグインが正常にインストールされているかどうかは、`Launchpad`の`その他`フォルダにある`オーディオMIDI設定`アプリケーションで確認できます。このアプリケーションのデバイスリストに「TRTC Audio Device」という名前のデバイスがある場合は、TRTCの仮想サウンドカードプラグインが正常にインストールされていることを示します。  
