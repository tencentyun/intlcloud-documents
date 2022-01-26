ここでは、オーディオビデオプラットフォームで一般的にみられる長編ビデオ再生のシーンについて、Super Playerでの長編ビデオ再生のチュートリアルを示します。ユーザーはWeb端末、iOS端末、Android端末のプレーヤーでのビデオ再生方法、 またアダプティブビットレートストリーミングへの自動切り替え、ビデオサムネイルのプレビュー、ビデオのキーモーメント情報の追加方法について知ることができます。

## 学習目標
この段階のチュートリアルで学べる内容は次のとおりです。
- VODでのアダプティブビットレートストリーミングへの変換と出力の方法（プレーヤーが現在の帯域幅に応じて最適なビットレートを動的に選択して再生可能）
- VODでのビデオのキーモーメント情報の設定方法
- VODでスプライトイメージを使用してサムネイルを作成する方法
- プレーヤーでの再生方法

お読みになる前に、Super Playerガイドラインの[段階1：Super playerを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)の部分をすでに学習し、VOD fileidの概念を理解しているかをご確認ください。

## 操作手順
### 手順1：アダプティブビットレートストリーミングとスプライトイメージへの変換と出力
この手順では、ビデオをアダプティブビットレートストリームとスプライトイメージに変換し出力する方法について指導します。
1. [VODコンソール](https://console.cloud.tencent.com/vod)にログインし、**ビデオ処理設定**>**テンプレート設定**>**ABS生成テンプレート**と選択し、**ABS生成テンプレートで作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/e941daca088dbf5ca8a40384fc3ade7f.png)
テンプレートによってユーザーが必要とするアダプティブビットレートストリーミングを作成します。ここではtestAdaptiveという名前のアダプティブビットレートストリーミングテンプレートを作成します。これには3本のサブストリームが含まれ、解像度はそれぞれ480p、720pおよび1080pです。ビデオビットレート、ビデオフレームレート、オーディオビットレートはオリジナルのビデオと同一に維持されます。
![](https://qcloudimg.tencent-cloud.cn/raw/21ee0dba1c79bde7bea922188d8f5b28.png)
2. **ビデオ処理設定**>**テンプレート設定**>**スクリーンキャプチャテンプレート**と選択し、**スクリーンキャプチャテンプレートの作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/8bac06234f924cc2d9327b6e9791157d.png)
テンプレートによってユーザーが必要とするスプライトイメージを作成します。ここではtestSpriteという名前のスプライトイメージテンプレートを作成します。サンプリング間隔は5%、小さい画像の行数は10、小さい画像の列数は10とします。
![](https://qcloudimg.tencent-cloud.cn/raw/3f62b3d05600f729baa8fbe0f7f0e98c.png)
3. タスクフローによって、アダプティブビットレートストリーミングテンプレートとスプライトイメージテンプレートを追加します。
**ビデオ処理設定**>**タスクフロー設定**>**タスクフローの作成**と選択し、**タスクフローの作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/bc6e4fcd4e53b050fa5f6d59d83608c8.png)
タスクフローによって、ユーザーが処理したいタスクを追加します。ここではアダプティブビットレートストリーミング再生プロセスを表示するため、testPlayVideoのタスクフローを作成しています。このタスクフローにはアダプティブビットレートストリーミングテンプレートとスプライトイメージテンプレートのみを追加しています。
![](https://qcloudimg.tencent-cloud.cn/raw/29ebf8e33157e9c342848c8f1c54ce6d.png)
4. **メディア資産管理**>**オーディオビデオ管理**と選択し、処理したいビデオにチェックを入れ、**ビデオ処理**>**アダプティブビットレートストリーミングへのトランスコード**>**タスクフローの選択**をクリックし、タスクを開始します。
![](https://qcloudimg.tencent-cloud.cn/raw/31392ed275f4406b73ceb2d3c866e3ad.png)
5. これで、**オーディオビデオ管理**>**操作**>**管理**にて、処理後のタスク結果を取得することができます。

### 手順2：ビデオのキーモーメント情報追加
この手順では、新規追加したビデオのキーモーメント情報について指導します。
1. VODサーバーAPIドキュメント>**メディア資産管理関連インターフェース**>[**メディアファイルのプロパティ修正**](https://intl.cloud.tencent.com/document/product/266/37570)と進み、デバッグをクリックし、Tencent Cloud APIコンソールに進んでデバッグを行います。
![](https://qcloudimg.tencent-cloud.cn/raw/69cc5e88d5858b25e6a21e59082c946a.png)
2. パラメータ名**AddKeyFrameDescs.N**によって指定のビデオのキーモーメント情報を追加します
![](https://qcloudimg.tencent-cloud.cn/raw/85eb2701162edf90c309d161af2bff99.png)
ここまででクラウド上の操作は完了です。この時点で、VODでのアダプティブビットレートストリーミング、ビデオスプライトイメージの変換と出力、および関連のビデオキーモーメント情報の追加が完了しています。

### 手順3：プレーヤーの統合
この手順では、Web端末、iOS端末、Android端末のプレーヤーでのアダプティブビットレートストリーミング再生、サムネイルとキーモーメント情報の追加方法について指導します。

<dx-tabs>
::: Web端末
ユーザーがView Cube Super Playerを統合したい場合は、[統合ガイド](https://intl.cloud.tencent.com/document/product/266/33976)を参照し、Player+ファイルをインポートした後、**メディア資産管理**でメディア資産をアップロードしたappIdおよびfileIdを抽出し、再生を行うことができます。

プレーヤーの構築方法は`TCPlayer`です。これによってプレーヤーインスタンスを作成すると、すぐに再生できます。

#### 1. htmlファイルにプレーヤーコンテナを配置

プレーヤーを表示したいページ位置にプレーヤーコンテナを追加します。例えば、index.htmlに次のコードを追加します（コンテナIDおよび幅と高さはいずれもカスタマイズできます）。

```
<video id="player-container-id" width="414" height="270" preload="auto" playsinline webkit-playsinline>
</video>
```

#### 2. fileIDを使用して再生

index.htmlページで初期化コードに次の初期化スクリプトを加え、取得したfileIDおよびappIDを渡すとすぐに再生できます。

```
var player = TCPlayer('player-container-id', { // player-container-idはプレーヤーコンテナIDであり、htmlのIDと一致している必要があります
    fileID: '5285890799710670616', // 再生したいビデオfileIDを渡してください（必須）
    appID: '1400329073' // VODアカウントのappIDを渡してください（必須）
});
```


:::
::: iOS端末
ユーザーがView Cube Super Playerを統合したい場合は、[統合ガイド](https://intl.cloud.tencent.com/document/product/266/33976)をご参照ください。統合完了後、**メディア資産管理**でメディア資産をアップロードしたappIdおよびfileIdを抽出し、再生を行うことができます。

プレーヤーのメインクラスは、`SuperPlayerView`です。作成後すぐにビデオを再生できます。

```xml
// ヘッダーファイルの導入
#import <SuperPlayer/SuperPlayer.h>

// プレーヤーの作成  
_playerView = [[SuperPlayerView alloc] init];
// イベントを受信するための、プロキシの設定
_playerView.delegate = self;
// 親Viewの設定。_playerViewがholderViewの下に自動的に追加されます
_playerView.fatherView = self.holderView;
```

#### fileIdを使用して再生

```java
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// AppIdを設定
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = @"5285890799710670616"; // FileIdを設定
[_playerView playWithModel:model];
```
:::
:::  Android端末
View Cube Super Playerの統合については、[統合ガイド](https://intl.cloud.tencent.com/document/product/266/33975)をご参照ください。統合完了後、**メディア資産管理**でメディア資産をアップロードしたappIdおよびfileIdを抽出し、再生を行うことができます。

プレーヤーのメインクラスは、`SuperPlayerView`です。作成後すぐにビデオを再生できます。

#### 1. レイアウトファイル上でのSuperPlayerViewの作成

```xml
<!-- Super Player-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

#### 2. fileIdを使用して再生

```java
//レイアウトファイルにSuperPlayerViewをインポートした後、インスタンスを作成します
mSuperPlayerView = (SuperPlayerView) findViewById(R.id.superVodPlayerView);
//ホットリンク防止は無効にします
SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppIdを設定
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "5285890799710670616"; // FileIdを設定
mSuperPlayerView.playWithModel(model);
```
:::
</dx-tabs>


## まとめ

これで、プレーヤーでスプライトイメージのプレビュー、ビデオのキーモーメント情報の確認および動的アダプティブビットレートストリーミングへの自動切り替えが行えるようになりました。その他の機能については、[機能説明](https://intl.cloud.tencent.com/document/product/266/42965)をご参照ください。





