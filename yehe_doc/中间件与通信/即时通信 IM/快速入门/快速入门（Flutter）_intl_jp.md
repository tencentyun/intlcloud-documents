ここでは、主にIM Demo（Flutter）を素早く実行する方法について説明します。

## 環境要件

| プラットフォーム | バージョン |
|---------|---------|
| Flutter | 2.2.0およびそれ以降のバージョン。 |
|Android|Android Studio 3.5以降のバージョン。Appの要件はAndroid 4.1以降のバージョンのデバイスです。|
|iOS|Xcode 11.0以降のバージョン。プロジェクトに有効な開発者署名を設定済みであることを確認してください。|

##  前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順
[](id:step1)

### 手順1：アプリケーションの作成
1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
>?アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから[キー情報の取得](#step2)を実行してください。
>同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)すると、新しいアプリケーションを作成することができます。**アプリケーションを削除した後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
>
2. **新しいアプリケーションの作成**をクリックし、**アプリケーションの作成**のダイアログボックスにアプリケーション名を入力し、**OK**をクリックします。
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID情報を保存してください。コンソールの概要ページで、作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、有効期限を確認できます。
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 作成後のアプリケーションをクリックし、左側のナビゲーションバーで**支援ツール**>**UserSig発行&チェック**をクリックすると、UserIDおよびそれに対応するUserSigが作成されます。署名情報をコピーし、後でログインして使用します。
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
### 手順2： SDKとソースコードのダウンロード
1. 実際の業務ニーズに応じて、SDKと付属の[Demoソースコード](https://github.com/tencentyun/TIMSDK/tree/master/Flutter/Demo/im_discuss)をダウンロードします。
2. ダウンロードが完了したら、ディレクトリ：TIMSDK/Flutter/Demo/im_discussに進みます。
![](https://qcloudimg.tencent-cloud.cn/raw/8b865854e14e8848b4e8d31d8daf55ac.png)
3. Flutter pub getで依存をインストールし、Demoプロジェクトを起動してコマンドラインに次のように入力します。
<dx-codeblock>
:::  plaintext
flutter run --dart-define=SDK_APPID=xxxx --dart-define=ISPRODUCT_ENV=false --dart-define=KEY=xxxx
:::
</dx-codeblock>
>?
>-  `--dart-define=SDK_APPID=xxxx`のうち、`xxxx`は[ステップ1](#step1)で作成したSDKAppIDにする必要があります。
>- `--dart-define=ISPRODUCT_ENV=false`は開発か本番環境かを判断します。開発環境の場合、falseとしてください。
>-  `--dart-define=KEY=xxxx`のうち、`xxxx`は[ステップ1](#step1)のキー情報にする必要があります。
4. Visual Studioでlaunch.jsonを設定して起動します。
![](https://qcloudimg.tencent-cloud.cn/raw/e495955902c8a594085aa045891ffe2a.png)


### ステップ3（オプション）：IDEを使用したデバッグの実行
<dx-tabs>
::: Androidプラットフォーム[](id:android)
1. Android Studioでdiscuss/andoridディレクトリを開きます。
![](https://qcloudimg.tencent-cloud.cn/raw/6516f9b17c58915c4ebc93c5c8829831.png)
2. Androidのエミュレーターを起動し、**Build And Run**をクリックすると、Demoが実行可能となります。ランダムなUserID（数字とアルファベットの組み合わせ）を入力できます。
>?UIは部分的に調整され更新される可能性があります。最新バージョンを基準としてください。
:::
::: iOSプラットフォーム[](id:ios)
1. Xcodeを開き、discuss/ios/Runner.xcodeprojファイルを開きます。
![](https://qcloudimg.tencent-cloud.cn/raw/6d74814ba9bce54c7439e8b3cea53e73.png)
2. iPhoneの実機に接続して、**Build And Run**をクリックします。iOSプロジェクトのコンパイルが終了すると、新しいウィンドウにXcodeプロジェクトが表示されます。
3. iOSプロセスを開き、メインTargetのSigning & Capabilities（Apple開発者アカウントが必要）を設定すると、プロジェクトをiPhoneの実機で実行可能になります。
4. プロジェクトを起動し、実機でDemoのデバッグを実行します。
![](https://qcloudimg.tencent-cloud.cn/raw/3fe6bbac88bb21ad7a7822bb297793b3.png)
:::
</dx-tabs>

## よくあるご質問

### サポートされているプラットフォームはどれですか。
現在iOS、AndroidおよびWebの3つのプラットフォームをサポートしています。また、WindowsとMacのバージョンも現在開発中です。どうぞご期待ください。

### AndroidでBuild And Runをクリックすると、使用できるデバイスが見つからないというエラーが発生します。
デバイスが他のリソースに使用されないことを保証するか、または**Build**をクリックしてAPKパッケージを生成してから、エミュレーター内にドラッグして実行します。

### iOSで初回実行時にエラーが発生します。
上のDemoで設定を実行した後もエラーが発生する場合、**Product** > **Clean**をクリックし、プロダクトを削除してから改めてBuildするか、またはXcodeをオフにして改めて開いて再度Buildします。

### Flutter環境の問題
Flutterの環境に問題のないことを確認する場合、Flutter doctorを実行してFlutter環境が適切にインストールされているかチェックしてください。
