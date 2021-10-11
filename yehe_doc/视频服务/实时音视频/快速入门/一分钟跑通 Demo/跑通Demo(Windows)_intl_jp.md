ここでは、主にTRTC Demo（Windows）を素早く実行する方法をご紹介します。

## 環境要件
### Windows（C++）開発環境
- Microsoft Visual Studio 2015バージョン以上、Microsoft Visual Studio 2015のご使用を推奨します。 
- Windows SDK バージョン8.0以上、Windows SDK 8.1の使用を推奨します。

### Windows（C#）開発環境
- Microsoft Visual Studio 2015バージョン以上、Microsoft Visual Studio 2017の使用を推奨します。
- .Net Framework バージョン4.0以上、.Net Framework 4.0の使用を推奨します。

### Windows（QT）開発環境
- Microsoft Visual Studio 2015およびそれ以降のバージョン。Microsoft Visual Studio 2015の使用を推奨します。
- [.vsix](https://download.qt.io/official_releases/vsaddin/) プラグインファイルをダウンロードしてインストールします。公式サイトで対応するプラグインのバージョンをさがしインストールすればOKです。
- VSを開いてツールバーから`QT VS Tools -> Qt Options -> Qt Versions`をさがし、自分のQtコンパイラ msvcをadd（追加）します。
- `SDK/CPlusPlus/Win32/lib` 下のすべての `.dll` ファイルをプロジェクトディレクトリ下の `debug` / `release` フォルダ下にコピーする必要があります。
>! `debug/release` フォルダは、すべて VS 上の環境設定が完了後に自動的に生成されます。

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)を行い、[実名認証](https://intl.cloud.tencent.com/document/product/378/3629)が完了済みであること。

## 操作手順
[](id:step1)
### ステップ1：新規アプリケーションの作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2.【アプリケーションの作成】をクリックして、 `TestTRTC`などのアプリケーション名を入力します。すでにアプリケーションがある場合は、【既存のアプリケーションを選択】をクリックします。
3. ビジネスのニーズに合わせてタグを追加または編集し、【作成する】をクリックします。
![](https://main.qcloudimg.com/raw/8dc52b5fa66ec4a5a4317719f9d442b9.png)
>?
>- アプリケーション名には、数字、中国語と英語の文字、アンダーラインのみを含めることができ、15文字以内とします。
>- タグは、Tencent Cloudのさまざまなリソースを識別および整理するのに役立ちます。例えば：企業に複数の事業部門があり、各部門に1つ以上のTRTCアプリケーションがある場合、TRTCアプリケーションにタグを追加することで部門情報にマークを付けることができます。タグは必須ではありません。実際のビジネスニーズに合わせてタグを追加または編集できます。

[](id:step2)
### ステップ2：SDKおよびDemoソースコードをダウンロード
1. 実際のビジネスニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロード済み。次へ】をクリックします。

[](id:step3)
### ステップ3： Demo プログラムファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2.  `GenerateTestUserSig` ファイルを見つけて開きます。：
 <table>
     <tr>
         <th nowrap="nowrap">適用可能なプラットフォーム</th>  
         <th nowrap="nowrap">ファイル相対パス</th>  
     </tr>
   <tr>      
         <td>Windows(C++)</td>   
       <td>Windows/DuilibDemo/GenerateTestUserSig.h</td>   
     </tr> 
   <tr>
       <td>Windows(C#)</td>   
       <td>Windows/CSharpDemo/GenerateTestUserSig.cs</td>
     </tr> 
 </table>
3. `GenerateTestUserSig.js`のファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
  
4. 貼り付け完了後、【貼り付けました。次へ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソールの概要ページに戻る】をクリックすればOKです。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:step4)
### ステップ4：コンパイル実行
- **Windows(C++):**
Visual Studio（VS2015をお勧めします）を使用してソースコードディレクトリの`DuilibDemo\TRTCDuilibDemo.sln`プロジェクトファイルを開きます。Release/X86 を選択してプラットフォームを構築することをお勧めします。Demoプロジェクトをコンパイルし動作させればOKです。
- **Windows(C#):**
Visual Studio（VS2017をお勧めします）を使用してソースコードディレクトリの`CSharpDemo\TRTCCSharpDemo.sln`プロジェクトファイルを開きます。Release/X86を選択してプラットフォームを構築することをお勧めします。Demoプロジェクトをコンパイルし動作させればOKです。
- **Windows(QT):** 
Visual Studio（ VS2015 以上を推奨）を使用してソースコードディレクトリの
QTDemo\QTDemo.proプロジェクトファイルを開きます。QTDemo プロジェクトをコンパイルし動作させればOKです。

## よくあるご質問

### 1. キーをクエリーするとき、公開鍵および秘密鍵の情報しか取得できませんが、キーはどうしたら取得できますか。
TRTC SDK 6.6バージョン（2019年08月）では、新しい署名アルゴリズムのHMAC-SHA256の使用を開始しました。それ以前に作成されたアプリケーションの場合、新しい暗号化鍵を取得するために、署名アルゴリズムをアップグレードする必要があります。アップグレードしない場合でも、[旧バージョンアルゴリズム ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムを切り替えます。

アップグレード/切替の操作：
 1. [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、ターゲットアプリケーションのある行の【アプリケーション情報】をクリックします。
 3．【クイックスタート】タブを選択して【ステップ2 UserSigを発行するためのキーを取得】エリアの【ここをクリックしてアップグレード】、【非対称暗号化】または【HMAC-SHA256】をクリックします。
  - アップグレード：
  - 旧バージョンアルゴリズムのECDSA-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/96a974bcc25d0fab17db839be12fdb5e/%E8%B7%91%E9%80%9ADemo(Windows)2-%E8%BF%94%E8%BF%98.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/c3d53c405bb074ef4758cb12aa01e024/%E8%B7%91%E9%80%9ADemo(Windows)3-%E8%BF%94%E8%BF%98.png)

### 2. 2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか？
2台のデバイスでDemoを実行するときは、異なるUserIDを使用していることを確認してください。TRTCでは、2台のデバイスでの同一UserID（SDKAppIDが異なる場合を除く）の同時使用をサポートしていません。

### 3. ファイアウォールにはどのような制限がありますか。
SDKがUDPプロトコルを使用してオーディオ・ビデオ伝送を行っているため、UDPをブロックするオフィスネットワークでは使用できません。同様の問題が発生した場合は、[企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。
