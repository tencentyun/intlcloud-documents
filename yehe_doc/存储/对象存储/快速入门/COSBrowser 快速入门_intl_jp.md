Tencent CloudのCloud Object Storage(COS)を初めて使用する場合、まずCOS[バケット](https://intl.cloud.tencent.com/document/product/436/13312)、[オブジェクト](https://intl.cloud.tencent.com/document/product/436/13324)、[仕様と制限](https://intl.cloud.tencent.com/document/product/436/14518)および[よくあるご質問](https://intl.cloud.tencent.com/document/product/436/6282)をご確認くださいますようお願いいたします。

COSBrowserは、COSがリリースした視覚化インターフェースツールで、Windows、macOS、Linux、Android、iOSバージョンを提供しています。より簡単なインタラクションの使用を可能にし、COSリソースの確認、転送および管理を手軽に実現できます。
ここでは、WindowsプラットフォームのCOSBrowserを例として、バケットの作成、オブジェクトのアップロードとダウンロード、オブジェクトの共有の方法についてご説明します。


##  前提条件

1. Tencent CloudのアカウントでCOSサービスをアクティブ化する必要があります。COSサービスをアクティブ化していない場合は、[COSコンソール](https://console.cloud.tencent.com/cos5)に移動し、プロンプトに従ってアクティブ化してください。
2. COSBrowserツールはAPIキーを使用してログインしますので、まず[APIキー](https://console.cloud.tencent.com/cam/capi)の管理ページに移動し、APIキーを作成する必要があります。


## 手順1：COSBrowserのダウンロードとインストール

<div style="background-color:#00A4FF; width: 190px; height: 35px; line-height:35px; text-align:center;"><a href="https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe" target="_blank"  style="color: white; font-size:16px;">ここをクリックして COSBrowserをダウンロード</a></div><br>


Windows版COSBrowserのシステム要件：Windows 7 32/64ビット以上、Windows Server 2008 R2 64ビット以上。
他のシステムバージョンのCOSBrowserについては、[COSBrowserの概要](https://intl.cloud.tencent.com/document/product/436/11366)でダウンロードしてください。



## 手順2：COSBrowserへのログイン

[APIキー](https://console.cloud.tencent.com/cam/capi)を使用 して、COSBrowserにログインします。


## 手順3：バケットの作成

1. ログインに成功したら、ツール画面左上の**バケットの作成**をクリックします。
2. ポップアップウィンドウで、バケットの情報を入力します。
![](https://main.qcloudimg.com/raw/d5c11a8be17d9a3462c0ca73ee189c73.png)
 - バケット名：バケット名をカスタマイズする場合、ここでは「examplebucket」と入力します。
 - リージョン：バケットの所属リージョンです。お客様に最も近いリージョンを選択します。例えば深圳にいる場合、リージョンは広州（ap-guangzhou）を選択できます。
 - アクセス権限：バケットのアクセス権限です。ここでは、「プライベート読み取り/書き込み」を選択します。
 - バケットタグ/マルチAZ特性はオプション項目で、ここでは無視します。
3. **OK**をクリックすると、バケットの作成が完了します。


## 手順4：オブジェクトのアップロード

1. 手順3で作成したバケットをクリックして、バケット管理ページに進みます。
2. **アップロード>ファイルの選択**を選択し、バケットにアップロードするローカルファイルを選択します。例えば、exampleobjext.txtとします。
3. **アップロード**をクリックすると、exampleobjext.txtをバケットにアップロードできます。


## 手順5：オブジェクトのダウンロード

#### 方法1


1. COSBrowserツール右上隅の<img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;">をクリックし、リストビューに切り替えます（すでにリストビューになっている場合は、この手順を行う必要はありません）。
2. ファイル右側のアクションバーの下にある<img src="https://main.qcloudimg.com/raw/0631f784902fb5e146ac0d0f6befe346.jpg"  style="margin:0;">をクリックすると、ファイルをダウンロードすることができます。


#### 方法2

1. ファイル上でマウスを右クリックし、ドロップダウンメニューから**高度なダウンロード**をクリックします。
2. COSBrowserツールが高度なダウンロードウィンドウをポップアップするので、実際の必要性に応じて「リネーム」、「上書き」、「スキップ」を選択してください。
![](https://main.qcloudimg.com/raw/6e533ea1b75df3de7dba029a6976f844.png)
3. **今すぐダウンロード**をクリックすると、COSBrowserツールは選択したファイルをダウンロードします。


## 手順6：オブジェクトの共有

COS内の各ファイルは、すべて特定のリンクを介してアクセスすることができます。ファイルにプライベート読み取り権限がある場合は、一時的な署名をリクエストすることで、時間制限付きの一時的なアクセスリンクを発行することができます。オブジェクトリンクの発行方法には、次の2つがあります。

#### 方法1

1. COSBrowserツール右上隅の<img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;">をクリックし、リストビューに切り替えます（すでにリストビューになっている場合は、この手順を行う必要はありません）。
2. ファイル右側のアクションバーの下にある<img src="https://main.qcloudimg.com/raw/37acaeb370eb77e1bb0c792d542792e2.jpg"  style="margin:0;">をクリックします。
3. COSBrowserツールの上部に**一時リンクのコピーに成功しました。リンクは2時間有効です**と表示されれば、リンクの発行とコピーに成功したことになります。
4. このリンクからファイルにアクセスすることができます。この方法で発行されたファイルリンクの有効期限は2時間です。有効期限をカスタマイズする必要がある場合は、方法2で行うことができます。


#### 方法2

1. COSBrowserツール右上隅の<img src="https://main.qcloudimg.com/raw/b3de2bc7284b5aaba9b4f9af6c408205.jpg" style="margin:0;">をクリックし、リストビューに切り替えます（すでにリストビューになっている場合は、この手順を行う必要はありません）。
2. ファイル右側の操作バーの下にある**...**をクリックし、ドロップダウンメニューから**共有**をクリックします。
![](https://main.qcloudimg.com/raw/1ab8d2c4a61ae3e0b94c06c9d65ce3f7.png)
3. ポップアップしたカスタムコピーリンクウィンドウで、ファイルリンクを設定します。ここのファイルがプライベート読み取り/書き込み権限になっている場合、**署名付き一時リンクをコピー....**を選択する必要があります。選択した場合、リンクは指定された期間中だけ有効になります。
![](https://qcloudimg.tencent-cloud.cn/raw/be35af7fe2e1a4138ec75e2fa90e5343.png)
4. **コピー**をクリックし、一時ファイルにリンクをコピーします。このリンクからファイルにアクセスすることができます。

## その他の機能

COSBrowserは上記の機能以外にも、バケットのアクセス権限の変更、ファイルのプレビューなど、多彩な機能を持っています。詳細については、[デスクトップ機能リスト](https://intl.cloud.tencent.com/document/product/436/11366#.E6.A1.8C.E9.9D.A2.E7.AB.AF.E5.8A.9F.E8.83.BD.E5.88.97.E8.A1.A8)ドキュメントをご参照ください。

## 問題が発生した場合

ご不便をおかけして申し訳ございません。[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)までご連絡ください。

##  関連ドキュメント

モバイル端末(iOS、Android)のCOSBrowserについては、以下のドキュメントをご参照ください。

- [COSBrowserの概要](https://intl.cloud.tencent.com/document/product/436/11366)
- [モバイル端末の使用説明](https://intl.cloud.tencent.com/document/product/436/41616)

