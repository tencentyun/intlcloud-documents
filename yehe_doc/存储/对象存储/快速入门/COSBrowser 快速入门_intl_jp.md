
COSBrowserはTencent CloudのCloud Object Storage（COS）がリリースした視覚化インターフェースツールです。インターフェースのインタラクションがより簡単に、操作がよりスピーディーになり、デスクトップとモバイル端末の両方をサポートしています。このツールによってCOSリソースの確認、転送および管理を手軽に実現できます。COSBrowserに関するその他の説明については、[COSBrowserの概要](https://intl.cloud.tencent.com/document/product/436/11366)をご参照ください。

ここでは、COSBrowserツールによるバケットのクイック作成、およびオブジェクトのアップロード、ダウンロード、共有操作の方法について簡単にご説明します。


##  前提条件

1. Tencent CloudアカウントでCOSサービスをアクティブ化していること。
>?
>- Tencent Cloudアカウントをお持ちでない場合は、[アカウント関連ドキュメント](https://www.tencentcloud.com/document/product/378)を参照して作成できます。
>- COSサービスをアクティブ化していない場合は、[COSコンソール](https://console.cloud.tencent.com/cos5)に移動し、プロンプトに従ってアクティブ化を行ってください。
2. COSを初めて使用する場合、まず以下の基本概念を理解することをお勧めします。
 - [バケット（Bucket）](https://intl.cloud.tencent.com/document/product/436/13312) ：オブジェクトのキャリアであり、オブジェクトを入れておくための「容器」と理解することができます。1つのバケットには無数のオブジェクトを格納できます。
 - [オブジェクト（Object）](https://intl.cloud.tencent.com/document/product/436/13324)：COSの基本ユニットであり、画像、ドキュメント、オーディオビデオファイルなどのあらゆるフォーマットタイプのデータを理解することができます。
 - [リージョン（Region）](https://intl.cloud.tencent.com/document/product/436/6224)：Tencent Cloudのホスティングデータセンターが分布する地域です。COSのデータはこれらのリージョンのバケット内に保存されます。


## ステップ1：COSBrowserのダウンロードとインストール


1. WindowsバージョンのCOSBrowserの場合は、[COSBrowserをクリックしてダウンロード](https://cos5.cloud.tencent.com/cosbrowser/cosbrowser-setup-latest.exe)します。
2. ダウンロード完了後、インストールパッケージを直接ダブルクリックし、プロンプトに従ってインストールします。


>?
>- WindowsバージョンのCOSBrowserのシステム要件：Windows 7 32/64ビット以上、Windows Server 2008 R2 64ビット以上。
>- 他のシステムバージョンのCOSBrowserをダウンロードしたい場合は、[COSBrowserの概要](https://intl.cloud.tencent.com/document/product/436/11366)でダウンロードしてください。



## 手順2：COSBrowserへのログイン

WindowsバージョンのCOSBrowserはAPIキーログイン、Tencent Cloudアカウントログイン、共有リンクログインを含む、複数のログイン方法をサポートしています。 ここではTencent Cloudアカウントログインの方法を選択します。


## 手順3：バケットの作成

1. ログインに成功したら、ツール画面左上の**バケットの作成**をクリックします。
2. ポップアップウィンドウで、バケットの情報を入力します。
![](https://main.qcloudimg.com/raw/d5c11a8be17d9a3462c0ca73ee189c73.png)
 - バケット名：バケット名をカスタマイズする場合、ここでは「examplebucket」と入力します。
 - リージョン：バケットの所属リージョンです。お客様に最も近いリージョンを選択します。例えば深圳にいる場合、リージョンは広州（ap-guangzhou）を選択できます。
 - アクセス権限：バケットのアクセス権限です。ここでは、「プライベート読み取り/書き込み」を選択します。
 - バケットタグ/マルチAZ特性はオプション項目で、ここでは無視します。
3. **OK**をクリックするとバケットの作成が完了します。作成済みのバケットはバケットリストで確認できます。


## 手順4：オブジェクトのアップロード

1. 先ほど作成したバケットをクリックし、バケット管理ページに進みます。
2. **アップロード>ファイルの選択**を選択し、バケットにアップロードするローカルファイルを選択します。例えば、exampleobject.txtとします。
3. **アップロード**をクリックすると、exampleobject.txtをバケットにアップロードできます。


## 手順5：オブジェクトのダウンロード

ダウンロードしたいファイルを選択し、**ダウンロード**を右クリックします。

## 手順6：オブジェクトの共有

COSBrowserではファイルリンクまたは2次元コード方式でファイル共有を行うことができます。以下はファイルリンク共有方式の例です。

1. 共有したいファイルを選択し、右側の<img src="https://main.qcloudimg.com/raw/37acaeb370eb77e1bb0c792d542792e2.jpg"  style="margin:0;">をクリックすると、共有リンクをクイック生成できます。
>?ファイル継承バケットの権限はプライベート読み取り書き込み権限であるため、生成される共有URLは一時アクセスリンクとなり、有効期間は2時間となります。
2. 生成された共有リンクを受信者に送信すると、オンラインアクセスまたはダウンロードが行えます。
>?
>デフォルトで、共有ファイルをブラウザで直接開くことがサポートされている場合は、一時リンクにアクセスすると、ダウンロードではなく直接オンラインで表示されます。


## その他の機能

COSBrowserは上記の機能以外にも、バケットのアクセス権限の変更、ファイルのプレビューなど、多彩な機能を持っています。詳細については、[デスクトップ機能リスト](https://intl.cloud.tencent.com/document/product/436/11366#.E6.A1.8C.E9.9D.A2.E7.AB.AF.E5.8A.9F.E8.83.BD.E5.88.97.E8.A1.A8)ドキュメントをご参照ください。

## 問題が発生した場合

ご不便をおかけして申し訳ございません。[よくあるご質問](https://intl.cloud.tencent.com/document/product/436/35735)をご確認いただくか、または[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)ください。

##  関連ドキュメント

モバイル端末(iOS、Android)のCOSBrowserについては、以下のドキュメントをご参照ください。

- [COSBrowserの概要](https://intl.cloud.tencent.com/document/product/436/11366)
- [モバイル端末の使用説明](https://intl.cloud.tencent.com/document/product/436/41616)
