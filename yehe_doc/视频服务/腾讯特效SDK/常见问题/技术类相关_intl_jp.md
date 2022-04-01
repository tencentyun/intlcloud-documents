[](id:que1)
### Android releaseパッケージで、あるメソッドが見つからないというエラーが発生しましたが、解決するにはどうすればよいですか。
- releaseパッケージを作成する際、コンパイルの最適化を有効（minifyEnabledをtrueに設定）にしていると、javaレイヤーで呼び出されないコードがカットされる場合があります。これらのコードはnativeレイヤーで呼び出される場合があり、` no xxx method`の異常が生じることがあります。
- このようなコンパイル最適化を有効にしている場合は、これらのkeepルールを追加し、xmagicのコードがカットされないようにする必要があります。
```java
-keep class com.tencent.xmagic.** { *;}
-keep class org.light.** { *;}
-keep class org.libpag.** { *;}
-keep class org.extra.** { *;}
-keep class org.gyailib.** { *;}
-keep class com.tencent.cloud.iai.lib.** { *;}
```

[](id:que2)
### Android SDKをホストプロジェクトに統合するとgsonライブラリとの競合エラーが発生しましたが、解決するにはどうすればよいですか。
ホストプロジェクトの`build.gradle`ファイルに次のコードを追加します。

```
Android{
  configurations {
    all*.exclude group: 'com.google.code.gson'
  }
}
```

[](id:que3)
### iOSでのリソースインポート実行後のエラー：Xcode 12.Xバージョンのコンパイルで、「Building for iOS Simulator, but the linked and embedded framework '.framework'...」と表示されました。

**Build Settings** > **Build Options** > **Validate Workspace** でYesに変更し、再度**実行**をクリックします。
> ? Validate WorkspaceをYesに変更するとコンパイルが完了します。再びNoに変更しても正常に実行できます。そのため、ここではこの問題が発生した場合にのみ注意してください。

[](id:que4)
### フィルター設定が反応しません。
設定値が正しいかどうか確認してください。範囲は0～100ですが、値が小さすぎると効果がわかりづらい場合があります。

[](id:que5)
### iOS Demoのコンパイルで、dSYMを生成する際にエラーが発生します。
- **エラーメッセージ：**
```
PhaseScriptExecution CMake\ PostBuild\ Rules build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh
    cd /Users/zhenli/Downloads/xmagic_s106
    /bin/sh -c /Users/zhenli/Downloads/xmagic_s106/build/XMagicDemo.build/Debug-iphoneos/XMagicDemo.build/Script-81731F743E244CF2B089C1BF.sh

Command /bin/sh failed with exit code 1
```
- **問題の解析**：`libpag.framework`と`Masonary.framework`の再署名に失敗したことが原因です。
- **解決方法**：
	1. **demo/copy_framework.sh**を開きます。
	2. `$(which cmake)`をローカルcmakeの絶対パスに変更します。
	3. 署名`Apple Development: ......`をご自身のアカウントに変更します。

[](id:que6)
### iOS Demoで、メインページに進むと権限承認エラーと表示されます。
ログに表示された検証承認失敗のエラーコードを確認します。ローカルのLicenseファイルを使用している場合は、ファイルがプロジェクトに追加されているかをチェックします。

[](id:que7)
### iOS Demoのコンパイルにエラーが発生しました。
- **エラーメッセージ：**
```
unexpected service error: build aborted due to an internal error: unable to write manifest to-xxxx-manifest.xcbuild': mkdir(/data, S_IRWXU | S_IRWXG | S_IRWXO): Read-only file system (30):
```
- **解決方法**：
	1. **File** > **Project settings** > **Build System**で**Legacy Build System**を選択します。
	2. Xcode 13.0++の場合は**File** > **Workspace Settings**で**Do not show a diagnostic issue about build system deprecation**にチェックを入れます。


