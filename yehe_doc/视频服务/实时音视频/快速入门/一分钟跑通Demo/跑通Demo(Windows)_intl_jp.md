ここでは、主にTencent Cloudの TRTC Demo（Windows）を速く動作させる方法を紹介します。

## 環境要件
**Windows（C++）開発環境**
- Microsoft Visual Studio 2015バージョン以上，Microsoft Visual Studio 2015のご使用を推奨します。 
- Windows SDK バージョン8.0以上、Windows SDK 8.1の使用を推奨します

**Windows（C#）開発環境**
- Microsoft Visual Studio 2015バージョン以上、Microsoft Visual Studio 2017の使用を推奨します。
- .Net Framework バージョン4.0以上、.Net Framework 4.0の使用を推奨します

## 前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)、及び [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了済みです。

## 操作手順
<span id="step1"></span>
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestTRTC`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

<span id="step2"></span>
### 手順2：SDKおよびDemoのソースコードをダウンロード
1. マウスを該当するカードに移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Windows)】をクリックし、 Github（または【[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Win_latest.zip?_ga=1.195966252.185644906.1567570704)】をクリック）にジャンプし、関連するSDKおよび付属のDemoソースコードをダウンロードします。
 ![](https://main.qcloudimg.com/raw/73b9bfa89b42acbc166074a29f20be47.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

<span id="step3"></span>

### 手順3：Demoプロジェクトファイルの設定
1．[手順2]（#step2）でダウンロードしたソースコードパッケージを解凍します。
2. `GenerateTestUserSig`ファイルを探して開きます。
 <table>
     <tr>
         <th nowrap="nowrap">プラットフォームに適用</th>  
         <th nowrap="nowrap">ファイル対応パス</th>  
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
3. `GenerateTestUserSig.js`ファイルの関連パラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
	<img src="https://main.qcloudimg.com/raw/f28b968c02e8f26fe02c7ff6907239cb.png">
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

≻本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：コンパイル動作
- **Windows（C++）**
Visual Studio（VS2015をお勧めします）を使用してソースコードディレクトリの`DuilibDemo\TRTCDuilibDemo.sln`プロジェクトファイルを開きます。Release/X86 を選択してプラットフォームを構築することをお薦めします。Demoプロジェクトをコンパイルし動作させればOKです。

- **Windows（C#）**
Visual Studio（VS2017をお薦めします）を使用してソースコードディレクトリの`CSharpDemo\TRTCCSharpDemo.sln`プロジェクトファイルを開きます。Release/X86を選択してプラットフォームを構築することをお勧めします。Demoプロジェクトをコンパイルし動作させればOKです。

## よくあるご質問

### 1. キーをクエリするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか？
TRTC SDK 6.6バージョン（2019年08月）では新しい署名アルゴリズムのHMAC-SHA256の使用を始めています。その前に作成済のアプリケーションは、署名アルゴリズムをアップグレードしないと暗号化したキーを取得できません。アップグレードしなくても、[旧バージョンアルゴリズム ECDSA-SHA256]（https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じて新旧アルゴリズムに切り替えます。

アップグレード/切替の操作：
 1. [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで【アプリケーション管理】を選択し、目的とするアプリケーションのある行の【アプリケーション情報】をクリックします。
 3．【すぐに作業を開始】タブを選択して【ステップ2 UserSigを発行するためのキーを取得】エリアの【このアップグレードをクリック】、【非対称暗号化】または【HMAC-SHA256】をクリックします。
  - アップグレード
  - 旧バージョンアルゴリズムのECDSA-SHA256に戻るよう切り替えます。
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。

### 2. 2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか？
2台のデバイスがDemoを操作するとき、UserIDが異なるものを使用してください。TRTCでは、同一のUserID（SDKAppIDが異なる場合を除く）が2台のデバイスで同時に使用することをサポートしていません。


### 3. ファイアウォールにどのような制限がありますか？
SDK が UDP プロトコルを使用してオーディオビデオ伝送を行っていることから、 UDPに対してブロックがあるパブリックネットワークでは使用することができません。類似の問題があれば、 [企業ファイアウォール制限の対応](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。
