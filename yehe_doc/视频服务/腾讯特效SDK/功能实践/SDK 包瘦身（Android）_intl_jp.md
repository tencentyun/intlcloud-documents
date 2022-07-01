パケットのサイズを小さくするために、SDKに必要なassetsリソース、soライブラリ、およびダイナミックエフェクトリソースMotionRes（一部のベーシック版SDKにはダイナミックエフェクトリソースはありません）をネットワークからのダウンロードに変更することができます。ダウンロード完了後、上記ファイルのパスをSDKに設定します。

Demoのダウンロードロジックを再利用することをお勧めします。当然のことながら、既存のダウンロードサービスを使用することもできます。

Demoのダウンロードロジックを再利用する場合は、次の点に注意してください：Demoでは、ブレークポイントからのダウンロード再開機能がデフォルトで有効になっています。これにより、ダウンロードが異常に中断された場合、次回の時に中断された場所から引き続きダウンロードできます。ブレークポイントからのダウンロード再開機能を有効にする場合は、ダウンロードサーバーがブレークポイントからのダウンロード再開機能をサポートしていることを確認してください。 

**検査方法**

```java
サーバーがブレークポイントからのダウンロード再開機能をサポートしているかどうかを判断するには、WebサーバーがRangeリクエストをサポートしているかどうかを確認してください。テスト方法は、コマンドラインで以下のcurlコマンドを実行することです：
curl -i --range 0-9 https://您的服务器地址/待下载的文件名
例：
curl -i --range 0-9 https://mediacloud-76607.gzc.vod.tencent-cloud.com/TencentEffect/Android/2.4.1.119/xmagic_S1-04_android_2.4.1.119.zip
返された内容にContent-Rangeフィールドがある場合は、サーバーがブレークポイントからのダウンロード再開機能をサポートしていることを意味します。
```

[](id:so)

