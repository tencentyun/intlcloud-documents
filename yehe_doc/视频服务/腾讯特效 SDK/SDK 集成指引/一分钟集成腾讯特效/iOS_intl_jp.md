## 統合の準備

### 開発者環境要件

- 開発ツールXCode11以降：App Storeまたは[Demoのダウンロード](https://intl.cloud.tencent.com/document/product/1143/45374)をクリックします。
- 推奨実行環境：
  - デバイス要件：iPhone 5およびそれ以上。iPhone 6およびそれ以下はフロントカメラのサポートは最大720pとし、1080pはサポートしていません。
  - システム要件：iOS 10.0およびそれ以降のバージョン。

### SDKのインポート

CocoaPodsスキームを使用するか、SDKをローカルにダウンロードして、現在のプロジェクトに手動でインポートするかを選択できます。
<dx-tabs>
::: CocoaPodsの使用
1. **CocoaPodsのインストール**
端末のウィンドウに次のコマンドを入力します（事前にMac にRuby環境をインストールしておく必要があります ）。
```
sudo gem install cocoapods
```
2. **Podfileファイルの作成**
プロジェクトが存在するパスに入り、次のコマンドラインを入力するとプロジェクトパスの下にPodfile ファイルが現れます。
```
pod init
```
3. **Profileファイルの編集**
プロジェクトのニーズに応じて適切なバージョンを選択し、Podfileを編集します：
	- **XMagicスタンダード版**
次の方法でProfileファイルの編集を行ってください。
```
platform :ios, '8.0'

target 'App' do
pod 'XMagic'
end
```
  - **XMagic簡易版**
インストールパッケージのボリュームがスタンダード版より小さく、ベーシック版A1-00、ベーシック版A1-01、プレミアム版S1-00のみをサポートしています。次の方法でPodfileファイルの編集を行ってください。
```
platform :ios, '8.0'

target 'App' do
pod 'XMagic_Smart'
end
```
4. **SDKの更新およびインストール**
端末ウィンドウに次のコマンドを入力し、ローカルライブラリファイルを更新し、SDKをインストールします。
```
pod install
```
pod コマンドの実行が完了すると、SDKが統合された.xcworkspace という拡張子のプログラムファイルが生成されますので、これをダブルクリックして開きます。
5. **実際のプロジェクトへの美顔リソースの追加**
対応するパッケージの[SDKおよび美顔リソース](https://www.tencentcloud.com/document/product/1143/45377)をダウンロードして解凍し、**resources**フォルダ下の**LightCore.bundle**、**Light3DPlugin.bundle**、**LightBodyPlugin.bundle**、**LightHandPlugin.bundle**、**LightSegmentPlugin.bundle**以外の**その他のbundleリソース**を実際のプロジェクトに追加します。
6. Bundle Identifierを、テスト用に申請した権限と同じものに変更します。
:::
::: SDKのダウンロードと手動でのインポート
1. [SDKおよび美顔リソース](https://www.tencentcloud.com/document/product/1143/45377)をダウンロードして解凍します。frameworksフォルダ内にあるのがsdk、resourcesフォルダ内にあるのが美顔のbundleリソースです。
2. ご自身のXcodeプロジェクトを開き、frameworksフォルダ内のframeworkを実際のプロジェクトに追加します。実行したいtargetを選択し、**General**の項目を選び、**Frameworks,Libraries,and Embedded Content**の項目をクリックして展開し、下部の「+」アイコンをクリックして依存ライブラリを追加します。ダウンロードした`XMagic.framework`、`YTCommonXMagic.framework`、`libpag.framework`およびそれらに必要な依存ライブラリ`MetalPerformanceShaders.framework`、`CoreTelephony.framework`、`JavaScriptCore.framework`、`VideoToolbox.framework`、`libc++.tbd`を順に追加します。必要に応じてその他のツールライブラリ、`Masonry.framework`（ウィジェットレイアウトライブラリ）、`SSZipArchive`（ファイル解凍ライブラリ）を追加します。
![](https://qcloudimg.tencent-cloud.cn/raw/64aacf4305d7adf3a2bbe025920be517.png)
3. resourcesフォルダ内の美顔リソースを実際のプロジェクトに追加します。
4. Bundle Identifierを、テスト用に申請した権限と同じものに変更します。
:::
::: 動的ダウンロードと統合
パッケージのサイズを抑えるため、SDKが必要とするモデルリソースとモーションリソースMotionRes（一部のベーシック版SDKにはモーションリソースがありません）をオンラインダウンロードに変更してください。ダウンロード後に、上記のファイルのパスをSDKに設定します。

Demoのダウンロードロジックを再利用することをお勧めします。もちろん、既存のダウンロードサービスを使用することもできます。動的ダウンロードの詳細なガイドについては、[SDKパッケージのスリム化（iOS）](https://www.tencentcloud.com/document/product/1143/48644)をご参照ください。
:::
</dx-tabs>

### 権限の設定
info.plistファイルに対応する権限の説明を追加します。これを行わなければ、iOS 10システム上でプログラムがクラッシュする場合があります。Privacy - Camera Usage Descriptionでカメラの権限を有効にし、Appによるカメラの使用を許可してください。

## 統合の手順

### 手順1：認証
1. 権限の承認を申請し、LicenseURLとLicenseKEYを取得します。
>! 正常な状況では、Appのネットワーク接続が一度成功すれば認証フローは完了するため、Licenseファイルをプロジェクトのプロジェクトディレクトリに保存する**必要はありません**。ただし、Appがネットワークに未接続の状態でSDKの関連機能を使用する必要がある場合は、Licenseファイルをダウンロードしてプロジェクトディレクトリに保存し、最低保証プランとすることができます。この場合、Licenseファイル名は必ず`v_cube.license`としなければなりません。
2. 関連業務モジュールの初期化コードの中でURLとKEYを設定し、licenseのダウンロードをトリガーします。使用する直前になってダウンロードすることは避けてください。あるいはAppDelegateのdidFinishLaunchingWithOptionsメソッドでダウンロードをトリガーすることもできます。このうち、LicenseURLとLicenseKeyはコンソールでLicenseをバインドした際に生成された権限承認情報です。
```
[TELicenseCheck setTELicense:LicenseURL key:LicenseKey completion:^(NSInteger authresult, NSString * _Nonnull errorMsg) {
	if (authresult == TELicenseCheckOk) {
		NSLog(@"認証成功");
	}else{
		NSLog(@"認証失敗");
	}
}];
```
**認証errorCodeの説明**：
<table>
<thead>
<tr>
<th>エラーコード</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>成功です。Success</td>
</tr>
<tr>
<td>-1</td>
<td>入力パラメータが無効です（例：URLまたはKEYが空など）</td>
</tr><tr>
<td>-3</td>
<td>ダウンロードの段階で失敗しました。ネットワークの設定を確認してください</td>
</tr><tr>
<td>-4</td>
<td>ローカルから読み取ったTE権限承認情報が空です。IOの失敗による可能性があります</td>
</tr><tr>
<td>-5</td>
<td>読み取ったVCUBE TEMP Licenseファイルの内容が空です。IOの失敗による可能性があります</td>
</tr><tr>
<td>-6</td>
<td>v_cube.licenseファイルのJSONフィールドが正しくありません。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr><tr>
<td>-7</td>
<td>署名の検証に失敗しました。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr><tr>
<td>-8</td>
<td>復号に失敗しました。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr><tr>
<td>-9</td>
<td>TELicenseフィールド内のJSONフィールドが正しくありません。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr><tr>
<td>-10</td>
<td>ネットワークから解析したTE権限承認情報が空です。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr><tr>
<td>-11</td>
<td>TE権限承認情報をローカルファイルに書き込む際に失敗しました。IOの失敗による可能性があります</td>
</tr><tr>
<td>-12</td>
<td>ダウンロードに失敗しました。ローカルassetの解析も失敗しました</td>
</tr><tr>
<td>-13</td>
<td>認証に失敗しました</td>
</tr><tr>
<td>その他</td>
<td>Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
</tbody></table>

[](id:step3)
### ステップ2：SDKのロード（XMagic.framework）
Tencent Effect SDK使用のライフサイクルはおおむね次のとおりです。
1. 美顔関連リソースをロードします。
```
NSDictionary *assetsDict = @{@"core_name":@"LightCore.bundle",
	@"root_path":[[NSBundle mainBundle] bundlePath]
};
```
2. Tencent Effect SDKを初期化します。
```
initWithRenderSize:assetsDict: (XMagic)
self.beautyKit = [[XMagic alloc] initWithRenderSize:previewSize assetsDict:assetsDict];
```
3. Tencent Effect SDKが各フレームのデータを処理し、対応する処理結果を返します。
```
process: (XMagic)
```
```
// カメラコールバックでフレームデータを渡します
- (void)captureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection;

// オリジナルデータを取得し、各フレームのレンダリング情報を処理します
- (void)mycaptureOutput:(AVCaptureOutput *)captureOutput didOutputSampleBuffer:(CMSampleBufferRef)inputSampleBuffer fromConnection:(AVCaptureConnection *)connection originImageProcess:(BOOL)originImageProcess;

// CPUを使用してデータを処理します
- (YTProcessOutput*)processDataWithCpuFuc:(CMSampleBufferRef)inputSampleBuffer;

// GPUを使用してデータを処理します
- (YTProcessOutput*)processDataWithGpuFuc:(CMSampleBufferRef)inputSampleBuffer;

// Tencent Effect SDKでデータインターフェースを処理します
/// @param input処理データ情報を入力します
/// @return処理後のデータ情報を出力します
- (YTProcessOutput* _Nonnull)process:(YTProcessInput * _Nonnull)input;
```
4. Tencent Effect SDKをリリースします。
```
deinit (XMagic)
// SDKリソースをリリースする必要がある場所を呼び出します
[self.beautyKit deinit]
```

>? 上記の手順が完了すると、ユーザーは自身の実際のニーズに応じて表示のタイミングおよびその他のデバイスの関連環境を制御できるようになります。

## よくあるご質問

[](id:que1)
### 質問1：コンパイルエラー「unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):」が発生しました。

1. **File** > **Project settings** > **Build System**と進み、**Legacy Build System**を選択します。
2. Xcode 13.0++の場合は**File** > **Workspace Settings**で**Do not show a diagnostic issue about build system deprecation**にチェックを入れます。

[](id:que2)
### 質問2：iOSでのリソースインポート実行後のエラー：「Xcode 12.XバージョンのコンパイルでBuilding for iOS Simulator, but the linked and embedded framework '.framework'...と表示される」が発生しました。

**Buil Settings** > **Build Options** > **Validate Workspace** をYesに変更し、再度**実行**をクリックします。
>?  Validate WorkspaceをYesに変更するとコンパイルが完了します。再びNoに変更しても正常に実行できます。そのため、ここではこの問題が発生した場合にのみ注意してください。

[](id:que3)
### 質問3：フィルター設定が反応しません。
設定値が正しいかどうか確認してください。範囲は0～100ですが、値が小さすぎると効果がわかりづらい場合があります。

[](id:que4)
### 質問4：iOS Demoのコンパイルで、dSYMを生成する際にエラーが発生します。
```
PhaseScriptExecution CMake\ PostBuild\ Rules build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh
    cd /Users/zhenli/Downloads/xmagic_s106
    /bin/sh -c /Users/zhenli/Downloads/xmagic_s106/build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh

Command /bin/sh failed with exit code 1
```
 - 問題の原因：`libpag.frameworkとMasonary.framework`の再署名に失敗したことが原因です。
 - 解決方法：
  1. `demo/copy_framework.sh`を開きます。
  2. 次のコマンドを使用してローカルマシンのcmakeのパスを確認し、`$(which cmake)`をローカルcmakeの絶対パスに変更します。
```
which cmake
```
  3. `Apple Development: ......`をすべてご自身の署名に置き換えます。
