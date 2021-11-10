## 製品概要

Tencent Cloud View Cube iOS Super Playerは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。簡単な数行のコードで、Tencent Videoのような強力な再生機能を備えることができます。画面の縦横切り替え、解像度の選択、ジェスチャー、ミニウィンドウなどの基本機能を備えるほか、ビデオキャッシュ、ソフトウェア/ハードウェアデコードの切り替え、倍速再生などの特殊機能もサポートしています。システムのプレーヤーよりも、サポートする形式が多く、互換性に優れ、機能もより強力です。同時に、トップ画面の秒速起動、低遅延などの優位性、ならびにビデオサムネイルなどの高度な機能も備えています。

## バージョンのサポート

このページのドキュメントで説明する機能のTencent Cloud View Cubeでのサポート状況は次のとおりです。

| バージョン名                            | 基本的なライブストリーミングSmart                                               | インタラクティブライブストリーミングLive                                                | User Generated Short Video（UGSV）                                                  | オーディオビデオ通話TRTC                                             | プレーヤーPlayer                                                | 全機能                                                       |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| サポート状況                            | -                                                            | -                                                            | -                                                            | -                                                           | &#10003;                                                     | &#10003;                                                     |
| SDKダウンロード <div style="width: 90px"/> | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=basicLive) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=interactivelive) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=shortVideo) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=video) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=player) | [ダウンロード](https://vcube.cloud.tencent.com/home.html?sdk=allPart) |

各バージョンのSDKに含まれるその他具体的な機能については、[SDKダウンロード](https://cloud.tencent.com/document/product/1449/56978)をご参照ください。

## プロジェクトアドレス[](id:sdkDownload)

Tencent Cloud View Cube iOS Super Playerのプロジェクトアドレスは、[SuperPlayer_iOS](https://github.com/tencentyun/SuperPlayer_iOS)です。

## 対象となる読者

このドキュメントの内容の一部は、Tencent Cloud専用の機能となっていますので、使用前に、[Tencent Cloud](https://intl.cloud.tencent.com)関連サービスのアクティブ化を行ってください。アカウント登録がないユーザーは[アカウント登録](https://intl.cloud.tencent.com/login)が可能です。

## 統合[](id:guide)

本プロジェクトはcocoapodsのインストールをサポートしています。次のコードをPodfileに追加するだけです。

```ruby
pod 'SuperPlayer'
```

pod installまたはpod updateを実行します。

### プレーヤーの使用[](id:usePlayer)

プレーヤーのメインクラスは、`SuperPlayerView`です。作成後すぐにビデオを再生できます。
```objc
// ヘッダーファイルの導入
#import <SuperPlayer/SuperPlayer.h>

// プレーヤーの作成  
_playerView = [[SuperPlayerView alloc] init];
// イベントを受信するための、プロキシの設定
_playerView.delegate = self;
// 親Viewの設定。_playerViewがholderViewの下に自動的に追加されます
_playerView.fatherView = self.holderView;
```

```objc
//ホットリンク防止は無効にします
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// AppIdを設定
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = "5285890799710670616"; // FileIdを設定
[_playerView playWithModel:model];
```
```objc
//ホットリンク防止を有効化するには、psignの入力が必要となり、psignはSuper Playerの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://cloud.tencent.com/document/product/266/42436
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// AppIdを設定
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = "5285890799710173650"; // FileIdを設定
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
```



コードを実行すると、携帯電話で再生したビデオを視聴でき、インターフェース上の機能もほとんどが使用可能な状態になります。


### FileIdの選択[](id:FileId)

ビデオFileIdは、通常、ビデオのアップロード後にサーバーから返されます。

1. クライアントからビデオが公開されると、サーバーがFileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するFileIdが含まれています。

ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、該当するファイルをさがして、FileIdを確認できます。



### キーモーメント機能

時間の長いビデオの再生時は、キーモーメント情報が、視聴者に興味のあるポイントをみつけやすくしてくれます。[メディアファイル属性変更](https://intl.cloud.tencent.com/document/product/266/37570)APIを使用し、AddKeyFrameDescs.Nパラメータによって、ビデオにキーモーメント情報を設定することができます。

呼び出し後、プレーヤーのインターフェースに新しいエレメントが追加されます。



### ミニウィンドウ再生[](id:smallWindow)
ミニウィンドウとはApp内でメインWindowにフロートするプレーヤーのことです。ミニウィンドウでの再生は非常に簡単で、適切な位置で次のコードを呼び出すだけです。

```objc
[SuperPlayerWindow sharedInstance].superPlayer = _playerView; // ミニウィンドウを表示するプレーヤーを設定
[SuperPlayerWindow sharedInstance].backController = self;  // 返されるview controllerを設定
[[SuperPlayerWindow sharedInstance] show]; // フロートの表示
```



### 再生の終了[](id:exitPlayer)

プレーヤーが不要な時には、`resetPlayer`を呼び出してプレーヤー内部の状態を消去し、メモリを解放します。

```objc
[_playerView resetPlayer];
```

## その他の機能[](id:morefeature)

完全な機能は、2次元コードをスキャニングし、ビデオクラウドツールキットをダウンロードして体験するか、またはプログラムのDemoを直接実行することもできます。
<img src="https://main.qcloudimg.com/raw/12c7da97cc910eda673cb19b66fc7cb3.png" width="150">