## soのダイナミックダウンロード
下図に示すように、so圧縮パッケージは `jniLibs/arm64-v8a`と`jniLibs/armeabi-v7a`にあります：
![](https://qcloudimg.tencent-cloud.cn/raw/785d9f1a64b556343ea8959f14fec646.png)


<dx-tabs>
::: Demoでダウンロードサービスを再利用したい場合
1. 2つのZIPパッケージのMD5値を計算します。Macでは、コマンドラインで`md5ファイルパス/ファイル名`を使用して直接MD5を計算することができます。または他のツールソフトウェアで計算することもできます。
2. 圧縮パッケージをサーバーにアップロードして、ダウンロードURLを取得します。
3. DemoプロジェクトのResDownloadConfigにある次の定数値を更新します：
![](https://qcloudimg.tencent-cloud.cn/raw/2c6e6b4e36eca9a7b17181f567efe01c.png)
4. `ResDownloadUtil.checkOrDownloadFiles`を呼び出すことで、ダウンロードを開始します。
:::
::: 自分でダウンロードサービスをしたい場合
1. ダウンロードを完了して解凍してから、SDKで解凍後のパスを設定してください。例：解凍完了後：`soのpath = /data/data/com.tencent.pitumotionDemo.effects/files/xmagic_libs`
<img src="https://qcloudimg.tencent-cloud.cn/raw/c4ee096758d599be54310d740c5026d4.png" width=400px>
>! 　クリーンアップソフトウェアによって誤って削除された場合に備えて、外部ストレージではなくアプリのプライベートディレクトリにダウンロードすることを強くお勧めします。同時に、ユーザーの携帯電話のCPUタイプによって、必要に応じてv8aまたはv7aをダウンロードし、ダウンロード速度を向上させることをお勧めします。ここでは、DemoプロジェクトのLaunchActivityのメソッドを参照できます。
2. 以下のコードを呼び出したら、soの読み込みとLicenceの認証は完了します。
```java
XmagicApi.setLibPathAndLoad(path);
auth();
```
:::
</dx-tabs>

>! 
>- SDKのバージョン更新により、対応するsoが変更される可能性があります。そのため、これらのsoを再度ダウンロードしてください。Demoのメソッドを参照し、検証にMD5を使用することをお勧めします。
>- 自分でsoをダウンロードするか、Demoのダウンロードサービスを再利用するかにかかわらず、SDKのauthインターフェースを呼び出す前に、soがダウンロードされているかどうかを先に確認してください。ResDownloadUtilは、以下の確認方法を提供しています。すでにダウンロードされている場合は、SDKでパスを以下のように設定します：
```java
String validLibsDirectory = ResDownloadUtil.getValidLibsDirectory(LaunchActivity.this,

isCpuV8a() ? ResDownloadConfig.DOWNLOAD_MD5_LIBS_V8A : ResDownloadConfig.DOWNLOAD_MD5_LIBS_V7A);
if (validLibsDirectory == null) {
     Toast.makeText(LaunchActivity.this,"libsがダウンロードされていない場合は先にダウンロードしてください",Toast.LENGTH_LONG).show();
     return;
}
XmagicApi.setLibPathAndLoad(validLibsDirectory);
auth();
```


## assetsリソースのダイナミックダウンロード
assetsリソースのダイナミックダウンロードについての具体的な操作は以下のとおりです：

1. ローカルプロジェクトのassetsで構成を行います。
     - **2.4.0以降のバージョン**：ローカルassetsのディレクトリにファイルを保存する必要はありません。
     - **2.4.0より前のバージョン**：Licenseファイルと`brand_name.json`、`device_config.json`、`phone_info.json`、`score_phone.json`の4つのJSON構成ファイルを保存してください。
2. SDKでパッケージ化された`download_assets.zip`を見つけます。
![](https://qcloudimg.tencent-cloud.cn/raw/b04e8d991a4aef086229a8610ad8f883.png)
3. [上記のsoファイル](#so)の処理方法と同じように、このZIPパッケージのMD5を計算し、サーバーにアップロードしてダウンロードアドレスを取得します。
<dx-tabs>
::: Demoでダウンロードサービスを再利用したい場合
1. 下図に示すダウンロードアドレスとMD5を更新します。
![](https://qcloudimg.tencent-cloud.cn/raw/a59277a9a3a9d5c000b103fce7ea2885.png)
2. `ResDownloadUtil.checkOrDownloadFiles`を呼び出してダウンロードを開始し、ResDownloadUtil.getValidAssetsDirectory`を呼び出してダウンロード後のassetsのパスを取得します。詳しい方法については、`LaunchActivity.java`をご参照ください。
:::
::: 自分でダウンロードサービスをしたい場合
上記のZIPパッケージをダウンロードして解凍した後、パッケージ内のファイルの構造を再構成する必要があります。最終的なファイル構造は以下のとおりです：
<img src="https://qcloudimg.tencent-cloud.cn/raw/8ad5eeb526671bea433967c91aa377bc.png" width=400px>
そのうち、赤枠内のlight_assets、light_materialなどの名前は任意に変更できません。ResDownloadUtillのorganizeAssetsDirectoryメソッドを直接再利用して、整理を完了することをお勧めします。
:::
</dx-tabs>

>! 
>- SDKのバージョン更新により、対応するassetsが変更される可能性があります。互換性を確保するために、これらのassetsを再度ダウンロードしてください。Demoのメソッドを参照し、検証にMD5を使用することをお勧めします。
>- 自分でassetsをダウンロードするか、Demoのダウンロードサービスを再利用するかにかかわらず、撮影する前に、assetsがダウンロードされているかどうかを先に確認してください。ResDownloadUtilは、以下の確認方法を提供しています。すでにダウンロードされている場合は、XmagicResParserでパスを設定します。詳しい方法については、`LaunchActivity.java`をご参照ください。
```java
String validAssetsDirectory = ResDownloadUtil.getValidAssetsDirectory(LaunchActivity.this,ResDownloadConfig.DOWNLOAD_MD5_ASSETS);
if (validAssetsDirectory == null) {
      Toast.makeText(LaunchActivity.this,"assetsがダウンロードされていない場合は先にダウンロードしてください",Toast.LENGTH_LONG).show();
      return;
}
XmagicResParser.setResPath(validAssetsDirectory);
startActivity(intent);
```

## ダイナミックエフェクトリソースMotionResのダウンロード
一部のベーシックパッケージにはダイナミックエフェクトリソースがありません。この場合は、このセクションをスキップしてもかまいません。

ダイナミックエフェクトは6つのカテゴリーに分類され、それぞれに複数のZIPパッケージがあり、各ZIPパッケージは1種類のダイナミックエフェクトです。購入したパッケージタイプによって、そのファイルの内容は異なります。
![](https://qcloudimg.tencent-cloud.cn/raw/e289586793242d7a9b363b42cacb0f38.png)
ダイナミックエフェクトリソースは、必要に応じて（たとえば、ユーザーが関連する機能ページに入った後、またはダイナミックエフェクトのアイコンをクリックした後など）ダウンロードできます。

これらのZIPパッケージをサーバーにアップロードし、各ZIPパッケージのダウンロードアドレスを取得する必要があります。
>!**ダイナミックエフェクトリソースのダウンロード後のディレクトリMotionResは、前のセクションのlight_assetsおよびlight_materialと同じレイヤーにある必要があります**。また、下図に示すように、ZIPパッケージを直接配置するのではなく、各エフェクトを解凍してください：
![](https://qcloudimg.tencent-cloud.cn/raw/96876dfb2d76901b4e20a3847b0be280.png) 

MotionResをダウンロードするには、ResDownloadUtil.checkOrDownloadMotionsメソッドをご参照ください。必要に応じて1つずつダウンロードすることをお勧めします。

**Demoでダウンロードサービスを再利用したい場合は、ResDownloadConfigのMOTION_RES_DOWNLOAD_PREFIX定数値を自分のダウンロードURLのプレフィックスに置き換えてください。**