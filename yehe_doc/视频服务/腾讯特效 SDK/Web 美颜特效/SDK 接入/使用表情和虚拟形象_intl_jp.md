美顔エフェクトSDKはバージョン0.3.0からAnimoji表情およびVRバーチャルキャラクター機能をサポートしています。
**この機能は現在Web端末のみサポートしています。**

## サポート対象かどうかのチェック
Animoji表情およびVRバーチャルキャラクターはWebGL2の環境下での使用のみサポートしています。SDKは判断用にチェックの静的メソッドを提供しています。
```javascript
import {ArSdk} from 'tencentcloud-webar'
if (ArSdk.isAvatarSupported()) {
    // 関連機能を初期化します

}else{
    alert('現在のブラウザではバーチャルキャラクターをサポートしていません')
    // 関連機能を非表示にします
}
```

## Animoji表情
### モデルリストの取得
SDKの初期化完了後に、内蔵されているモデルリストを取得できます。現在SDKには4つの表情プロフィール画像が内蔵されています。
```javascript
const avatarARList = await sdk.getAvatarList('AR')
```

>! Animoji表情およびバーチャルキャラクターはメイクアップ、ステッカーなどの効果を自動的に消去します。同様にメイクアップとステッカーを設定した場合も表情またはバーチャルキャラクター効果が消去されます。

### モデル設定
リストを取得後、EffectIdによってAnimoji表情エフェクトを設定することができます。
```javascript
ar.setAvatar({
  mode: 'AR', // モードをARに設定します
  effectId: avatarARList[0].EffectId// 内蔵idを渡します
}, () => {
  // success callback
  
});
```
### カスタムモデル
モデルのカスタマイズが必要な場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)ください。


## VRバーチャルキャラクター
### モデルリストの取得
SDKの初期化完了後に、内蔵されているモデルリストを取得できます。現在SDKには10個のバーチャルキャラクターが内蔵されています。
```javascript
const avatarVRList = await sdk.getAvatarList('VR')
```

### シナリオの設定
```javascript

ar.setAvatar({
  mode: 'VR', // modeはARを渡します
  effectId: avatarVRList[0].EffectId, // 内蔵idを渡します
  backgroundUrl: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg',
}, () => {
    // success callback

  
});
```

>! VRシナリオの設定には背景画像URLの同期設定が必要です。デフォルトでは黒色の背景となります。

### カスタムモデル
ご自身のバーチャルキャラクターをスピーディーにカスタマイズし、直接SDKで使用できるようにする方法は2種類あります。
- 方法1：`readyplayer.me`
- 方法2：[Vroid](https://vroid.com/en/studio)

どちらの方法でもエクスポートしたモデルはご自身でCDNにアップロードし、URLを使用してSDKを設定する必要があります。
```javascript
ar.setAvatar({
  mode: 'VR', // modeはARを渡します
  url: 'https://xxxx.glb', // 内蔵idを渡します
  backgroundUrl: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg',
}, () => {
    // success callback

});
```
現在、カスタムモデルはGLBおよびVRM形式のみサポートしています。
