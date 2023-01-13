

## 概要


Cloud Object Storage（COS）コンソールは、COSユーザーのための、最も簡単でスタートしやすい操作方法です。ユーザーはコードを記述したりプログラムを実行したりする必要はなく、COSコンソールから直接COSサービスを利用できます。

## 準備作業

COSを初めて使用する場合、まず以下の基本概念を理解することをお勧めします。

- [バケット（Bucket）](https://intl.cloud.tencent.com/document/product/436/13312) ：オブジェクトのキャリアであり、オブジェクトを入れておくための「容器」と理解することができます。1つのバケットには無数のオブジェクトを格納できます。
- [オブジェクト（Object）](https://intl.cloud.tencent.com/document/product/436/13324)：COSの基本ユニットであり、画像、ドキュメント、オーディオビデオファイルなどのあらゆるフォーマットタイプのデータを理解することができます。
- [リージョン（Region）](https://intl.cloud.tencent.com/document/product/436/6224)：Tencent Cloudのホスティングデータセンターが分布する地域です。COSのデータはこれらのリージョンのバケット内に保存されます。

次に、COSコンソールでCOSサービスをすばやく利用し、クラウドにデータを保存する方法についてご説明します。

## 手順1：Tencent Cloudアカウントの登録
Tencent CloudのCOSサービスを利用する前に、Tencent Cloudアカウントの登録が必要です。下のボタンをクリックして登録を開始してください（すでに登録している場合は、この手順をスキップしてください）。

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://www.tencentcloud.com/en/account/register" target="_blank"  style="color: white; font-size:13px;">登録開始</a></div>

## 手順2. 実名認証の完了
アカウントの登録が完了したら、このアカウントを使用して[Tencent Cloudコンソール](https://console.cloud.tencent.com/)にログインし、実名認証を開始します。詳細な操作ガイドについては、[実名認証の説明](https://intl.cloud.tencent.com/document/product/378/3629)をご参照ください。（完了済みの場合は、この手順をスキップしてください）

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:13px;"  hotrep="document.guide.3128.btn2">実名認証の開始</a></div>


## 手順3：COSサービスのアクティブ化
[Tencent Cloudコンソール](https://console.cloud.tencent.com/)で、**クラウド製品>COS**を選択し、COSコンソールに進み、インターフェースプロンプトに従ってCOSサービスをアクティブ化します（すでにアクティブ化している場合は、この手順をスキップしてください）。

<div style="background-color:#00A4FF; width: 225px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:13px;">COSサービスのアクティブ化</a></div>


## 手順4：バケットの作成
オブジェクトを格納するためのバケットを作成する必要があります。

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、左側ナビゲーションバーの**バケットリスト**をクリックし、バケット管理ページに進みます。
2. **バケットの作成**をクリックし、以下の設定情報を入力します。その他の設定はデフォルトのままでかまいません。
 - 名称：バケットの名前を入力します。名称は設定すると変更できません。ここでは例として、「examplebucket」と入力します。
 - 所属リージョン：バケットが属するリージョンです。広州リージョンなど、お客様のビジネスに最も近いリージョンを選択します。
 - アクセス権限：バケットのアクセス権限です。ここでは、デフォルトの「プライベート読み取り/書き込み」のままにします。
3. **OK**をクリックすると、作成が完了します。


## 手順5：オブジェクトのアップロード
ローカルからファイルを選択してバケットにアップロードします。

1. バケット名をクリックして、バケットリストページに進みます。
2. **ファイルのアップロード>ファイルの選択**を選択し、バケットにアップロードしたいファイルを選択します。例えば、exampleobjext.zipというファイル名のファイルとします。
3. **アップロード**をクリックすると、exampleobjext.zipファイルをバケットにアップロードできます。


## 手順6：オブジェクトのダウンロード
クラウドからローカルにデータをダウンロードします。
1. exampleobjext.zipファイルの右側にある**詳細**をクリックし、オブジェクトのプロパティページに進みます。
2. 基本情報設定項目で、**オブジェクトのダウンロード**をクリックしてダウンロードするか、**一時リンクのコピー**をクリックし、ブラウザのアドレスバーにリンクを貼り付けてエンターキーを押せば、オブジェクトをダウンロードすることができます。
>?デフォルトで、ダウンロードしたオブジェクトをブラウザで直接開くことがサポートされている場合、ダウンロードではなく、一時リンクにアクセスする方法でオブジェクトを直接プレビューできます。

## その他の機能
オブジェクトのアクセス権限の設定、リンク不正アクセス防止の設定、静的ウェブサイトの設定など、コンソールの詳しい機能については、[コンソールの概要](https://intl.cloud.tencent.com/document/product/436/11365)をご参照ください。


## その他のクイックスタート方式
COSは、COSサービスを管理・使用するためのコンソールをユーザーに提供するだけでなく、ユーザーの選択肢として、以下のようなクイックスタート方式を提供しています。

<table>
<thead>
<tr>
<th align="left" width="30%">その他のクイックスタート方式</th>
<th align="left" width="70%">機能説明</th>
</tr>
</thead>
<tbody><tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowserツール</a></td>
<td align="left" width="70%">このツールは、ユーザーが視覚化インターフェースを通じて、データのアップロード、ダウンロード、アクセスリンク生成などの操作を便利に行えるようサポートするものです。</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://cloud.tencent.com/doc/product/436/10976">COSCMDツール</a></td>
<td align="left" width="70%">このツールは、ユーザーが簡単なコマンド行を使用して、オブジェクトの一括アップロード、ダウンロード、削除などの操作を実現できるようサポートするものです。</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">API方式</a></td>
<td align="left" width="70%">COSはXML APIという、軽量でコネクションレスなインターフェースを使用しています。このインターフェースを呼び出すことで、HTTP/HTTPSにより直接のリクエスト送信およびレスポンス受信を行うことができ、Tencent Cloud COSバックエンドとのインタラクション操作を実現することができます。</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK方式</a></td>
<td align="left" width="70%">Android、C、C++、.NET、Go、iOS、Java、JavaScript、Node.js、PHP、Python、ミニプログラムSDKなど、様々なメインストリーム開発言語をサポートしています。</td>
</tr>
</tbody></table>



## 問題が発生した場合

ご不便をおかけして申し訳ございません。[お問い合わせ](https://intl.cloud.tencent.com/contact-sales)までご連絡ください。



