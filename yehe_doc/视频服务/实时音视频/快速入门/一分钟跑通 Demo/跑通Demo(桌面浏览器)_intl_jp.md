このドキュメントでは、主にTencent Cloud TRTC デスクトップブラウザ SDKのDemoのクイック実行の方法を紹介します。

## サポートするプラットフォーム

WebRTC の技術は Googleが一番早く提案し、現在は主に、デスクトップ版Chromeブラウザ、デスクトップ版Safariブラウザおよびモバイル版Safariブラウザでかなり完全にサポートされています。その他のプラットフォーム（例：Androidプラットフォームブラウザ）のサポート状況はこれに比べると劣ります。

- ユースケースが主に教育系シナリオである場合は、教師側にはより安定性の高い [Electron](https://intl.cloud.tencent.com/document/product/647/35097) のソリューションを使用することをお勧めします。大小2系統の画面、よりフレキシブルな画面共有プラン、脆弱なネットワークからのより強力なリカバー能力をサポートしています。



<table>
<thead>
<tr>
<th width="15%">OS</th>
<th width="24%">ブラウザタイプ</th>
<th>ブラウザの最低<br>バージョン要件</th>
<th>受信（再生）</th>
<th>送信（マイク・オン）</th>
<th>画面共有</th>
</tr>
</thead>
<tbody><tr>
<td>Mac OS</td>
<td>デスクトップ版 Safari ブラウザ</td>
<td>11+</td>
<td>サポート</td>
<td>サポート</td>
<td>サポート（Safari 13+のバージョンが必要）</td>
</tr><tr>
<td>Mac OS</td>
<td>デスクトップ版 Chrome ブラウザ</td>
<td>56+</td>
<td>サポート</td>
<td>サポート</td>
<td>サポート（Chrome 72+のバージョンが必要）</td>
</tr><tr>
<td>Mac OS</td>
<td>デスクトップ版 Firefox ブラウザ</td>
<td>56+</td>
<td>サポート</td>
<td>サポート</td>
<td>サポート（Firefox 66+のバージョンが必要）</td>
</tr><tr>
<td>Mac OS</td>
<td>デスクトップ版 Edge ブラウザ</td>
<td>80+</td>
<td>サポート</td>
<td>サポート</td>
<td>サポート</td>
</tr><tr>
<td>Windows</td>
<td>デスクトップ版 Chrome ブラウザ</td>
<td>56+</td>
<td>サポート</td>
<td>サポート</td>
<td>サポート（Chrome 72+のバージョンが必要）</td>
</tr><tr>
<td>Windows</td>
<td>デスクトップ版 QQ ブラウザ（超高速カーネル）</td>
<td>10.4+</td>
<td>サポート</td>
<td>サポート</td>
<td>未サポート</td>
</tr><tr>
<td>Windows</td>
<td>デスクトップ版 Firefox ブラウザ</td>
<td>56+</td>
<td>サポート</td>
<td>サポート</td>
<td>サポート（Firefox 66+のバージョンが必要）</td>
</tr><tr>
<td>Windows</td>
<td>デスクトップ版 Edge ブラウザ</td>
<td>80+</td>
<td>サポート</td>
<td>サポート</td>
<td>サポート</td>
</tr><tr>
<td>iOS 11.1.2+</td>
<td>モバイル版 Safari ブラウザ</td>
<td>11+</td>
<td>サポート</td>
<td>サポート</td>
<td>未サポート</td>
</tr><tr>
<td>iOS 12.1.4+</td>
<td>WeChat埋込ウェブページ</td>
<td>-</td>
<td>サポート</td>
<td>未サポート</td>
<td>未サポート</td>
</tr><tr>
<td>Android</td>
<td>モバイル版 QQ ブラウザ</td>
<td>-</td>
<td>未サポート</td>
<td>未サポート</td>
<td>未サポート</td>
</tr><tr>
<td>Android</td>
<td>モバイル版 UC ブラウザ</td>
<td>-</td>
<td>未サポート</td>
<td>未サポート</td>
<td>未サポート</td>
</tr><tr>
<td>Android</td>
<td>WeChat埋込ウェブページ（TBS カーネル）</td>
<td>-</td>
<td>サポート</td>
<td>サポート</td>
<td>未サポート</td>
</tr><tr>
<td>Android</td>
<td>WeChat埋込ウェブページ（XWEB カーネル）</td>
<td>-</td>
<td>サポート</td>
<td>未サポート</td>
<td>未サポート</td>
</tr>
</tbody></table>

>! 
>- ブラウザで、[WebRTC 能力テスト](https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/web/demo/env-detect/index.html) の画面を開き、WebRTCが完全にサポートされているかチェックすることができます（例：公式アカウント等のブラウザ環境）。
>- H.264の版権の制限により、ファーウェイのシステムの Chrome ブラウザおよび Chrome WebViewをカーネルとするブラウザでは、TRTC デスクトップブラウザ版SDKの正常な動作をサポートしていません。

[](id:requirements)
## 環境要件
- 最新バージョンの Chrome ブラウザを使用してください。
- TRTC デスクトップブラウザ SDKは、以下のポートに依存してデータ転送を行いますので、これらをファイアウォールのホワイトリストに追加してください。設定完了後、[公式ウェブサイトのDemo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html)にアクセスして体験し、設定が有効かどうかをチェックすることができます 。
 - TCP ポート：8687
 - UDP ポート：8000、8080、8800、843、443、16285
 - ドメイン名：qcloud.rtc.qq.com
 
## 前提条件
[Tencent Cloudの登録](https://intl.cloud.tencent.com/document/product/378/17985) アカウントがあり、 [実名認証(https://intl.cloud.tencent.com/document/product/378/3629)が完了している必要があります。実名認証を行っていない場合、中国国内のリソースを購入することができません。

##　操作手順

[](id:step1)

### ステップ1：新規アプリケーションの作成
1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 【今すぐスタート】をクリックし、アプリケーション名（例：`TestTRTC`）を入力して、【アプリケーションの作成】をクリックします。

[](id:step2)
### ステップ2： SDKとDemoソースコードのダウンロード
1. マウスを対応するカードのところに移動させ、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Web/TRTCSimpleDemo)】をクリックして Githubに移動（または【[ZIP](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/H5_latest.zip?_ga=1.195966252.185644906.1567570704)】をクリック）し、関連する SDKおよび付属のDemo ソースコードをダウンロードします。
 ![](https://main.qcloudimg.com/raw/70f4f26e438e63b62b1dd55306d1c296.png)
2. ダウンロードが完了したら、TRTCコンソールに戻り、【ダウンロード済み、次へ】をクリックすれば、 SDKAppIDとキー情報を確認できます。

[](id:step3)
### ステップ3： Demo プログラムファイルの設定
1. [ステップ2](#step2)でダウンロードしたソースコードパッケージを解凍します。
2. `Web/TRTCSimpleDemo/js/debug/GenerateTestUserSig.js`のファイルを見つけて開きます。
3. `GenerateTestUserSig.js`ファイルの中の関連パラメータを設定します。
  <ul><li>SDKAPPID：デフォルトの状態は0です。実際の SDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトの状態は空文字列です。実際のキー情報を設定してください。</li></ul> 
4. TRTCコンソールに戻り、【ペースト完了、次へ】をクリックします。
5. 【ガイドを閉じ、コンソールに入ってアプリケーション管理】をクリックします。

>!ここで言及する UserSigの生成方式は、クライアントコードの中でのSECRETKEYの設定となります。この方法でのSECRETKEYは非常に簡単に逆コンパイルされ、逆方向にクラッキングされやすくなり、一度キーが漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。このため、**この方法はローカルでのDemoのクイック実行と機能のデバッグにのみ適しています**。
>正しい UserSigの発行方法は、UserSig の計算コードをお客様のサーバーに統合して、App向けのポートを用意し、UserSig を必要とするときは、App から業務サーバーにリクエストを出して、ダイナミック UserSigを取得することです。より詳細な内容については、 [サーバーでのUserSig生成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### ステップ4： Demoの動作
Chrome ブラウザを使用してDemoのルートディレクトリの下の`index.html`ファイルを開くと Demoが動作します。

>!
> -  通常の場合、体験 Demo はサーバーにデプロイする必要があり、`https://ドメイン名/xxx`経由でアクセスするか、または直接ローカルにサーバーを構築して、 `localhost:ポート`経由でアクセスします。
> - 現在デスクトップ版Chromeブラウザは、TRTC デスクトップブラウザ SDKの関連機能がかなり完全にサポートされています。よってChrome ブラウザを使用して体験することをお勧めします。

Demoの動作画面は図のとおりです。

- 【ルーム参加】をクリックして音声ビデオ通話ルームに入り、ローカルの音声ビデオストリームをリリースします。
 複数の画面を開き、それぞれの画面で 【ルームに参加】をクリックすることが可能です。正常な場合は、複数の画面を視聴しながらTRTCの通話をシミュレーションすることができます。
- カメラのアイコンをクリックしてカメラデバイスを選択できます。
- マイクのアイコンをクリックしてマイクデバイスを選択できます。

>?WebRTCではカメラとマイクを使用してビデオキャプチャと集音を行います。体験のプロセスで Chrome ブラウザから関連する通知を受け取った場合は、【許可する】をクリックしてください。


## よくあるご質問

### 1. キーの確認時にパブリックキーとプライベートキーの情報しか取得できません。キーを取得するにはどうすればいいですか？
TRTC SDK 6.6 バージョン（2019年8月）以降、新しい署名アルゴリズム HMAC-SHA256を採用しています。これ以前に作成したアプリケーションで、新しい暗号化キーを取得するには、先に署名アルゴリズムをアップグレードする必要があります。アップグレードしない場合も、 [旧バージョンアルゴリズム ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)引き続き使用でき、またアップグレード済みの場合は、必要に応じて新旧アルゴリズムを切り替えることができます。

アップグレード/切り替え操作：
 1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側のナビゲーションバーから【アプリケーション管理】を選択し、ターゲットアプリケーションがある行の【アプリケーション情報】をクリックします。
 3. 【クイックマスター】のタブを選択し、【第2ステップ UserSig発行のキーの取得】の部分の【ここをクリックしてアップグレード】、【非対称暗号化】または【HMAC-SHA256】をクリックします。
  - アップグレード：
  - 旧バージョンのアルゴリズム ECDSA-SHA256に切り替えます。
   ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - 新バージョンのアルゴリズム HMAC-SHA256に切り替えます。
   ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. クライアントエラー：“RtcError: no valid ice candidate found”が出現したときの対処方法は？
このエラーの出現は、TRTC デスクトップブラウザ SDK が STUNでの穴あけに失敗したことを意味します。[環境要件](#requirements) にしたがってファイアウォールの設定をチェックしてください。

### 3. クライアントエラー："RtcError: ICE/DTLS Transport connection failed"または“RtcError: DTLS Transport connection timeout”が出現したときの対処方法は？
このエラーの出現は、 TRTC デスクトップブラウザ SDKがメディア転送パスの構築時に失敗したことを意味します。[環境要件](#requirements)  にしたがってファイアウォールの設定をチェックしてください。

### 4. 10006 error が出現したときの対処方法は？
"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"が出現したときは、お客様のTRTCアプリケーションのサービス状態が使用可能かどうかを確認してください。
[TRTCコンソール](https://console.cloud.tencent.com/rav)にログインして、作成したアプリケーションをクリックし、【アカウント情報】をクリックすれば、アカウント情報パネルでサービス状態を確認できます。
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)
