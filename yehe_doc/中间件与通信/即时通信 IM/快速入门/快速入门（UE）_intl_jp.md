ここでは、主にTencent Cloud IM Demo（Unreal Engine）を素早く実行する方法について説明します。

>?現時点ではWindows、macOS、iOS、Androidをサポートしています。

## 環境要件
Unreal Engine 4.27.1およびそれ以降のバージョンを推奨します。
<table>
   <tr>
      <th width="0px" style="text-align:center">開発端末</td>
      <th width="0px" style="text-align:center">環境</td>
   </tr>
   <tr>
      <td>Android</td>
      <td><li>Android Studio 4.0およびそれ以降のバージョン。</li><li>Visual Studio 2017 15.6およびそれ以降のバージョン。 </li><li>実機デバッグのみサポートしています。                    </li></td>
   </tr>
   <tr>
      <td>iOS & macOS</td>
      <td><li>Xcode 11.0およびそれ以降のバージョン。                   </li><li>OSXシステムバージョンは10.11およびそれ以降のバージョン。       </li><li>プロジェクトに有効な開発者署名を設定済みであることを確認してください。   </li></td>
   </tr>
   <tr>
      <td>Windows</td>
      <td><li>OS：Windows 7 SP1およびそれ以降のバージョン（x86-64ベースの64ビットOS）。                    </li><li>ディスク容量：IDEおよびいくつかのツールのインストールの他、少なくとも1.64GBの空きがある必要があります。                            </li><li><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Visual Studio 2019</a>のインストール。        </li></td>
   </tr>
</table>

##  前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順
[](id:step1)
### 手順1：アプリケーションの新規作成
1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
>?アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから[キー情報の取得](#step2)を実行してください。
>同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)すると、新しいアプリケーションを作成することができます。**アプリケーションを削除した後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
>
2. **新しいアプリケーションの作成**をクリックし、**アプリケーションの作成**のダイアログボックスにアプリケーション名を入力し、**OK**をクリックします。
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. 作成が完了すると、コンソールの概要ページで、作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、タグおよび有効期限を確認できます。SDKAppID情報を記録してください。
![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)

[](id:step2)

### ステップ2：キー情報の取得
1. 対象のアプリケーションカードをクリックし、アプリケーションの基本設定画面に移動します。
![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
2. **基本情報**セクションで、**表示キー**をクリックし、キー情報をコピーして保存します。
>!キー情報を適切に保管して、漏えいしないようにしてください。

[](id:step3)
### ステップ3：Demo プログラムファイルの設定
1. IM Demoプログラムをダウンロードします。ダウンロードアドレスは[Demoダウンロード](https://github.com/tencentyun/IMUnrealEngine)をご参照ください（ご不明な点がございましたら、QQグループにご参加の上、764231117にお問い合わせください）。
2. `/IM_Demo/Source/debug/include/DebugDefs.h`ファイルを見つけて開きます。
3. `DebugDefs.h`のファイルの関連パラメータを設定します。
<ul><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
	<li/>SECRETKEY：デフォルトは""。実際のキー情報を設定してください。</ul>


>?
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- 正しい UserSigの発行方法は、 UserSig の計算コードをお客様のサーバーに統合して、App向けのインタフェースを用意し、UserSig を必要とするときは、App から業務サーバーにリクエストを出して、ダイナミックUserSigを取得することです。より詳細な内容については、 [サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

[](id:step4)
### 手順4：コンパイルとパッケージ化の実行
1. `/IM_Demo/IM_Demo.uproject`をダブルクリックして開いてください。
2. コンパイルを実行し、デバッグを行います。
<dx-tabs>
::: macOS\s端末
**File** -> **Package Project** -> **Mac**
:::
::: Windows\s端末
**File**->**Package Project**->**Windows**->**Windows(64-bit)**
![](https://imgcache.qq.com/operation/dianshi/other/win.ba79ccce59ae58718e6c35c16cdef55531456a70.png)
:::
::: iOS\s端末
プロジェクトをパッケージ化します
**File** -> **Package Project**-> **iOS**
:::
:::  Android\s端末
1. 開発とデバッグ：[Androidクイックスタート](https://docs.unrealengine.com/4.27/en/SharingAndReleasing/Mobile/Android/GettingStarted/)をご参照ください。
2. プロジェクトのパッケージ化：[Androidプロジェクトのパッケージ化](https://docs.unrealengine.com/4.27/en/SharingAndReleasing/Mobile/Android/PackagingAndroidProject/)をご参照ください。
:::
</dx-tabs>

## IM Unreal Engine APIドキュメント
その他のインターフェースについては、[API概要](https://im.sdk.qcloud.com/doc/en/md_introduction_CPP%E6%A6%82%E8%A7%88.html)をご参照ください。

## よくあるご質問

### Android“Attempt to construct staged filesystem reference from absolute path"”エラー
UE4プロジェクトを閉じて、CMDを開き、次のコマンドを実行します。

<dx-codeblock>
:::  cmd
adb shell

cd sdcard

ls (you should see the UE4Game directory listed)

rm -r UE4Game
:::
</dx-codeblock>

プロジェクトを再コンパイルします
