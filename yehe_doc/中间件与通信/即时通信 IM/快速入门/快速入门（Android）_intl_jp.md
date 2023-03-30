>## 操作手順
>[](id:step1)
>### 手順1：アプリケーションの作成
>1. [IMコンソール](https://console.cloud.tencent.com/im)にログインします。
>>?アプリケーションをすでに保有している場合は、そのSDKAppIDを記録してから[キー情報の取得](#step2)を実行してください。
>>同じTencent Cloudのアカウントで、最大300個のIMアプリケーションを作成することができます。すでにアプリケーションが300個ある場合は、使用する必要のないアプリケーションを[使用停止して削除](https://intl.cloud.tencent.com/document/product/1047/34540)すると、新しいアプリケーションを作成することができます。**アプリケーションを削除した後、そのSDKAppIDに対応するすべてのデータとサービスは失われます。慎重に操作を行ってください。**
>>
>2. **新しいアプリケーションの作成**をクリックし、**アプリケーションの作成**のダイアログボックスにアプリケーション名を入力し、**OK**をクリックします。
>![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
>3. 作成が完了すると、コンソールの概要ページで、作成したアプリケーションのステータス、サービスバージョン、SDKAppID、作成時間、タグおよび有効期限を確認できます。SDKAppID情報を記録してください。
>![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
>
>
>[](id:step2)
>### ステップ2：キー情報の取得
>1. 対象のアプリケーションカードをクリックし、アプリケーションの基本設定画面に移動します。
>![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)
>2. **基本情報**セクションで、**表示キー**をクリックし、キー情報をコピーして保存します。
>>!キー情報を適切に保管して、漏えいしないようにしてください。
>
>[](id:step3)
>### ステップ3： Demo ソースコードのダウンロードおよび設定
>
>1. IM Demoプロジェクトをダウンロードします。具体的なダウンロードアドレスについては、[SDKダウンロード](https://intl.cloud.tencent.com/document/product/1047/33996)をご参照ください。
>>?顔絵文字デザインの著作権を尊重するため、ダウンロードするDemoプロジェクトには大きな顔絵文字要素の切り取りが含まれておらず、自身のローカル顔絵文字パッケージを使用してコードを設定できます。IM Demoでの顔絵文字パッケージの不正使用は意匠権の侵害に当たる可能性があります。
>2. 端末ディレクトリのプロジェクトを開き、対応する`GenerateTestUserSig`ファイルを見付けます。パスは「Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java」です。
>3. `GenerateTestUserSig`ファイルの関連パラメータを設定します：
>
> - SDKAPPID：[手順1](#step1)で取得した実際のアプリケーションSDKAppIDを設定してください。
> - SECRETKEY： [手順2](#step2)で取得した実際のキー情報を設定してください。
> ![](https://qcloudimg.tencent-cloud.cn/raw/928dd6de772f31c5328737050baf8c5a.png)
>
>
>>!ここで言及するUserSigの取得方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適しています**。
>>正しい UserSigの発行方法は、UserSig の計算コードをお客様のサーバーに統合して、App向けのポートを用意し、UserSig を必要とするときは、App から業務サーバーにリクエストを出して、ダイナミック UserSigを取得することです。より詳細な内容については、 [サーバーでのUserSig生成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。
>
>[](id:step4)
>### 手順4：コンパイルと実行
>Android Studioを用いてプロジェクトをインポートし、直接コンパイルして実行します。
>詳細については、[ステップ3](#step3) でクローンしたDemoプロジェクトの対応ディレクトリにある`README.md`ファイルをご参照ください。
>
>**開発環境要件**
>- Android Studio-Chipmunk 
>- Gradle-6.7.1
>- Android Gradle Plugin Version-4.2.0
>- kotlin-gradle-plugin-1.5.31
>
>>!Demoデフォルトでオーディオビデオ通話機能が統合されています。この機能が依存するAVのSDKは現在、シミュレーターをサポートしていないため、実際のマシンを使用してデバッグするかまたはDemoを実行してください。
