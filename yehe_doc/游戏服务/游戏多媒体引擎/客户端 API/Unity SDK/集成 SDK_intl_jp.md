Unityを使う開発者たちがTencent Cloud Gaming Multimedia Engineの製品APIのデバッグ・アクセスを手軽に実行できるように、Unityでの開発に向けるプロジェクト設定について説明します。


## SDK のダウンロード

1.　DemoおよびSDKをダウンロードしてください。ダウンロードリンクの詳細については、[SDK ダウンロードガイド]（https://intl.cloud.tencent.com/document/product/607/18521）をご参照ください。
2.　インターフェースでUnityバージョンのSDKリソースを見つけます。
3. **ダウンロード**をクリックします。ダウンロードしたSDKリソースを解凍後に次の内容が含まれます。ファイル説明は下表のとおりです：
<table>
<thead>
<tr>
<th>ファイル名</th>
<th align="center">説明</th>
<th>作用</th>
</tr>
</thead>
<tbody><tr>
<td>Plugins</td>
<td align="center">SDKライブラリファイル</td>
<td>各プラットフォームからエクスポートされるライブラリファイルを格納します</td>
</tr>
<tr>
<td>GMESDK</td>
<td align="center">SDKコードファイル</td>
<td>APIインターフェースの提供</td>
</tr>
</tbody></table>
4.　HD音質を使用している場合は、[UnityのHD音質ドキュメント設定](https://intl.cloud.tencent.com/document/product/607/46016)をご参照ください。

<dx-alert infotype="explain" title="平台支持">
Unity SDKは、Windows、Mac、Android、iOS、PlayStation、Xbox、Switch、WebGLのプラットフォームアーキテクチャを同時に統合しています。
</dx-alert>



## プロジェクトの設定手順

### ステップ1： Pluginsファイルのインポート

下図に示すように、SDKにあるPluginsフォルダーのファイルを、**Unityプロジェクト**>**Assets**>**Plugins**フォルダーにコピーします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/ce8ba3561d43148971f1cbe9076be3a3.png"  width="65%" /></img>



<dx-alert infotype="explain" title="">
win32アーキテクチャの実行可能ファイルをエクスポートしない場合は、Pluginsフォルダの下にあるx86フォルダを削除してください。
</dx-alert>




### ステップ2：コードファイルのインポート

SDKにあるScripts フォルダーのファイルを、 Unityプロジェクトのコード保存フォルダーにコピーします、下図の通りです：  
<img src="https://qcloudimg.tencent-cloud.cn/raw/5ab4509590a5effa9e8aadeee2456492.png"  width="65%" /></img>



##　Unity2021の設定
使用しているUnity EditorがUnity 2021以降の場合は、Plugins>Android>Opensdk.pluginの下にあるlibフォルダを切り取って、プロジェクトのPluginsファイル内のAndroidディレクトリ（Opensdk.pluginと同じレベル）に置く必要があります。

<img src="https://qcloudimg.tencent-cloud.cn/raw/bc7156db71faf994654c824787bfb1a9.png"  width="65%" /></img>


## オーディオ設定

図に示すように、Unityエディッターでは、**Edit**>**Project Setting**>**Audio**はシステムデフォルトを使ってよいです。修正すると、Unity再生サウンドエフェクトはiOSにおけるハードキャッシュエリアの設定に影響されます、表現としてはサウンドエフェクトが中断されてしまいます。
<img src="https://main.qcloudimg.com/raw/db8975fcaefa3dc71732ede1b5f979db.png"  width="50%" /></img>


<dx-alert infotype="forbid" title="Unity Audio Setting">
Project SettingでAudioモジュールの設定を禁止します。
</dx-alert>

下の図に示すようなモードに設定された場合、Unityの効果音再生は、iOSでハードキャッシュエリアの設定に影響されます。表現としては効果音が中断されてしまします。次の図をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/6eb910221b8a24289dcffe0a39d60573.png)

##　MacOSプラットフォーム使用操作

MacOS　10.15.xでGME SDKを統合したUnityを使用し、実行時にファイル破損エラーが表示されます。これは`com.apple.quarantine`属性が原因となります。

最も直接的な解決策は、次の手順で`com.apple.quarantine`属性を削除します。
1.　端末でcdコマンドを実行し、プロジェクト内のフォルダ`Unity_OpenSDK_Audio/Assets/Plugins/`にすばやく移動します。
2. 次のコマンドを実行します。
```
$ xattr -d com.apple.quarantine gmesdk.bundle
```



<dx-alert infotype="explain" title="">
この操作にはリスクがあるので、古いバージョンのMacOSを使用してアクセスすることをお勧めします。
</dx-alert>


