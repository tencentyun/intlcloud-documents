現在、ショート動画のエンタープライズ版はサポートが終了しています。そのうち、美顔モジュールはデカップリングおよびアップグレードされ、Tencent Effect SDKになりました。Tencent Effect SDKの美顔効果はより自然であるほか、製品の機能はより強力であり、統合方法はより柔軟です。このドキュメントは、ショート動画のエンタープライズ版をTencent Effect SDK（美顔エフェクト）にアップグレードするための移行ガイドです。

## 注意事項
1. xmagicモジュールのglideライブラリのバージョン番号を変更して、実際に使用するものと一致させます。
2. xmagicモジュールの最小バージョン番号を変更して、実際に使用するものと一致させます。


## 統合の手順
### 手順1：Demoプロジェクトの解凍
1. Tencent Effect TEを統合した[UGSV Demo](https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.115.vcube/UGSV_Demo.zip)プロジェクトをダウンロードします。このDemoは、Tencent Effect SDK S1-04パッケージに基づいて作成されています。
2. リソースを置き換えます。このDemoプロジェクトで使用されるSDKパッケージは実際のパッケージと同じではない可能性があるため、このDemoの関連SDKファイルを実際に使用するパッケージのSDKファイルに置き換えてください。具体的な操作は以下のとおりです：
   - xmagicモジュールのlibsディレクトリにある`.aar`ファイルを削除し、SDKのlibsディレクトリにある.aar`ファイルをxmagicモジュールのlibsディレクトリにコピーします。
   - xmagicモジュールのassetsディレクトリにあるすべてのファイルを削除し、SDKの`assets/`ディレクトリにあるすべてのリソースをxmagicモジュールの`../src/main/assets`ディレクトリにコピーします。SDKパッケージのMotionResフォルダにリソースがある場合は、このフォルダを`../src/main/assets`ディレクトリにコピーします。
   - xmagicモジュールのjniLibsディレクトリにあるすべての.soファイルを削除し、SDKパッケージのjniLibsで対応する.soファイルを見つけて（SDKのjinLibsフォルダにあるarm64-v8aおよびarmeabi-v7aの.soファイルが圧縮パッケージに存在しているため、先に解凍してください）、xmagicモジュールの`../src/main/jniLibs`ディレクトリにコピーします。
3. Demoプロジェクトのxmagicモジュールを実際のプロジェクトにインポートします。

### 手順2：SDKバージョンのアップグレード
SDKをEnterprise版からProfessional版にアップグレードします。
- **置換前**：`implementation 'com.tencent.liteav:LiteAVSDK_Enterprise:latest.release'`
- **置換後**：`implementation 'com.tencent.liteav:LiteAVSDK_Professional:latest.release'`

### 手順3：美顔Licenseの設定
1. プロジェクトのapplicationのoncreateメソッドで以下のメソッドを呼び出します：
```java
XMagicImpl.init(this);
XMagicImpl.checkAuth(null);
```
2. XMagicImpl型で、申請したTencent Effectの**License URLとKey**に置き換えます。

### 手順4：コードの実装
ショート動画のレコーディングインターフェース（TCVideoRecordActivity.java）を例として説明します。

1. `TCVideoRecordActivity.java`型で、以下の変数コードを追加します。
```java
private XMagicImpl mXMagic;
private int isPause = 0;//0：一時停止ではない、1：一時停止、2：一時停止中、3：廃棄が必要
```
2. `TCVideoRecordActivity.java`型のonCreateメソッドの後に以下のコードを追加します。
```java
TXUGCRecord instance = TXUGCRecord.getInstance(this);
instance.setVideoProcessListener(new TXUGCRecord.VideoCustomProcessListener() {
	 @Override
	 public int onTextureCustomProcess(int textureId, int width, int height) {
			 if (isPause == 0 && mXMagic !=null) {
					 return mXMagic.process(textureId, width, height);
			 }
			 return 0;
	 }

	 @Override
	 public void onDetectFacePoints(float[] floats) {
	 }

	 @Override
	 public void onTextureDestroyed() {
			 if (Looper.getMainLooper() != Looper.myLooper()) {  //メインスレッドではない
					 if (isPause == 1) {
							 isPause = 2;
							 if (mXMagic != null) {
									 mXMagic.onDestroy();
							 }
							 initXMagic();
							 isPause = 0;
					 } else if (isPause == 3) {
							 if (mXMagic != null) {
									 mXMagic.onDestroy();
							 }
					 }
			 }
	 }
});
XMagicImpl.checkAuth((errorCode, msg) -> {
	 if (errorCode == TELicenseCheck.ERROR_OK) {
			 loadXmagicRes();
	 }else{
			 TXCLog.e("TAG", "認証に失敗しました。認証urlおよびkeyを確認してください" + errorCode + " " + msg);
	 }
});
```
3. onStopメソッドで以下のコードを追加します：
```java
isPause = 1;
if (mXMagic != null) {
	 mXMagic.onPause();
}
```
4. onDestroyメソッドで以下のコードを追加します：
```java
isPause = 3;
XmagicPanelDataManager.getInstance().clearData();
```
5. onActivityResultメソッドの一番前に以下のコードを追加します：
```java
if (mXMagic != null) {
	 mXMagic.onActivityResult(requestCode, resultCode, data);
}
```
6. このデータ型の最後に以下の2つのメソッドを追加します：
```java
private void loadXmagicRes() {
	 if (XMagicImpl.isLoadedRes) {
			 XmagicResParser.parseRes(getApplicationContext());
			 initXMagic();
			 return;
	 }
	 new Thread(() -> {
			 XmagicResParser.setResPath(new File(getFilesDir(), "xmagic").getAbsolutePath());
			 XmagicResParser.copyRes(getApplicationContext());
			 XmagicResParser.parseRes(getApplicationContext());
			 XMagicImpl.isLoadedRes = true;
			 new Handler(Looper.getMainLooper()).post(() -> {
					 initXMagic();
			 });
	 }).start();

}
/**
* 美顔SDKの初期化
*/
private void initXMagic() {
	 if (mXMagic == null) {
			 mXMagic = new XMagicImpl(this, mUGCKitVideoRecord.getBeautyPanel());
	 }else{
			 mXMagic.onResume();
	 }
}
```

### 手順5：その他のデータ型の変更

1. AbsVideoRecordUI型のmBeautyPanel型をRelativeLayout型に変更し、getBeautyPanel()メソッドの戻り型をRelativeLayoutに変更します。同時に、対応するXMLの構成を変更し、エラーコードをコメントアウトします。
2. UGCKitVideoRecord型のエラーコードをコメントアウトします。
3. ScrollFilterView型のコードを変更し、mBeautyPanel変数を削除して、エラーコードをコメントアウトします。

### 手順6：beautysettingkitモジュールへの依存関係の削除
ugckitモジュールのbuild.gradleファイルで、beautysettingkitモジュールへの依存関係を削除し、プロジェクトをコンパイルして、エラーコードをコメントアウトしてください。

