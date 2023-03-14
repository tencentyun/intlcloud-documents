Unityを使う開発者たちがTencent Cloud Gaming Multimedia Engineの製品APIのデバッグ・アクセスを手軽に実行できるように、ここでUnity開発に向けるプロジェクトエクスポート設定について説明します。

## iOSプラットフォームのエクスポートについて

UnityプロジェクトからXcodeプロジェクトにエクスポートする際には、GME動的ライブラリを処理する必要があり、処理手段はUnityのバージョンによって異なります。

###　1.　動的ライブラリ処理（Unity 2019以降）

#### 設定の原理

UnityEditor.iOS.Xcode.Extensions.PBXProjectExtensions.AddFileToEmbedFrameworksを使用して新しいEditor OnPostprocessBuildスクリプトを作成します。このAPIは、動的ライブラリを最終的なパッケージBundleのframeworkディレクトリに自動的にコピーし、署名します。

ビジネス層は、必要な機能に基づいて動的ライブラリを削減し、動的ライブラリのリストに基づいてサンプルコードにインポートするフレームワークのリストを決定します。動的ライブラリの機能については、[動的ライブラリディレクトリ](https://intl.cloud.tencent.com/document/product/607/32363)をご参照ください。

```
string[] framework_names = {
	"libgme_fdkaac.framework",
	"libgme_lamemp3.framework",
	"libgme_ogg.framework",
	"libgme_soundtouch.framework"
};
```


####  サンプルコード

Demoプロジェクト内のadd_dylib.csスクリプトファイルを参照して、プロジェクトのニーズに応じて、このコードの一部をプロジェクト内のEditorフォルダに配置します。

```c#
[UnityEditor.Callbacks.PostProcessBuild(1002)]
public  static void OnPostprocessBuild (UnityEditor.BuildTarget BuildTarget, string path){  
	if (BuildTarget == UnityEditor.BuildTarget.iOS) {
		UnityEngine.Debug.Log ("OnPostprocessBuild add_dylib:" + path);
#if UNITY_EDITOR_OSX || UNITY_STANDALONE_OSX
		{
			string projPath = UnityEditor.iOS.Xcode.PBXProject.GetPBXProjectPath (path);  
			UnityEditor.iOS.Xcode.PBXProject proj = new UnityEditor.iOS.Xcode.PBXProject ();  

			proj.ReadFromString (System.IO.File.ReadAllText (projPath));  
			// string targetGuid = proj.TargetGuidByName (UnityEditor.iOS.Xcode.PBXProject.GetUnityTargetName ()); // 2018
			string targetGuid = proj.GetUnityMainTargetGuid();	// 2019
				
			//　インポートされたフレームワークによる削減
			string[] framework_names = {
				"libgme_fdkaac.framework",
				"libgme_lamemp3.framework",
				"libgme_ogg.framework",
				"libgme_soundtouch.framework"
			};

			for (int i = 0; i < framework_names.Length; i++)
			{
				string framework_name = framework_names[i];
				string dylibGuid = null;
				dylibGuid = proj.FindFileGuidByProjectPath("Frameworks/Plugins/iOS/" + framework_name);

				if (dylibGuid == null) {
					UnityEngine.Debug.LogWarning (framework_name + " guid not found");
				}else{
					UnityEngine.Debug.LogWarning (framework_name + " guid:" + dylibGuid);
					// proj.AddDynamicFramework (targetGuid, dylibGuid);
					UnityEditor.iOS.Xcode.Extensions.PBXProjectExtensions.AddFileToEmbedFrameworks(proj, targetGuid, dylibGuid);

					proj.AddBuildProperty(targetGuid, "LD_RUNPATH_SEARCH_PATHS", "@executable_path/Frameworks");
					System.IO.File.WriteAllText (projPath, proj.WriteToString ());
				}
			}
		}
#endif
	}
}
```

###　2.　動的ライブラリ処理（Unity2019以前）

UnityEditor.iOS.Xcode.Extensionsは現在Unity 2019以降でのみ使用できます。以前のUnityバージョンでの使用については、上位バージョンのUnityからUnityEditor.iOS.Xcodeパッケージをエクスポートするか、添付ファイル[UnityEditorAV.iOS.XCode.zip](http://dldir1.qq.com/hudongzhibo/QCloud_TGP/GME/GME2.9.0/Other/UnityEditorAV.iOS.XCode.zip)を参照してこのファイルを展開し、Engineering Directory Editorフォルダに配置してもよい。

<img src="https://qcloudimg.tencent-cloud.cn/raw/a141d2c41dc4494148e9451d3d63cd38.png"  width="60%" /></img>

###　3.　Xcodeプロジェクトのエクスポート

Xcode10.0以降であることを確認し、UnityエディタでXcodeプロジェクトをエクスポートします。

### 4. bitcodeの無効化

コンパイル中に次のようなエラーが表示された場合は、Bitcodeを無効にしてください。この設定を無効化するには、**Targets**>**Build Settings**でBitcodeをサーチし、対応するオプションを見つけてからNOに設定すればよいです。
<img src="https://main.qcloudimg.com/raw/bcc77d7574e2d1861ca408cdd77dff00.png"  width="60%" /></img>

###　5.　iOSプラットフォームの権限を追加

- Required background modes：バックグラウンド実行が許容されます（オプション）。
- Microphone Usage Description：マイク権限が許容されます。

###　6.　補充ライブラリファイル

コンパイル中に次の図のエラーが発生した場合、ライブラリファイルを補完してください。
<img src="https://main.qcloudimg.com/raw/335c9d806cd2d5fe11b5f6a04a6fad80.png"  width="25%" /></img>
ライブラリファイルのリストは次のとおりです：
```
libc++.tbd
CoreMedia.framework
libresolv.tbd
AVFoundation.framework
Security.framework
CoreAudio.framework
AudioToolbox.framework
libiconv.tbd
libz.tbd
SystemConfiguration.framework
OpenAL.framework
```

###　7.　libresolv9.tbdを追加

次の図のエラーが発生した場合、

<img src="https://main.qcloudimg.com/raw/b8e40f601d9e8c1a62cf88bd10bdd241.png"  width="60%" /></img>

**UnityFramework**にlibresolv9.tbdを追加してください。

<img src="https://main.qcloudimg.com/raw/ee0a20a0b0ad99f30fa87855d1b17f0f.jpg"  width="60%" /></img>

### 8. エクスポート問題
エクスポートについては、[iOSエクスポート](https://intl.cloud.tencent.com/document/product/607/39522)をご参照ください。



## Androidプラットフォームからのエクスポート

###　1.　libファイルの削除

GME Unity SDKには、arm64-v8a、armeabi-v7aおよびx86のlibファイルがデフォルトで用意されています。プロジェクトの必要に応じて削除してください。
<dx-alert infotype="alarm" title="架构缺失">
指定されたアーキテクチャがないAndroid実行可能ファイルをエクスポートすると、Crashが発生します。
</dx-alert>
実行可能ファイルapkファイルをエクスポートした後、開くと黒画面となり、強制終了した場合、通常は適切なアーキテクチャのlibファイルがないので、プロジェクトに応じて追加または削除してください。

###　2.　権限設定
**2.1　必要な権限**
必ずプロジェクトのAndroidManifest.xmlファイルに下記の権限を追加してください。

```
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
```

**2.2　必要に応じて権限を追加**
必要に応じてプロジェクトのAndroidManifest.xmlファイルに、下記の権限を追加してください。
<dx-tabs>
:::　読み書き権限
読み書き権限の追加は必須ではありません。次のルールに基づいて追加するかどうかを判断します。

- デフォルトのログパス（/sdcard/Android/data/xxx.xxx.xxx/files）を使用している場合は、SetLogPathが呼び出されていないことを意味しますので、WRITE_EXTERNAL_STORAGE権限は必要ありません。
- SetLogPathインターフェースを呼び出してログパスを外部ストレージデバイスに配置し、音声メッセージ機能を使用した録音時のストレージパスは外部ストレージデバイスである場合は、WRITE_EXTERNAL_STORAGE権限をユーザーに要求し、ユーザーの明示的な承認を得る必要があります。

```
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```
:::
：：：　Bluetooth権限
Bluetooth権限の追加は、次のルールに従って決定する必要があります。

- プロジェクトのtargetSDKVersionは30以上の場合：
```
<uses-permission android:name="android.permission.BLUETOOTH"/>
```

- プロジェクトのtargetSDKVersionは31以降の場合：
```
<uses-permission android:name="android.permission.BLUETOOTH" android:maxSdkVersion="30" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
```
:::
</dx-tabs>


### 3. エクスポート問題
エクスポートについては、[Androidからのエクスポート](https://intl.cloud.tencent.com/document/product/607/39522)をご参照ください。


## Windowsプラットフォームのエクスポートについて

エクスポートについては、[Windowsからのエクスポート](https://intl.cloud.tencent.com/document/product/607/39522)をご参照ください。


## WebGLからのエクスポート

### 1. WebGL下のpluginsの設定
WebGLプラットフォームでのgmesdkと競合しないよう、Windowsプラットフォームでのgmesdk.dllの適用範囲を設定します。

<img src="https://qcloudimg.tencent-cloud.cn/raw/18870d8c1a15a496da1dc3fe3e579d45.png"  width="60%" /></img>

<img src="https://qcloudimg.tencent-cloud.cn/raw/4b697ba47fb49484989a1e201f2d7ee6.jpg"  width="60%" /></img>


### 2. Flare Layerの取消（Unity 2018以降）

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Gb53323_894943f084fc5aefc94c709e35d65d0e.png"  width="60%" /></img>

一部のUnityバージョンではMainCameraのFlare Layerモードをサポートしなくなるため、パッケージ化するSceneでFlare Layerのチェックを外す必要があります。チェックを外さない場合、次のエラーが表示されます：

<img src="https://qcloudimg.tencent-cloud.cn/raw/67506d24d1fef748b9ffbf6654ea27bc.png"  width="60%" /></img>


###　3.　テンプレートの選択
WebGLプラットフォームからエクスポートするときは、GMEのWebGLテンプレートを選択します。これにより、正常にパッケージ化された目的物が依存ライブラリに正しくインポートしていることが保証されます。プロジェクトでは、デフォルトでGMEWebGLTemplatesUnity2018テンプレートが使用されます。このテンプレートはUnity2018とUnity2019の両方のバージョンをサポートしています。Unity2020およびUnity2021のバージョンでは、パッケージ化の際に使用テンプレートを変更し、GMEWebGLTemplatesUnity2021を使用してパッケージ化する必要があります。
 
<img src="https://qcloudimg.tencent-cloud.cn/raw/def41a1210c286b47ddbe7dbeef1dd19.png"  width="60%" /></img>

###　4.　フロントエンドライブラリの導入
 
GME- WebGLを独自のプロジェクトにインポートする場合、Unityを使用して適切なWebページを生成する際には、フロントエンドライブラリを手動で導入し、フロントエンドライブラリファイルを適切な参照位置に配置し、Audioタグを追加する必要があります（下の図を参照）。Unityの目的物をパッケージ化するたびに上記の作業を自動的に行いたい場合は、GME-WebGL demoのやり方を参考にして、自分のプロジェクトに適切なテンプレートを追加してください。

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/j2Qx251_b939e1cd5e331579440c16672a59c2e1.png"  width="60%" /></img>


### 5. エクスポート問題
エクスポートについては、[Unity-WebGLからのエクスポート](https://intl.cloud.tencent.com/document/product/607/39522)をご参照ください。
