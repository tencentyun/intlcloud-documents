このドキュメントでは、主にTencent Cloud TRTC Demo (Windows C++）を素早く実行する方法を紹介します。

## 環境要件
- Microsoft Visual Studio 2017バージョン以上、Microsoft Visual Studio 2019の使用を推奨します。
- [QT](https://download.qt.io/archive/qt/5.14/5.14.2/)（QT 5.14.xバージョン）開発環境をダウンロードしてインストールします。
- [.vsix](https://download.qt.io/official_releases/vsaddin/2.7.2/)プラグインファイルをダウンロードしてインストールします。公式サイトで対応するプラグインのバージョンを探してインストールすると完了できます。
- VSを開いてツールバーから`QT VS Tools -> Qt Options -> Qt Versions`をさがし、自分のQtコンパイラ msvcをadd（追加）します。
- `SDK/CPlusPlus/Win64/lib` 下のすべての `.dll` ファイルをプロジェクトディレクトリ下の `debug` / `release` フォルダ下にコピーしてください。
>! `Debug/release`フォルダはいずれもVSの環境構成後に自動的に生成されます。32bitプログラムならば、`SDK/CPlusPlus/Win64/lib`下のすべての`.dll`を`debug` / `release` フォルダ下にコピーしてください。


##  前提条件
[Tencent Cloudの登録](https://intl.cloud.tencent.com/document/product/378/17985)によりアカウントを登録している。

## 操作手順
[](id:step1)
### 手順1：新規アプリケーションの作成
1. TRTCコンソールにログインし、**開発支援** > [**Demoクイックスタート**](https://console.cloud.tencent.com/trtc/quickstart)を選択します。
2. **アプリケーションの作成**をクリックし、`TestTRTC`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合、**既存のアプリケーションを選択**をクリックします。
3. 実際の業務ニーズに応じてタグを追加または編集し、**作成**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)
>?
>-アプリケーション名には、数字、中国語と英語の文字、アンダーラインのみを含めることができ、15文字以内とします。
タグはTencent Cloudのさまざまなリソースを識別して管理するために使用されます。たとえば、企業に複数の事業部門があり、各部門に1つ以上のTRTCアプリケーションがある場合、企業はTRTCアプリケーションにタグを追加することで部門情報にマークを付けることができます。タグは入力必須ではありません。実際のビジネスニーズに応じてタグを追加または編集できます。

[](id:step2)
### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際のビジネスニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、**ダウンロードしました。次のステップ**をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### 手順3：Demo プログラムファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. SDKAppIDとキー情報の設定ファイルを検索して開きます。以下の通りです：
 <table>
     <tr>
         <th nowrap="nowrap">適用可能なプラットフォーム</th>  
         <th nowrap="nowrap">ファイル相対パス</th>  
     </tr>
     <tr>      
         <td>Windows(C++/QT)</td>   
         <td>Windows/QTDemo/src/Util/defs.h</td>   
     </tr>
     <tr>      
         <td>Windows(C++/Duilib)</td>   
         <td>Windows/DuilibDemo/GenerateTestUserSig.h</td>   
     </tr>
 </table>
3. `defs.h`または`GenerateTestUserSig.h`ファイルの関連するパラメータを設定します：
  <ul><li>SDKAppID：デフォルトでは0です。実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul>
  <img src="https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png">
4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要である場合には、Appから業務サーバーにリクエストを送信し、動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166#Server)をご参照ください。

[](id:step4)
### 手順4：コンパイルと実行
#### QtDemo
- **方法1：**QtCreatorを使用してソースコードディレクトリ下の`QTDemo\QTDemo.pro`プロジェクトファイルを開き、QTDemoプロジェクトをコンパイルして実行します。
- **方法2：**QT開発プラグインをインストールしたVisual Studio（VS2015以降を推奨）を起動し，メニューから`Qt VS Tools > Open Qt Project File(.pro)...`を選択します。ソースコードディレクトリ下の`QTDemo\QTDemo.pro`プロジェクトファイルを開き、QTDemoプロジェクトをコンパイルして実行します。

#### DuilibDemo
- Visual Studio（VS2015を推奨）を使用してソースコードディレクトリの`DuilibDemo\TRTCDuilibDemo.sln`プロジェクトファイルを開きます。Release/X86を選択してプラットフォームを構築することをお勧めします。Demoプロジェクトをコンパイルし実行させればOKです。

## よくあるご質問

### 1. キーをクエリーするとき、パブリックキーとプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか？
TRTC SDK 6.6バージョン（2019年08月）では、新しい署名アルゴリズムのHMAC-SHA256の使用を開始しました。それ以前に作成されたアプリケーションの場合、新しい暗号化キーを取得するために、署名アルゴリズムをアップグレードしてください。アップグレードしない場合でも、[旧バージョンアルゴリズムECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166#Old)は引き続き使用できます。アップグレード済みであれば、必要に応じて新旧アルゴリズムを切り替えます。

アップグレード/切替の操作：
 1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで**アプリケーション管理**を選択し、ターゲットアプリケーションのある行の**アプリケーション情報**をクリックします。
 3. **クイックマスター**タブを選択して**手順2 UserSigを発行するためのキーを取得**エリアの**ここをクリックしてアップグレード**、**非対称暗号化**または**HMAC-SHA256**をクリックします。
  - アップグレード
  - 旧バージョンアルゴリズムの ECDSA-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. 2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか。
2台のデバイスでDemoを実行するときは、異なるUserIDを使用していることを確認してください。TRTCでは、2台のデバイスでの同一UserID（SDKAppIDが異なる場合を除く）の同時使用をサポートしていません。


### 3. ファイアウォールにはどのような制限がありますか？
SDKがUDPプロトコルを使用してオーディオ・ビデオ伝送を行っているため、UDPをブロックするオフィスネットワークでは使用できません。類似した問題がある場合には、[企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照の上、問題及び原因解決にお役立てください。
