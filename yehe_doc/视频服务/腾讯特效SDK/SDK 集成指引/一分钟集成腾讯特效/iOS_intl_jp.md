## 統合の準備

### 開発者環境要件

- 開発ツールXCode 11およびそれ以上：App Storeまたは[ダウンロードアドレス](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/iOS/2.4.1.18/demo.zip)をクリックします。
- 推奨実行環境：
  - デバイス要件：iPhone 5およびそれ以上。iPhone 6およびそれ以下はフロントカメラのサポートは最大720pとし、1080pはサポートしていません。
  - システム要件：iOS 10.0およびそれ以降のバージョン。

### C/C++レイヤー開発環境

XCodeはデフォルトではC++環境となります。

<table>
<tr><th>タイプ</th><th>依存ライブラリ</th></tr>
<tr>
<td>システム依存ライブラリ</td>
<td><ul style="margin:0">
<li/>AVFoundation
<li/>Accelerate
<li/>AssetsLibrary
<li/>CoreML
<li/>JavaScriptCore
<li/>CoreFoundation
<li/>MetalPerformanceShaders
<li/>CoreTelephony
<li/>libc++.tbd
</ul></td>
</tr>
<tr>
<td>付属ライブラリ</td>
<td><ul style="margin:0">
<li/>YTCommon（認証静的ライブラリ）
<li/>XMagic（美顔静的ライブラリ）
<li/>libpag（ビデオデコード動的ライブラリ）
</ul></td>
</tr>
</table>

## リソースのインポート
### リソース
- 必須リソースパック：`LightCore.bundle`
- 分割機能パッケージ：`LightSegmentPlugin.bundle`
- ジェスチャー機能パッケージ：`LightHandPlugin.bundle`
- 3D機能パッケージ：`Light3DPlugin.bundle`

### インポート方法
- **方法1**：プロジェクトのリソースに追加するだけです。
- **方法2**：パス`initWithRenderSize:assetsDict: (XMagic)`を指定する必要がある場合は、ここの`assetsDict`によって各リソースパスを設定することができます。

### 権限の設定
info.plistファイルに対応する権限の説明を追加します。これを行わなければ、iOS 10システム上でプログラムがクラッシュする場合があります。Privacy - Camera Usage Descriptionでカメラの権限を有効にし、Appによるカメラの使用を許可してください。

## 統合の手順

[](id:step1)
### ステップ1：署名の準備
frameworkの署名は、直接General-->Masonry.frameworkおよびlibpag.frameworkでEmbed & Signを選択できます。
[](id:step2)
### ステップ2：認証
1. 権限承認を申請し、LicenseURLとLicenseKEYを取得します。[Licenseガイド](https://intl.cloud.tencent.com/document/product/1143/45380)をご参照ください。
> ! 正常な状況では、appのネットワーク接続が一度成功すれば認証フローは完了するため、Licenseファイルをプロジェクトのプロジェクトディレクトリに保存する**必要はありません**。ただし、appがネットワークに未接続の状態でSDKの関連機能を使用する必要がある場合は、licenseファイルをダウンロードしてプロジェクトディレクトリに保存し、最低保証プランとすることができます。この場合、licenseファイル名は必ずv_cube.licenseとしなければなりません。
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
### ステップ3：SDKのロード（XMagic.framework）
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

> ? 上記の手順が完了すると、ユーザーは自身の実際のニーズに応じて表示のタイミングおよびその他のデバイスの関連環境を制御できるようになります。

## よくあるご質問

[](id:que1)
### 質問1：コンパイルエラー「unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):」が発生しました。

1. **File** > **Project settings** > **Build System**と進み、**Legacy Build System**を選択します。
2. Xcode 13.0++の場合は**File** > **Workspace Settings**で**Do not show a diagnostic issue about build system deprecation**にチェックを入れます。

[](id:que2)
### 質問2：iOSでのリソースインポート実行後のエラー：「Xcode 12.XバージョンのコンパイルでBuilding for iOS Simulator, but the linked and embedded framework '.framework'...と表示される」が発生しました。

**Buil Settings** > **Build Options** > **Validate Workspace** をYesに変更し、再度**実行**をクリックします。
> ?  Validate WorkspaceをYesに変更するとコンパイルが完了します。再びNoに変更しても正常に実行できます。そのため、ここではこの問題が発生した場合にのみ注意してください。

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
