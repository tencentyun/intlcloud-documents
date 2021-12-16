このドキュメントでは、インスタントメッセージングIMの体験Demoを迅速に実行する方法をご紹介します。



## ステップ1. アプリケーションの作成
1. [インスタントメッセージングIMコンソール](https://console.cloud.tencent.com/im)にログインします。
 >?作成済みのアプリケーションがある場合は、そのアプリケーションのSDKAppIDを記録し、[キー情報を取得](#step2)します。
 >同じTencent Cloudアカウントで、最大300個のインスタントメッセージングIMアプリケーションを作成できます。すでに300個のアプリケーションがある場合は、新しいアプリケーションを作成する前に、不要になったアプリケーションを[無効化して削除](https://intl.cloud.tencent.com/document/product/1047/34540)することができます。**なお、アプリケーションを削除すると、そのアプリケーションのSDKAppIDに関連付けられているデータやサービスはすべてリカバーできなくなりますので、慎重に操作してください。**
 >
2. 地域を選びましょう。
3. **新しいアプリケーションを追加**をクリックします。
4. **アプリケーションを作成**のダイアログボックスが表示されたら、アプリケーション名を入力し、**OK**をクリックします。
    作成後、コンソールの[概要]ページで、新規作成のアプリケーションの状態、サービスバージョン、SDKAppID、作成時間、有効期限を確認できます。SDKAppID情報を記録してください。



## ステップ2：キー情報の取得

1. 対象のアプリケーションカードをクリックし、[アプリケーションの基本設定]ページに進みます。
2. **基本情報**セクションで**キーを表示**をクリックし、キー情報をコピーして保存します。
 >!キー情報は第三者に知られないように適切に保管してください。


## ステップ3：Demoソースコードをダウンロードして設定します。

1. インスタントメッセージングIMのDemoプロジェクトをダウンロードします。具体的なダウンロードアドレスについては、[SDKのダウンロード](https://intl.cloud.tencent.com/document/product/1047/33996)をご覧ください。
2. お使いのデバイスのディレクトリで該当のプロジェクトを開き、対応する`GenerateTestUserSig`ファイルを見つけます。
 <table>
     <tr>
         <th nowrap="nowrap">使用しているプラットフォーム</th>  
         <th nowrap="nowrap">ファイル相対パス</th>  
     </tr>
  <tr>      
      <td>Android</td>   
      <td>Android/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java</td>   
     </tr> 
  <tr>
      <td>iOS</td>   
      <td>iOS/TUIKitDemo/TUIKitDemo/Debug/GenerateTestUserSig.h</td>
     </tr> 
  <tr>      
      <td>Mac</td>   
      <td>Mac/TUIKitDemo/TUIKitDemo/Debug/GenerateTestUserSig.h</td>   
     </tr>  
  <tr>      
      <td>Windows</td>   
      <td>cross-platform/Windows/IMApp/IMApp/GenerateTestUserSig.h</td>   
     </tr>  
  <tr>      
      <td>Web（一般）</td>   
      <td>H5/dist/debug/GenerateTestUserSig.js</td>   
     </tr>  
  <tr>      
      <td>ウィジェット</td>   
      <td>WXMini/dist/wx/debug/GenerateTestUserSig.js</td>   
     </tr>  
</table>
3.`GenerateTestUserSig`ファイル内の関連パラメータを設定します。
 >?このドキュメントでは、Android Studioを使用してAndroidプロジェクトを開くケースを例に説明します。
  >
 - SDKAPPID：[ステップ1](#step1)で取得した実際のアプリケーションSDKAppIDに設定してください。
 - SECRETKEY：[ステップ2](#step2)で取得した実際のキー情報に設定してください。


>!このドキュメントに記載されているUserSigを取得するための方法では、クライアント側のコードでSECRETKEYを設定します。この方法では、SECRETKEYを簡単に逆コンパイルして逆ハッキングできます。キーが漏洩してしまうと、攻撃者がTencentCloudトラフィックを盗用する可能性があります。したがって、**この方法は、ローカルで実行するDemoと機能のデバッグにのみ適用します**。
>UserSigを正しく発行するには、UserSig計算コードをサーバー側に渡し、App指向のインターフェースを提供してもらいます。Appは、UserSigが必要なときに、サービスサーバーに対して動的なUserSigを取得するためのリクエストを開始します。詳細については、[サーバー側でのUserSig生成](https://intl.cloud.tencent.com/document/product/1047/34385)をご覧ください。

## ステップ4：コンパイルと実行
ユーザーの各デバイスのIDEで直接コンパイルして実行できます。詳細については、[ステップ3](#step3)のクローンDemoプロジェクトの対応するディレクトリにある`README.md`ファイルをご覧ください。

** iOS DemoとMac Demoのコンパイルと実行にはpodの統合が必要です。詳細な手順は次のとおりです。**
1.デバイスで以下のコマンドを実行して、podのバージョンを確認します。
```
pod --version
```
podが存在しないと表示されるか、またはpodのバージョンが1.7.5以前の場合は、以下のコマンドを実行して最新のpodをインストールしてください。
```
//gemソースを置き換えます
gem sources --remove https://rubygems.org/
gem sources --add https://gems.ruby-china.com/
//podをインストールします
sudo gem install cocoapods -n /usr/local/bin
//複数のXcodeがインストールされている場合は、以下のコマンドを使用してXcodeバージョンを選択してください（通常は最新のXcodeバージョンを選択します）
sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer
//podのローカルライブラリを更新します
pod setup
```
2.デバイスで以下のコマンドを実行して、依存関係ライブラリをインストールします。
```
//iOS
cd iOS/TUIKitDemo
pod install
//Mac
cd Mac/TUIKitDemo
pod install
```
 インストールに失敗した場合は、以下のコマンドを実行して、ローカルのCocoaPodsリポジトリリストを更新します。
 ```bash
 pod repo update
 ```
3.コンパイルと実行
 - iOS：iOS/TUIKitDemoフォルダに移動し、`TUIKitDemo.xcworkspace`を開いてコンパイルして実行します。
 - Mac：Mac/TUIKitDemoフォルダに移動し、`TUIKitDemo.xcworkspace`を開いてコンパイルして実行します。



