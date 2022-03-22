## 統合の準備
**ファイルの準備**：
<table>
<tbody><tr><th>ファイルタイプ</th><th>説明</th></tr>
<tr>
<td>xmagic-xxx.aar</td><td>SDK。入力必須</td>
</tr><tr>
<td>../assets/</td><td>アルゴリズムモデル、素材リソースパック。入力必須</td>
</tr><tr>
<td>../jniLibs</td><td>soライブラリ。入力必須</td>
</tr></tbody></table>

## リソースのインポート

### リソース

- 上記で準備したすべての`.aar`ファイルをappプロジェクトの`libs`ディレクトリ下に追加します。
- SDKパッケージ内のassets/ディレクトリ下のすべてのリソースを`../src/main/assets`ディレクトリ下にコピーします。
- jniLibsフォルダをプロジェクトの`../src/main/jniLibs`ディレクトリ下にコピーします。

### インポート方法
appモジュールの`build.gradle`を開き、依存参照を追加します。

```groovy
android{
    ...
    defaultConfig {
        applicationIdを「権限承認licにバインドしたパッケージ名に変更」します
        ....
    }
    packagingOptions {
        pickFirst '**/libc++_shared.so'
    }
}

dependencies{
    ...
    compile fileTree(dir: 'libs', include: ['*.jar','*.aar'])//追加*.aar
}
```

[](id:download)
## assets、so、動的エフェクトリソースガイドの動的ダウンロード

パッケージのサイズを小さくするため、SDKに必要なassetsリソース、soライブラリ、および動的エフェクトリソースMotionRes（一部のベーシック版SDKには動的エフェクトリソースはありません）をネットワークからのダウンロードに変更することができます。ダウンロード成功後、上記ファイルのパスをSDKに設定します。

