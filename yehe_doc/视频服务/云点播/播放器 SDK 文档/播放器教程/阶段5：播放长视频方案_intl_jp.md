ここでは、オーディオビデオプラットフォームにみられる長編ビデオ長編ビデオ再生のシーンについて、プレーヤーでの長編ビデオ再生のチュートリアルをご紹介します。ユーザーは、Web端末、iOS端末、Android端末のプレーヤーでのビデオ再生方法と同時に、KEY[リンク不正アクセス防止](https://www.tencentcloud.com/document/product/266/49274)の有効化、アダプティブビットレートストリーミングへの自動切り替え、ビデオサムネイルのプレビュー、ビデオのキーモーメント情報の追加方法について知ることができます。

## 学習目標
この段階のチュートリアルで学べる内容は次のとおりです。
- VODでKEYリンク不正アクセス防止を設定し、有効時間、再生人数、再生時間などの制御を実現する方法
- VODでのアダプティブビットレートストリーミングへの変換と出力の方法（プレーヤーが現在の帯域幅に応じて最適なビットレートを動的に選択して再生可能）
- VODでのビデオのキーモーメント情報の設定方法
- VODでスプライトイメージを使用してサムネイルを作成する方法
- プレーヤーでの再生方法

お読みになる前に、プレーヤーガイドラインの[第1段階：プレーヤーを使用したビデオ再生](https://intl.cloud.tencent.com/document/product/266/38098)の部分をすでに学習し、VOD fileidの概念を理解しているかをご確認ください。

## 操作手順
### ステップ1：KEYリンク不正アクセス防止をアクティブにする
アカウントにおけるデフォルト配信ドメイン名でKEYリンク不正アクセス防止を有効にしたケースを例にします。
>!本番環境の現行のネットワークドメイン名に対して直接ホットリンク防止を有効にしないでください。現行のネットワークのビデオが再生できなくなります。

1. VODコンソールにログインし、【配信と再生の設定】 >[ 【ドメイン名管理】 ](https://console.cloud.tencent.com/vod/distribute-play/domain)と選択し、設定画面に進みます。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/pyHf434_1.png" width="800" />

2. 「アクセス制御」タブをクリックし、【Keyリンク不正アクセス防止】を見つけ、グレーのボタンをクリックして有効化し、ポップアップした設定画面で【ランダム生成】をクリックしてランダムなKeyを生成し、その後【OK】をクリックして保存すると有効になります。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/azQ5558_2.jpg" width="522" />

### 手順2：アダプティブビットレートストリーミングとスプライトイメージへの変換と出力
この手順では、ビデオをアダプティブビットレートストリームとスプライトイメージに変換し出力する方法について指導します。
1. [VODコンソール](https://console.cloud.tencent.com/vod)にログインし、**ビデオ処理設定**>**テンプレート設定**>**ABS生成テンプレート**と選択し、**ABS生成テンプレートを作成**をクリックします。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3gkP770_3.png)

テンプレートによってユーザーが必要とするアダプティブビットレートストリーミングを作成します。ここではtestAdaptiveという名前のABSテンプレートを作成します。これには3つのサブストリームが含まれ、解像度はそれぞれ480p、720pおよび1080pです。ビデオビットレート、ビデオフレームレート、オーディオビットレートはオリジナルのビデオと同一に維持されます。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/XIga303_4.jpg)

2. **ビデオ処理設定**>**テンプレート設定**>**スクリーンキャプチャテンプレート**と選択し、**スクリーンキャプチャテンプレートの作成**をクリックします。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/mVrf686_5.png)

テンプレートによってユーザーが必要とするスプライトイメージを作成します。ここでは、testSpriteという名前のスプライトイメージテンプレートを作成します。サンプリング間隔は5%、小さい画像の行数は10、小さい画像の列数は10とします。

![](https://qcloudimg.tencent-cloud.cn/raw/3f62b3d05600f729baa8fbe0f7f0e98c.png)

3. タスクフローによって、ABSテンプレートとスプライトイメージテンプレートを追加します。
**ビデオ処理設定**>**タスクフロー設定**と選択し、**タスクフローの作成**をクリックします。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/sUGF476_7.jpg)

タスクフローによって、ユーザーが処理したいタスクを追加します。ここではアダプティブビットレートストリーミング再生プロセスを表示するため、testPlayVideoのタスクフローを作成しています。このタスクフローには、ABSテンプレートとスプライトイメージテンプレートのみを追加しています。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/4e45517_8.jpg)

4. **メディア資産管理**>**オーディオビデオ管理**と選択し、処理したいビデオ（FileId：387xxxxx8142975036）にチェックを入れ、**タスクフロー**をクリックし、テンプレートを選択してタスクを開始します。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/LAPx726_9.png)

