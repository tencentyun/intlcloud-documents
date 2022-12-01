ここでは、AndroidとiOS端末に関するいくつかのよくあるご質問とその解決策についてご説明します。

### エラー「no v4 play info」の発生
- FileIdによって再生する場合、まずAdaptive-HLS(10)トランスコードテンプレートでビデオトランスコードするか、プレーヤーの署名psignで再生するビデオを指定する必要があります。この操作をしない場合、ビデオの再生に失敗することがあります。
- リンク不正アクセス防止を有効にせずに再生を行い、その途中で「no v4 play info」エラーが表示された場合は、Adaptive-HLS(10)トランスコードテンプレートを使用してビデオのトランスコードを行うか、またはソースビデオの再生リンクを直接取得し、URL方式で再生することをお勧めします。

### プレーヤーログを抽出してエラーフィードバックを行う方法
Player+は、デフォルトで実行ログをローカルファイルにエクスポートします。[Tencent Cloudテクニカルサポート](https://intl.cloud.tencent.com/document/product/266/19905)は問題の特定を支援する際、これらの実行ログを分析する必要があります。

### Tencent Cloudのメディア資産をプルして再生する方法

セキュリティ上の理由から、現在、AppからTencent Cloudメディア資産を直接プルするためのインターフェースはありません。そのため、**App**>**Appサービスバックエンド**>**Tencent Cloud**のパスで、Tencent Cloudメディア資産をプルする必要があります。バックエンドサービスでは、Tencent Cloud API[メディア情報検索インターフェース](https://intl.cloud.tencent.com/document/product/266/34179)を呼び出して、リストを取得することができます。

## Android SDK

### 再生中に画面が表示されない

SurfaceViewやTextureViewがTXVodPlayerオブジェクトにバインドされているかどうかチェックしてください。

### パッケージサイズの縮小方法

- これまでに9.4およびそれ以前のバージョンのSDKの[ダウンロードキャッシュ機能](https://www.tencentcloud.com/document/product/266/47849)（TXVodDownloadManager内の関連インターフェース）を使用したことがなく、なおかつ9.5およびそれ以降のSDKバージョンで9.4およびそれ以前にキャッシュしたダウンロードファイルを再生する必要がない場合は、この機能のsoファイルをダウンロードしなくてよいため、インストールパッケージのボリュームを減らすことができます。 例えば、9.4およびそれ以前のバージョンでTXVodDownloadManagerクラスのsetDownloadPathとstartDownloadUrl関数を使用して該当のキャッシュファイルをダウンロードしており、なおかつアプリケーション内にTXVodDownloadManagerからコールバックされたgetPlayPathパスを保存してその後の再生に使用しているような場合は、このgetPlayPathパスファイルの再生にlibijkhlscache-master.soが必要ですが、そうでない場合は不要です。app/build.gradleに次を追加します。
  ```xml
  packagingOptions {
      exclude "lib/armeabi/libijkhlscache-master.so"
      exclude "lib/armeabi-v7a/libijkhlscache-master.so"
      exclude "lib/arm64-v8a/libijkhlscache-master.so"
  }
  ```

- お客様のAppが中国本土でのみ使用するAppの場合、`armeabi-v7a`と`arm64-v8a`という2つのアーキテクチャ用にsoファイルをパッケージ化するか、jarのみをパッケージ化して、インストール後にsoファイルを動的にダウンロードすることができます。具体的なチュートリアルについては、[インストールパッケージを圧縮する方法](https://intl.cloud.tencent.com/document/product/647/35165)をご参照ください。

### コンソールのログ出力を減らす方法

LogLevelを設定することによって、注意する必要のないログをフィルタリングして除外することができます。TXLiveBase.setLogLevel(TXLiveConstants.LOG_LEVEL_DEBUG)。

## iOS SDK

### 再生コントロールパネルが表示されない

再生コントロールパネルはMPNowPlayingInfoCenterを介して表示し、nowPlayingInfoの属性でタイトルや画像の更新、サウンドレベルの設定などを行うことができます。詳細については、[SuperPlayer Demo](https://github.com/LiteAVSDK/Player_ios)をご参照ください。

### コンソールのログ出力を減らす

LogLevelは、TXLiveBase.hのsetLogLevelインターフェースを設定することで設定できます。[TXLiveBase setLogLevel:LOGLEVEL_DEBUG] では、数値が大きいほど出力するログが少なくなり、0（すべてのレベルのログを出力する）から6（ログを出力しない）となります。詳細については、TXLiveBase.hをご参照ください。