Demoのダウンロードロジックを再利用することをお勧めします。もちろん、既存のダウンロードサービスを使用することもできます。動的ダウンロードの詳細なガイドについては、[Tencent Effect SDKリソースの動的ダウンロードの説明（Android）](https://docs.qq.com/doc/DWHRlU0dlcHlGR3V4)をご参照ください。 

## 全体フロー

[](id:step1)
### ステップ1：認証

1. 権限承認を申請し、License URLとLicense KEYを取得します。[Licenseガイド](https://intl.cloud.tencent.com/document/product/1143/45380)をご参照ください。
> ! 正常な状況では、Appのネットワーク接続が一度成功すれば認証フローは完了するため、Licenseファイルをプロジェクトのassetsディレクトリに保存する**必要はありません**。ただし、Appがネットワークに未接続の状態でSDKの関連機能を使用する必要がある場合は、Licenseファイルをダウンロードしてassetsディレクトリに保存し、最低保証プランとすることができます。この場合、Licenseファイル名は必ず`v_cube.license`としなければなりません。
2. 関連業務モジュールの初期化コードの中でURLとKEYを設定し、licenseのダウンロードをトリガーします。使用する直前になってダウンロードすることは避けてください。ApplicationのonCreateメソッドでダウンロードをトリガーすることもできますが、この時点でネットワークの権限がない可能性や、ネットワーク接続の失敗率が比較的高い可能性があるため、推奨しません。
```
//ダウンロードのトリガーまたはlicenseの更新のみが目的であり、認証結果には関心がない場合は、4つ目のパラメータにはnullを渡します。
TELicenseCheck.getInstance().setXMagicLicense(context, URL, KEY, null);
```
3. その後、実際に美顔機能を使用する前に(例えばDemoの`LaunchActivity.java`など)認証を行います。
```java
// soライブラリがネットワークからダウンロードしたものの場合は、TELicenseCheck.getInstance().setTELicenseを呼び出す前にsoのパスを設定しておかなければ、認証に失敗する場合があります。
// XmagicApi.setLibPathAndLoad(validLibsDirectory);
// soがapkパッケージ内にある場合は、上記のメソッドを呼び出す必要はありません。
TELicenseCheck.getInstance().setTELicense(context, URL, KEY, new TELicenseCheckListener() {

            @Override
            public void onLicenseCheckFinish(int errorCode, String msg) {
                //注意：このコールバックは呼び出しスレッド内にあるとは限りません
                if (errorCode == TELicenseCheck.ERROR_OK) {
                    //認証に成功しました
                }else{
                    //認証に失敗しました
                }
            }
        });
```
**認証errorCodeの説明：**
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
</tr>
<tr>
<td>-3</td>
<td>ダウンロードの段階で失敗しました。ネットワークの設定を確認してください</td>
</tr>
<tr>
<td>-4</td>
<td>ローカルから読み取ったTE権限承認情報が空です。IOの失敗による可能性があります</td>
</tr>
<tr>
<td>-5</td>
<td>読み取ったVCUBE TEMP Licenseファイルの内容が空です。IOの失敗による可能性があります</td>
</tr>
<tr>
<td>-6</td>
<td><code>v_cube.license</code>ファイルのJSONフィールドが正しくありません。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-7</td>
<td>署名の検証に失敗しました。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-8</td>
<td>復号に失敗しました。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-9</td>
<td>TELicenseフィールド内のJSONフィールドが正しくありません。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-10</td>
<td>ネットワークから解析したTE権限承認情報が空です。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>-11</td>
<td>TE権限承認情報をローカルファイルに書き込む際に失敗しました。IOの失敗による可能性があります</td>
</tr>
<tr>
<td>-12</td>
<td>ダウンロードに失敗しました。ローカルassetの解析も失敗しました</td>
</tr>
<tr>
<td>-13</td>
<td>認証に失敗しました。soがパッケージ内にあるか、またはsoパスが正しく設定されているかを確認してください</td>
</tr>
<tr>
<td>3004/3005</td>
<td>権限承認が無効です。Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
<tr>
<td>3015</td>
<td>Bundle Id / Package Name が一致しません。Appで使用しているBundle Id / Package Nameが申請時のものと同じか、正しい権限承認ファイルを使用しているかを確認してください</td>
</tr>
<tr>
<td>3018</td>
<td>権限承認ファイルが期限切れです。Tencent Cloudに更新を申請する必要があります</td>
</tr>
<tr>
<td>その他</td>
<td>Tencent Cloudチームに連絡して処理を依頼してください</td>
</tr>
</tbody></table>

[](id:step2)
### ステップ2：リソースのコピー
1. リソースファイルがassetsディレクトリ内にある場合は、使用する前にappのプライベートディレクトリにコピーしておく必要があります。事前にコピーしておくか、または前の手順の認証成功のコールバックの中でコピー操作を行うこともできます。サンプルコードは、Demoの`LaunchActivity.java`です。
```
XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath());
//loading

//リソースファイルのプライベートディレクトリへのコピーは1回のみ行います
XmagicResParser.copyRes(getApplicationContext());
```
2. リソースファイルが[ネットワークから動的ダウンロード](#download)したものの場合は、ダウンロード成功後にリソースファイルパスを設定する必要があります。サンプルコードは、Demoの`LaunchActivity.java`です。
```
XmagicResParser.setResPath(ダウンロードしたリソースファイルのローカルパス);
```

[](id:step3)
### ステップ3：SDKの初期化および使用方法

Tencent Effect SDK使用のライフサイクルはおおむね次のとおりです。
1. 美顔UIデータを作成します。Demoプロジェクトのものを参照できます。 `XmagicResParser.java,XmagicUIProperty.java,XmagicPanelDataManager.java`コード。
2. プレビューレイアウトにGLSurfaceViewを追加します。  
```java
<android.opengl.GLSurfaceView
android:id="@+id/camera_gl_surface_view"
android:layout_width="match_parent"
android:layout_height="match_parent" />
```
3. （オプション）カメラをクイック実装します。
Demoプロジェクトのcom.tencent.demo.cameraディレクトリをプロジェクトにコピーします。`PreviewMgr`クラスを利用してカメラ機能をクイック実装します。実装の詳細についてはDemoプロジェクトの`MainActivity.java`をご参照ください。
```java
//カメラ初期化
mPreviewMgr = new PreviewMgr();
//レイアウトしたGlSurfaceViewサンプルをカメラツールクラスに渡します
mPreviewMgr.onCreate(mGlSurfaceView,false);
//プレビューテクスチャデータのコールバック関数を登録します
mPreviewMgr.setCustomTextureProcessor((textureId, textureWidth, textureHeight) -> {
	if (mXmagicApi == null) {
			return textureId;
	}
	//美顔sdkを呼び出してレンダリングします
	int outTexture = mXmagicApi.process(textureId, textureWidth, textureHeight);
	return outTexture;
});

//Activityの中のonResumeメソッドでカメラを有効にします
mPreviewMgr.onResume(this, 1280, 720);
```
4. 美顔SDKを初期化します。Activityの`onResume()`メソッドに保存することをお勧めします。
```java
mXmagicApi = new XmagicApi(this, XmagicResParser.getResPath(),new XmagicApi.OnXmagicPropertyErrorListener()); 
```
- **パラメータ**
 <table>
 <tr><th>パラメータ</th><th>意味</th></tr><tr><td>Context context</td><td>コンテキスト</td>
 </tr><tr>
 <td>String resDir</td><td>リソースファイルディレクトリ。詳細については、<a href="#step2">ステップ2</a>をご参照ください</td>
 </tr><tr>
 <td>OnXmagicPropertyErrorListener errorListener</td><td>コールバック関数実装クラス</td>
 </tr></table>
- **戻り値**
 エラーコードの意味対照表：
 <table>
 <tr><th>エラーコード</th><th>意味</th></tr><tr>
 <td>-1</td><td>不明なエラー</td>
 </tr><tr>
 <td>-100</td><td>3Dエンジンリソースの初期化に失敗しました</td>
 </tr><tr>
 <td>-200</td><td>GAN素材をサポートしていません</td>
 </tr><tr>
 <td>-300</td><td>デバイスがこの素材コンポーネントをサポートしていません</td>
 </tr><tr>
 <td>-400</td><td>テンプレートのJSONの内容が空です</td>
 </tr><tr>
 <td>-500</td><td>SDKのバージョンが低すぎます</td>
 </tr><tr>
 <td>-600</td><td>分割をサポートしていません</td>
 </tr><tr>
 <td>-700</td><td>OpenGLをサポートしていません</td>
 </tr><tr>
 <td>-800</td><td>スクリプトをサポートしていません</td>
 </tr><tr>
 <td>5000</td><td>分割背景画像の解像度が2160*3840を超えています</td>
 </tr><tr>
 <td>5001</td><td>分割背景画像に必要なメモリが不足しています</td>
 </tr><tr>
 <td>5002</td><td>分割背景ビデオの解析に失敗しました</td>
 </tr><tr>
 <td>5003</td><td>分割背景ビデオが200秒を超えています</td>
 </tr><tr>
 <td>5004</td><td>分割背景ビデオのフォーマットをサポートしていません</td>
 </tr>
 </tbody></table>
5. 素材プロンプトのコールバック関数を追加します（メソッドのコールバックはサブスレッドで実行される場合があります）。一部の素材はユーザーに、うなずく、手を伸ばす、指ハートなどを促します。このコールバックは類似のプロンプトの表示に用いられます。
```
mXmagicApi.setTipsListener(new XmagicTipsListener() {
	final XmagicToast mToast = new XmagicToast();
	@Override
	public void tipsNeedShow(String tips, String tipsIcon, int type, int duration) {
		mToast.show(MainActivity.this, tips, duration);
	}

	@Override
	public void tipsNeedHide(String tips, String tipsIcon, int type) {
		mToast.dismiss();
	}
});
```
6. 美顔SDKが各フレームのデータを処理し、対応する処理結果を返します。
```
int outTexture = mXmagicApi.process(textureId, textureWidth, textureHeight);
```
7. 指定するタイプの美顔エフェクトの数値を更新します。
```java
// 使用可能な入力パラメータのプロパティはXmagicResParser.parseRes()から取得できます
mXmagicApi.updateProperty(XmagicProperty<?> p);
```
8. 美顔SDKをPauseします。Activityの`onPause()`ライフサイクルにバインドすることをお勧めします。
```java
//ActivityがonPauseの場合に呼び出します。OpenGLスレッドで呼び出す必要があります
mXmagicApi.onPause();
```
9. 美顔SDKをリリースします。Activityの`onDestroy() `ライフサイクルにバインドすることをお勧めします。
```java
//このメソッドはGLスレッドで呼び出す必要があることにご注意ください
mXmagicApi.onDestroy()
```