5. これで**タスクセンター**>[**オーディオビデオ管理**](https://console.cloud.tencent.com/vod/task)で、タスクの実行状況を確認し、完了後にタスク結果を取得することができます。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/wrMs396_10.jpg" width="800" />

### 手順3：ビデオのキーモーメント情報追加
この手順では、新規追加したビデオのキーモーメント情報について指導します。
1. VODサーバーAPIドキュメント>**メディア資産管理関連インターフェース**>[**メディアファイルのプロパティ修正**](https://intl.cloud.tencent.com/document/product/266/37570)と進み、デバッグをクリックし、Tencent Cloud APIコンソールに進んでデバッグを行います。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3hHA645_11.jpg)
2. パラメータ名**AddKeyFrameDescs.N**によって指定のビデオのキーモーメント情報を追加します
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dpvW350_12.jpg)
ここまででクラウド上の操作は完了です。この時点で、VODでのアダプティブビットレートストリーミング、ビデオスプライトイメージの変換と出力、および関連のビデオキーモーメント情報の追加が完了しています。

### ステップ4：プレーヤー署名の生成
このステップでは、署名ツールを使用して速やかにプレーヤー署名を生成し、プレーヤーのビデオ再生に使用します。
**配信と再生の設定**>[**プレーヤー署名ツール**](https://console.cloud.tencent.com/vod/distribute-play/signature)を選択し、以下の情報を入力します。
 - **ビデオfileId**に**ステップ2** で使用したFileId（387xxxxx8142975036）を入力します
 - **署名期限タイムスタンプ** プレーヤー署名の有効期間です。入力がなければ署名の有効期限が切れていないことを意味します
 - **再生可能なビデオタイプ**は**アダプティブビットレートストリーミング変換(非暗号化)**を選択します
 - **再生可能なABSテンプレート**は`testAdaptive (1429229)`を選択します
 - **サムネイルプレビューに使用するスプライトイメージ** は`testSprite (131353)`を選択します
 - **リンク不正アクセス防止&暗号化設定**スイッチをオンにし、次のように設定します
  - **リンク期限**に、取得した再生リンクのリンク不正アクセス防止署名の有効期限を設定します
  - **再生可能なIPの最大数**に、再生が許可される異なるIPを持つ端末の最大数を設定します

**署名生成結果**をクリックし、署名結果文字列を取得します。


### 手順5：プレーヤーの統合
ステップ4で、ビデオ再生に必要な3つのパラメータである`appId`、`fileId` およびプレーヤー署名（`psign`）を取得しています
この手順では、Web端末、iOS端末、Android端末のプレーヤーでのアダプティブビットレートストリーミング再生、サムネイルとキーモーメント情報の追加方法について指導します。

<dx-tabs>
::: Web端末
ユーザーがView Cubeプレーヤーを統合したい場合は、[統合ガイド](https://intl.cloud.tencent.com/document/product/266/33977)をご参照ください。Player SDKファイルをインポートした後に、`appId`、`fileId`およびプレーヤー署名（`psign`）を使用して再生します。

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
    fileID: '387xxxxx8142975036', // 再生したいビデオfileID
    appID: '1400329073', // 再生したいビデオのVODアカウントappID
    psign:'psignxxxx'   // psignはプレーヤーの署名です。署名についての紹介および生成方法については、以下のリンクをご参照ください。https://www.tencentcloud.com/document/product/266/38099
});
```


:::
::: iOS端末
ユーザーがView Cubeプレーヤーを統合したい場合は、[統合ガイド](https://intl.cloud.tencent.com/document/product/266/33976)をご参照ください。統合完了後、`appId`、`fileId`およびプレーヤー署名（`psign`）を使用して再生します。

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
model.videoId.fileId = @"387xxxxx8142975036"; // FileIdを設定
// pSignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://www.tencentcloud.com/document/product/266/38099
model.videoId.pSign = @"psignxxxx";
[_playerView playWithModelNeedLicence:model];
[_playerView playWithModel:model];
```
:::
:::  Android端末
ユーザーがView Cubeプレーヤーを統合したい場合は、[統合ガイド](https://intl.cloud.tencent.com/document/product/266/33975)をご参照ください。統合完了後、`appId`、`fileId`およびプレーヤー署名（`psign`）を使用して再生します。

プレーヤーのメインクラスは、`SuperPlayerView`です。作成後すぐにビデオを再生できます。

#### 1. レイアウトファイル上でのSuperPlayerViewの作成

```xml
<!-- プレーヤー-->
<com.tencent.liteav.demo.superplayer.SuperPlayerView
    android:id="@+id/superVodPlayerView"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

#### 2. fileIdを使用して再生

```java
//レイアウトファイルにSuperPlayerViewをインポートした後、インスタンスを作成します
mSuperPlayerView = (SuperPlayerView) findViewById(R.id.superVodPlayerView);

SuperPlayerModel model = new SuperPlayerModel();
model.appId = 1400329073;// AppIdを設定
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "387xxxxx8142975036"; // FileIdを設定
// pSignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://www.tencentcloud.com/document/product/266/38099
model.videoId.pSign = "psignxxxx";

mSuperPlayerView.playWithModel(model);
```
:::
</dx-tabs>


## まとめ

これで、プレーヤーでKeyリンク不正アクセス防止を有効化したVODアカウント下のメディアファイルを再生し、スプライトイメージのプレビューの確認、ビデオキーモーメント情報およびダイナミックアダプティブビットレートストリーミングの自動切り替えを行うことができます。
プレーヤー機能の詳細については、 [機能説明](https://intl.cloud.tencent.com/document/product/266/42965)をご参照ください。
