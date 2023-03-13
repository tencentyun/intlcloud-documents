
## iOSプラットフォームのエクスポートについて
### Xcodeで実行可能なファイルをエクスポートするとき、`GMESDK.framework` ライブラリがすでに追加されています。しかし、コンパイル時にエラーが発生しました。どのようにして解決しますか？

プロジェクトファイルからBuild Settingを選択し、"Other Linker Flags"に“-all_load” フラグが使用されていれば、それを削除してから再コンパイルしてください。


### UnityからXCodeプロジェクトをエクスポートした後、`framework not found GMESDK`エラーが発生しました。どのようにして解決できますか？

Unityエンジンを使用する場合、GME Unity SDKを導入し`libGMESDK.a`ライブラリを使用してください。frameworkファイルを使用する必要はありません。

### Unity SDKを使用した場合、iOS実行可能なファイルをエクスポートする時にエラーが発生し、armv7に関係している旨のメッセージが出力されました。armv7を削除した後、正常に利用できます。どのようにして解決できますか？

- Unityをアップグレードすることをお勧めします。詳しくは、[Unity公式サイト](https://forum.unity.com/threads/undefined-symbols-for-architecture-armv7-query_call_back-callback_func_type.830544/#post-5590516)をご参照ください。
- アップグレードする必要がなければ、armv7アーキテクチャーをパッケージングしないでください。

### iOS Demoをダウンロードしましたが実行できません。どのようにして解決できますか？

公式のiOS Demoをダウンロードした後、Xcode（バージョンが10以降）でコンパイルする時に、`ld: warning: directory not found for option`などのエラーが発生します。この場合、Demoと同じレベルのディレクトリ配下の「GME_SDK」フォルダ中の「GMESDK.framework」ファイルをプロジェクトのFrameworkリストに手動で追加してください。


### iOS SDKはエミュレーターによるデバッグをサポートしますか？

サポートします。公式サイトで提供された[最新パッケージ](https://intl.cloud.tencent.com/document/product/607/18521)を使用して検証してください。

### Demoをエクスポートする時、証明書エラーが発生しました。どのように解決できますか？
エラーメッセージは以下のとおりです：
```
Showing Recent Messages:-1: Unity-iPhone has conflicting provisioning settings. Unity-iPhone is automatically signed, but code signing identity iPhone Distribution: Tencent Technology (Shenzhen) Co., Ltd has been manually specified. Set the code signing identity value to "iPhone Developer" in the build settings editor, or switch to manual signing in the project editor. (in target 'Unity-iPhone')
```
ソリューション：
物理デバイスでエクスポートする時、お客様ご自身の開発者証明証でTencent Cloudのエンタープライズ証明書を置き換えます。


### エクスポートする時、以下のエラーが発生しました。どうすればいいですか？
エラーメッセージは以下のとおりです：
```
dyld: Library not loaded: @rpath/libLamemp3.framework/libLamemp3
Referenced from: /private/var/containers/Bundle/Application/XXXX
Reason: image not found
dyld: launch, loading dependent libraries
DYLD_LIBRARY_PATH=/usr/lib/system/introspection
DYLD_INSERT_LIBRARIES=/Developer/usr/lib/libBacktraceRecording.dylib:/Developer/usr/lib/libMainThreadChecker.dylib:/Developer/Library/PrivateFrameworks/DTDDISupport.framework/libViewDebuggerSupport.dylib
```
ソリューション：
- 動的ライブラリを使用した場合、ロードした動的ライブラリはデフォルトで静的ライブラリ`Linked Frameworks and Libraries`の配下に存在します。動的ライブラリを選択し、その下の`-`をクリックして削除します。その後、`Embedded Binaries`の下の`+`をクリックして動的ライブラリを追加します。
- または、下図に示すようにframeworkを変更します。
![](https://main.qcloudimg.com/raw/fe01a75aba37436d4cae1dd68b3b9640.jpg)


## Windowsプラットフォームのエクスポートについて

### Unity Demoをダウンロードし、実行可能なPCファイルをエクスポートするときにエラーが発生しました。どうすればいいですか？

使用中に`Found plugins with same names and architectures`のようなエラーが発生した場合、その原因は、GME SDKがデフォルトでx86向けSDKとx86_64向けSDKともに提供しているためです。pluginsフォルダからどちらかを削除してください。


### Unreal Demoをダウンロードし、実行可能なPCファイルをエクスポートするとき、dllが見つからない旨のエラーメッセージが出力されました。どうすればいいですか？

Windows x64バージョンのエクスポートを例として説明します。実行可能なファイルをエクスポートした後、プロジェクトディレクトリ `UEDemo1\Plugins\GMESDK\Source\ThirdParty\GMESDKLibrary\x64`配下のdllファイルを全部、実行可能なファイル（.exe）が所在するディレクトリにコピーします。

## Androidプラットフォームのエクスポートについて

### GME SDKを統合しApkをエクスポートした後、プログラムを起動するとブラックスクリーンになりました。どのようにして解決できますか？

一部のlibファイルがないためこの問題が発生しました。Apkを解凍して、lib配下の各フォルダに不足するライブラリファイルがあるかを確認してください。

### Androidスマートフォンにエクスポートした後、Appをクリックと当該デバイスをサポートしない旨のエラーメッセージが出力されました。どのようにして解決できますか？

これは、パッケージングした実行ファイルに含まれたアーキテクチャーによって発生します。v8aアーキテクチャーを必要としなければ、Unityプロジェクト設定のエクスポート欄でv8aのチェックを外してください。

### エクスポートしたApkはエミュレーターをサポートしません。どうすればいいですか？

エクスポートしたApkにx86を含んだライブラリファイルがあるかをチェックしてください。ない場合、SDKを再ダウンロードしx86向けのSDKファイルを導入してから、実行可能なファイルを改めてエクスポートしてください。




## Unity-WebGLエクスポート問題

### Unity-WebGLプラットフォームはhttpsプロトコルまたはhttpプロトコルを使用しますか。
パッケージ化された製品は、**httpsプロトコル**を使用してデプロイする必要があります。サーバーへのデプロイにhttpプロトコルを使用すると、機能が異常になります。

### Unity-WebGLプラットフォームのパッケージ化後、入室時に1004エラーが発生します。
入力されたOpenidが10000未満であるため、チェックイン時に1004（Invalid Argument）エラーが報告されます。ここに入力する必要がある**Openidは10000を超えています**。

### Unity-WebGLプラットフォームはパッケージ化後、携帯電話で使用できますか？
Unityの公式サイトによると、Unity-WebGLによりパッケージ化された製品は現在、携帯電話での動作をサポートしません。詳しくは[Unity - Manual: WebGL Browser Compatibility (unity3d.com)](https://docs.unity3d.com/2020.1/Documentation/Manual/webgl-browsercompatibility.html)をご参照ください。

### Unity-WebGLプラットフォームはパッケージ化後、GME範囲音声機能を使用できますか？
WebGLプラットフォームは現在、最も簡単なリアルタイム音声通話機能（チェックインとチェックアウト、マイクオンとマイクオフ機能）のみをサポートしています。サポートされていない機能の場合は、呼び出しインターフェースからエラーコード1006が返されます。範囲音声機能は現在、WebGLプラットフォームに適応しています。
