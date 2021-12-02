ここでは、主にTencent Cloud IM Demo（Unity)を素早く実行する方法をご紹介します。

## 環境要件

| プラットフォーム | バージョン |
|---------|---------|
| Unity | 2019.4.15f1以降のバージョン。 |
|Android|Android Studio 3.5以降のバージョン。Appの要件はAndroid 4.1以降のバージョンのデバイスです。|
|iOS|Xcode 11.0以降のバージョン。プロジェクトに有効な開発者署名を設定済みであることを確認してください。|

## 前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順
[](id:step1)
## 手順1：アプリケーションの作成
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
## 手順2： SDKとソースコードのダウンロード
1. 実際のサービス要求に基づいて、SDKと付属の[Demoソースコード](https://intl.cloud.tencent.com/document/product/1047/33996)をダウンロードします。
2. ダウンロード完了後、Packageをダブルクリックして開くと、デフォルトではパッケージリソースがすべて選択されており、現在のUnityプロジェクトにインポートされます。
![](https://main.qcloudimg.com/raw/c338ce838fff81841f85b06fd3dc5c6c.png)
3. ソースコードAssets/TIMCloud/Demo/ExampleEntry.csを開き、[手順1](#step1)で取得したSDKAppID、UserID、UserSigを以下画像の赤枠内に入力し、Config.keyのある行のコメントを削除します。
![](https://main.qcloudimg.com/raw/e31692ae98503221f45ece41039ead92.png)
4. ExampleEntry.csのコメントはuserSigロジックを動的取得します（動的取得の設定はやや複雑であるため、後で独自に設定する必要があります）。
![](https://main.qcloudimg.com/raw/7a8ac734ac60a73caf6139fc0d1d250f.png)

## 手順3：パッケージ化の実行
### Androidプラットフォーム
1. Unity Editorを設定して、**File**>**Build Setting**をクリックし、Androidに切り替えます。
![](https://main.qcloudimg.com/raw/d913d32e36aa01ff93acf0316d4f103f.png)
2. Androidのエミュレーターを起動して、**Build And Run**をクリックすると、Demoを実行できます。

>- Demo内にはアップロード済みのAPIのすべてが含まれており、テストおよび参考のために呼び出すことができます。APIドキュメントについては[SDK API（Unity）](https://intl.cloud.tencent.com/document/product/1047/40125)をご参照ください。
> - UIは部分的に調整され更新される可能性があります。最新バージョンを基準としてください。
>
![](https://main.qcloudimg.com/raw/e6f3583d0b807af62a27ee753cfa3b53.png)
3. インターフェースをテストします。まず1行目2つ目の入力ボックス内にUserIDを追加してから、initSDKとloginをコールします。データ表示ウィンドウにコールの成功が表示されると、基本的にインターフェースのコールを試すことができます。

### iOSプラットフォーム
1. Unity Editorを設定して、**File**>**Build Setting**をクリックし、iOSに切り替えます。
![](https://main.qcloudimg.com/raw/3982b96c4f9e76107bb4aadac33a5de5.png)
2. iPhoneの実機に接続して、**Build And Run**をクリックします。1つの新しいディレクトリを選択して、コンパイルされたiOSプロジェクトに保存する必要があります。コンパイルが終了すると、新しいウィンドウにXcodeプロジェクトが表示されます。
3. iOSプロセスを開き、メインTargetのSigning & Capabilities（Apple開発者アカウントが必要）を設定すると、プロジェクトをiPhoneの実機で実行可能になります。
4. プロジェクトを起動し、実機でDemoのデバッグを実行します。

## よくあるご質問

### サポートされているプラットフォームはどれですか。
現在iOSとAndroidの2つのプラットフォームをサポートしています。また、WindowsとMacのバージョンも現在開発中です。どうぞご期待ください。

### AndroidでBuild And Runをクリックすると、使用できるデバイスが見つからないというエラーが発生します。
デバイスが他のリソースに使用されないことを保証するか、またはBuildをクリックしてapkパッケージを生成してから、エミュレーター内にドラッグして実行します。

### iOSで初回実行時にエラーが発生します。
上のDemoで設定を実行した後もエラーが発生する場合、**Product**>**Clean**をクリックし、プロダクトを削除してから改めてBuildするか、またはXcodeをオフにして改めて開いて再度Buildします。
### 2019.04バージョンのUnity、iOSプラットフォームでエラーが発生します。
Library/PackageCache/com.unity.collab-proxy@1.3.9/Editor/UserInterface/Bootstrap.cs(23,20): error CS0117: 'Collab' does not contain a definition for 'ShowChangesWindow'
Editorツールバーで**Window**>**Package Manager**をクリックし、Unity Collaborateを1.2.16にダウングレードします。

### 2019.04バージョンのUnity、iOSプラットフォームでエラーが発生します。
Library/PackageCache/com.unity.textmeshpro@3.0.1/Scripts/Editor/TMP_PackageUtilities.cs(453,84): error CS0103: The name 'VersionControlSettings' does not exist in the current context
ソースコードを開き、`|| VersionControlSettings.mode != "Visible Meta Files"`の部分のコードを削除すれば完了です。
