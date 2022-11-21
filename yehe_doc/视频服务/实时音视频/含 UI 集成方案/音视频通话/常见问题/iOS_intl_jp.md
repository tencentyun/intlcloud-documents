### 「The package you purchased does not support this ability」というエラーが表示されました。

上記のエラーが表示された場合は、現在のアプリケーションのオーディオビデオ通話機能パッケージが期限切れまたはアクティブ化されていないことを表します。クイックアクセスの[ステップ1：サービスのアクティブ化](https://www.tencentcloud.com/document/product/647/50992#step1)を参照し、オーディオビデオ通話機能を取得またはアクティブ化することで、引き続きTUICallKitコンポーネントを使用することができます。

### オーディオビデオ通話パッケージを購入するにはどうすればよいですか。

購入リンク[オーディオビデオ通話SDK価格一覧](https://www.tencentcloud.com/document/product/647/50553)をご参照ください。その他にご質問がありましたらページ右側をクリックし、パッケージのご購入前にお問い合わせください。

### TUICallKitソースコードを変更するにはどうすればよいですか。

`CocoaPods`を使用してコンポーネントをインポートします。具体的な手順は次のとおりです。

1. プロジェクトの`Podfile`ファイルと同じ階層のディレクトリ下に`TUICallKit`フォルダを作成します。

2. クリックして[**Github/TUICallKit**](https://github.com/tencentyun/TUICalling)に進み、コードのクローン/ダウンロードを選択した後、[**iOS**](https://github.com/tencentyun/TUICalling/tree/main/iOS)ディレクトリ下の`TUICallKit`、`Resources`フォルダおよび`TUICallKit.podspec`ファイルを、`ステップ1`で作成した`TUICallKit`フォルダ下にコピーします。
3. `Podfile`ファイルに次の依存を追加します。

```objectivec
# :path => "TUICallKit.podspecを指定する相対パス"
pod 'TUICallKit', :path => "TUICallKit/TUICallKit.podspec"
```

4. `pod install`コマンドを実行し、インポートを完了します。

>! `TUICallKit`、`Resources`フォルダと`TUICallKit.podspec`ファイルは同一のディレクトリ下にある必要があります。

**TUICallKitコンポーネント統合後の効果**：

![](https://qcloudimg.tencent-cloud.cn/raw/91afcf4f9c3752222ef4e0589c818eed.png)

>? TUICallKitコンポーネントが統合されると、フォルダの階層化表示がサポートされ、ソースコードの閲覧と変更がしやすくなります。

### TUICallKitと自身で統合したオーディオビデオライブラリは競合しますか。

Tencent Cloudの`オーディオビデオライブラリ`は同時に統合できないため、シンボルの競合が発生する可能性があります。ケースごとに、次のように処理することができます。

1. `TXLiteAVSDK_TRTC`ライブラリを使用している場合は、シンボル競合は発生しません。`Podfile`ファイルに次の依存を直接追加できます。
```objectivec
pod 'TUICallKit'
```

2. `TXLiteAVSDK_Professional`ライブラリを使用している場合は、シンボル競合が発生します。`Podfile`ファイルに次の依存を追加できます。
```objectivec
pod 'TUICallKit/Professional'
```

3. `TXLiteAVSDK_Enterprise`ライブラリを使用している場合は、シンボル競合が発生します。`TXLiteAVSDK_Professional`にアップグレードしてから`TUICallKit/Professional`を使用することをお勧めします。

### TUICallKit統合後に実行エラー「ld: framework not found BoringSSL clang: error: linker command failed with exit code 1 sdk」が表示されました

`TUICallKit`の依存するオーディオビデオライブラリは現時点ではエミュレーターをサポートしていません。実機で実行またはデバッグを行ってください。

### TUICallKitでIM SDKをインポートせず、TRTCだけを使用することはできますか。

**できません。**`TUIKit`全シリーズのコンポーネントはすべて、通信の基本サービス、例えば通話発信シグナル、通話中シグナルなどのコアロジックにTencent Cloud IM SDKを使用しています。他の`IM`製品をご購入済みの場合は、`TUICallKit`ロジックを参照して適合させることも可能です。

### TUICallKitコンポーネントは着信音のカスタマイズをサポートしていますか。

**サポートしています**。[TUICalling#setCallingBell](https://www.tencentcloud.com/document/product/647/51011#setcallingbell)を呼び出して行うことができます。

### CocoaPodsをインストールするにはどうすればよいですか。

ターミナルポートに以下のコマンド（事前に`Mac`に`Ruby`環境をインストールする必要があります）を入力します。
```objectivec
sudo gem install cocoapods
```

### TUICallKitはバックエンドでの実行をサポートしていますか。

**サポートしています**。バックエンドに入っても引き続き関連機能を実行する必要がある場合は、現在のプロジェクトを選択できます。下図に示すように、 **Capabilities** の下に**Background Modes** を設定して **ON**を開いて **Audio，AirPlay and Picture in Picture** にチェックを入れます。

![](https://qcloudimg.tencent-cloud.cn/image/document/970de09ccdab7defb8df741fe671de33.jpeg)
