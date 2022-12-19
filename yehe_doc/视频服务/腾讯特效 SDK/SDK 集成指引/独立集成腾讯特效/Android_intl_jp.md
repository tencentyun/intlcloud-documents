## 統合の準備
1. [SDKのダウンロード](https://intl.cloud.tencent.com/document/product/1143/45377)を実行し、解凍します。
2. **以下のファイルを準備**します。
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
<dx-tabs>
::: 手動統合
#### 統合
- 上記で準備したすべての`.aar`ファイルをappプロジェクトの`libs`ディレクトリ下に追加します。
- SDKパッケージのassets/ディレクトリにあるすべてのリソースを`../src/main/assets`ディレクトリにコピーします。SDKパッケージのMotionResフォルダにリソースがある場合は、このフォルダを`../src/main/assets`ディレクトリにコピーします。
- jniLibsフォルダをプロジェクトの`../src/main/jniLibs`ディレクトリ下にコピーします。

#### インポート方法
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
>! プロジェクトにGoogleのGsonライブラリを統合していない場合は、次の依存も追加する必要があります。
```groovy
dependencies{
    implementation 'com.google.code.gson:gson:2.8.2'
}
```
:::
::: Mavenの統合
Tencent Effect SDKはMaven Central Repositoryに公開済みであり、gradleの設定によって自動でダウンロードおよび更新が可能です。

1. dependenciesにTencent Effect SDKの依存を追加します。
```groovy
dependencies{
	//例：S1-04パッケージの場合
	implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release'
}
```
2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
```
defaultConfig {
	ndk {
		abiFilters "armeabi-v7a", "arm64-v8a"
	}
}
```
>? 現在、Tencent Effect SDKはarmeabi-v7aおよびarm64-v8aをサポートしています。

3. ![img](https://main.qcloudimg.com/raw/d6b018054b535424bb23e42d33744d03.png)**Sync Now**をクリックすると、SDKが自動的にダウンロードされプロジェクトに統合されます。
4. パッケージに動的エフェクトおよびフィルター機能が含まれる場合は、[SDKダウンロードページ](https://intl.cloud.tencent.com/document/product/1143/45377)で対応するリソースをダウンロードし、動的エフェクトおよびフィルター素材をプロジェクトの以下のディレクトリに配置する必要があります。
	- 動的エフェクト：`../assets/MotionRes`      
	- フィルター：`../assets/lut`

#### 各パッケージに対応するMavenアドレス

| バージョン    | Mavenアドレス                                                    |
| ------- | ------------------------------------------------------------ |
| A1 - 01 | implementation 'com.tencent.mediacloud:TencentEffect_A1-01:latest.release' |
| A1 - 02 | implementation 'com.tencent.mediacloud:TencentEffect_A1-02:latest.release' |
| A1 - 03 | implementation 'com.tencent.mediacloud:TencentEffect_A1-03:latest.release' |
| A1 - 04 | implementation 'com.tencent.mediacloud:TencentEffect_A1-04:latest.release' |
| A1 - 05 | implementation 'com.tencent.mediacloud:TencentEffect_A1-05:latest.release' |
| A1 - 06 | implementation 'com.tencent.mediacloud:TencentEffect_A1-06:latest.release' |
| S1 - 00 | implementation 'com.tencent.mediacloud:TencentEffect_S1-00:latest.release' |
| S1 - 01 | implementation 'com.tencent.mediacloud:TencentEffect_S1-01:latest.release' |
| S1 - 02 | implementation 'com.tencent.mediacloud:TencentEffect_S1-02:latest.release' |
| S1 - 03 | implementation 'com.tencent.mediacloud:TencentEffect_S1-03:latest.release' |
| S1 - 04 | implementation 'com.tencent.mediacloud:TencentEffect_S1-04:latest.release' |
:::
::: 動的ダウンロードと統合
#### assets、so、動的エフェクトリソースガイドの動的ダウンロード
パッケージのサイズを小さくするため、SDKに必要なassetsリソース、soライブラリ、および動的エフェクトリソースMotionRes（一部のベーシック版SDKには動的エフェクトリソースはありません）をネットワークからのダウンロードに変更することができます。ダウンロード成功後、上記ファイルのパスをSDKに設定します。

Demoのダウンロードロジックを再利用することをお勧めします。もちろん、既存のダウンロードサービスを使用することもできます。動的ダウンロードの詳細なガイドについては、[SDKパッケージのスリム化（Android）](https://www.tencentcloud.com/document/product/1143/47831)をご参照ください。
:::
</dx-tabs>


## 全体フロー

[](id:step1)
### 手順1：認証

1. 権限の承認を申請し、License URLとLicense KEYを取得します。
>! 正常な状況では、Appのネットワーク接続が一度成功すれば認証フローは完了するため、Licenseファイルをプロジェクトのassetsディレクトリに保存する**必要はありません**。ただし、Appがネットワークに未接続の状態でSDKの関連機能を使用する必要がある場合は、Licenseファイルをダウンロードしてassetsディレクトリに保存し、最低保証プランとすることができます。この場合、Licenseファイル名は必ず`v_cube.license`としなければなりません。

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
### 手順2：リソースのコピー
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
### 手順3：SDKの初期化および使用方法

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
 <td>String resDir</td><td>リソースファイルディレクトリ。詳細については、<a href="#step2">手順2</a>をご参照ください</td>
 </tr><tr>
 <td>OnXmagicPropertyErrorListener errorListener</td><td>コールバック関数実装クラス</td>
 </tr></table>

- **戻り値**
 エラーコードの意味については[APIドキュメント](https://intl.cloud.tencent.com/document/product/1143/45399)をご参照ください。
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