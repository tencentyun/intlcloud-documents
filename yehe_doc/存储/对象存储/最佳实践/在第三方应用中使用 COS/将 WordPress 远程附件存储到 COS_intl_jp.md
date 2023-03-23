## 概要

[WordPress](https://cn.wordpress.org/)は、PHP言語を使用して開発されたブログプラットフォームです。ユーザーは、PHPとMySQLデータベースをサポートするサーバーに、自分のウェブサイトを設置することができます。また、WordPressをコンテンツ管理システム(CMS)として使用することも可能です。

WordPressは強力な機能と拡張性を備えています。それは主にプラグインの多さによるもので、機能を拡充しやすく、ウェブサイトが備えるべき機能を基本的に完備しており、サードパーティプラグインによってすべての機能を実現することができます。

ここでは、プラグインを使用してリモート添付ファイルを実装し、WordPressのメディアライブラリ添付ファイルをTencent Cloudの[Cloud Object Storage（COS）](https://www.tencentcloud.com/products/cos)に保存する方法についてご説明します。

COSは高い拡張性、低コスト、高い信頼性と安全性などの特徴を備えています。メディアライブラリ添付ファイルをCOSに保存すると次のようなメリットがあります。

- 添付ファイルの信頼性が高まります。
- サーバーが添付ファイルのために追加のストレージスペースを用意する必要がありません。
- ユーザーが画像添付ファイルを確認する際は直接COSサーバーに接続するため、サーバーのダウンストリーム帯域幅/トラフィックを占有せず、ユーザーのアクセス速度がより速くなります。
- Tencent Cloudの[Content Delivery Network（CDN）](https://www.tencentcloud.com/products/cdn)と併用することで、ユーザーの画像添付ファイル表示速度がさらに早くなり、ウェブサイトのアクセス速度が最適化されます。



##  前提条件

1. COSバケットがすでにあること。ない場合は[バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)操作ガイドをご参照ください。
2. サーバーを作成済みであること。例えばCloud Virtual Machine（CVM）などです。関連ガイドについては[CVM製品ドキュメント](https://www.tencentcloud.com/document/product/213)をご参照ください。


## 実践手順

### Wordpressのデプロイ

Tencent CVMをベースにしてスピーディーにWordPressを構築するには、イメージによるデプロイと手動デプロイという2つの方法があります。業務ウェブサイトに比較的高い拡張性が求められる場合は、手動での構築が可能です。詳細については次のガイドをご参照ください。

- [WordPress個人サイトの手動構築（Linux）](https://intl.cloud.tencent.com/document/product/213/8044)
- [WordPress個人サイトの手動構築（Windows）](https://intl.cloud.tencent.com/document/product/213/34806)

ここではイメージによるWordPressのデプロイについてご説明します。イメージデプロイは便利かつスピーディーな方法です。操作手順は次のとおりです。

1. イメージからWordPressを起動します。
   1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、インスタンス管理ページの**新規作成**をクリックします。
   2. ページのプロンプトに従ってモデルを選択し、**インスタンス構成 > イメージ**で**イメージマーケットプレイス**をクリックし、**イメージマーケットプレイスから選択**を選択します。
   3. 「イメージマーケットプレイス」のポップアップウィンドウで、**基本ソフトウェア**を選択し、**wordpress**と入力して検索します。
   4. 必要なイメージを選択します。例として**WordPressブログプログラミング\_v5.5.3(CentOS | LAMP)**を選択し、**無料で使用**をクリックします。
   5. 購入完了後、CVMコンソールにログインし、先ほど作成したインスタンスにセキュリティグループをバインドします。ポート80を許可するインバウンドルールを追加する必要があります。
2. インスタンスの管理ページで、このCVMインスタンスの**パブリックIP**をコピーし、ローカルブラウザでアドレス`http://パブリックIP/wp-admin`にアクセスし、次のようにWordPressウェブサイトのインストールを開始します。
   1. Wordpressの言語を選択し、**Continue**をクリックします。
   2. 必要に応じてWordPressのサイトのタイトル、管理者ユーザー名、管理者パスワード、メールアドレスを入力します。
   3. **WordPressをインストールする**をクリックします。
   4. **ログイン**をクリックします。
4. WordPressを新バージョンの6.0.2にアップグレードします。
ダッシュボード左側のメニューをクリックし、「更新」メニューに進み、バージョン6.0.2に更新します。





### COSバケットの作成

1. **パブリック読み取り・プライベート書き込み**のバケットを作成します。バケットのリージョンはWordPressブログプラットフォームのCVMの実行リージョンと同一にすることをお勧めします。作成の詳細については、[バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)のドキュメントをご参照ください。
2. 作成したバケットを**バケットリスト**から見つけ、そのバケット名をクリックし、バケットのページに進みます。
3. 左側ナビゲーションバーで**概要**をクリックし、アクセスドメイン名を確認して記録します。


### プラグインのインストールと設定

プラグインのインストール方法には、プラグインライブラリからのインストールとソースコードからのインストールがあります。

#### プラグインライブラリからのインストール（推奨）

WordPressバックエンドで**プラグイン**をクリックし、**tencentcloud-cos**プラグインを直接検索し、**今すぐインストール**をクリックすればインストールできます。


#### ソースコードからのインストール

まずプラグインのソースコードをダウンロードした後、プラグインのソースコードをWordPressプラグインディレクトリ`wp-content/plugins`にアップロードし、最後にバックエンドで起動します。

以下はUbuntuでのプラグインインストールの例です。

1. wp-contentの親ディレクトリに進みます。 
```
cd /var/www/html 
```
2. 権限を追加します。 
```
chmod -R 777 wp-content 
```
3. プラグインディレクトリを作成します。
```
cd wp-content/plugins/
mkdir tencent-cloud-cos
cd tencent-cloud-cos
```
4. プラグインをプラグインディレクトリにダウンロードします。
```
wget https://cos5.cloud.tencent.com/cosbrowser/code/tencent-cloud-cos.zip
unzip tencent-cloud-cos.zip
rm tencent-cloud-cos.zip -f
```
5. 「プラグイン」の左側のメニューをクリックすると、このプラグインが見つかります。このプラグインをクリックして起動します。





#### **プラグインの設定**

プラグインtencent-cloud-cosにCOSバケットの情報を設定します。

1. 「設定」ボタンをクリックし、プラグインtencent-cloud-cosを設定します。

2. ページ内でCOSの関連情報を設定します。設定の説明については次の表をご参照ください。
<table>
<thead>
<tr>
<th align="left">設定項目</th>
<th align="left">設定値</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">SecretId、SecretKey</td>
<td align="left">アクセスキー情報。<a href="https://console.cloud.tencent.com/capi">Tencent Cloud APIキー</a>に進んで作成と取得を行うことができます</td>
</tr>
<tr>
<td align="left">所属リージョン</td>
<td align="left">バケット作成時に選択したリージョン</tdz
</tr>
<tr>
<td align="left">スペース名</td>
<td align="left">バケット作成時にカスタマイズしたバケット名。例：examplebucket-1250000000</td>
</tr>
<tr>
<td align="left">アクセスドメイン名</td>
<td align="left">COSのデフォルトのバケットドメイン名であり、ユーザーのバケット作成時に、システムがバケット名およびリージョンに基づいて自動的に生成します。<a href="https://console.cloud.tencent.com/cos5">COSコンソール</a> に進み、バケットの<strong>概要>ドメイン名情報</strong>で確認することができます</td>
</tr>
<tr>
<td align="left">自動リネーム</td>
<td align="left">ファイルをCOSにアップロードすると自動的にリネームされ、同名ファイルとの競合を防止します。リネームは指定の形式で行うことができます</td>
</tr>
<tr>
<td align="left">ローカルに保存しない</td>
<td align="left">有効にすると、ソースファイルをローカルに保存しません</td>
</tr>
<tr>
<td align="left">リモートファイルの維持</td>
<td align="left">有効にすると、ファイルを削除したときにローカルファイルのレプリカだけを削除し、リモートCOSバケット内のファイルレプリカは維持されるため、復元に便利です</td>
</tr>
<tr>
<td align="left">サムネイル禁止</td>
<td align="left">有効にすると、対応するサムネイルファイルをアップロードしません</td>
</tr>
<tr>
<td align="left">Cloud Infinite</td>
<td align="left">Cloud Infiniteサービスを有効にすると、画像の編集、圧縮、形式変換、ウォーターマーク追加などの操作を行うことができます。詳細については、<a href="https://www.tencentcloud.com/products/ci">Cloud Infinite製品の紹介</a>をご参照ください</td>
</tr>
<tr>
<td align="left">ファイル審査</td>
<td align="left">ファイル審査を有効にすると、画像、ビデオ、オーディオ、テキスト、ドキュメント、ウェブページなどのマルチメディアのコンテンツセキュリティに対してインテリジェント審査サービスを行うことができます。ユーザーが、ポルノ・低俗、違法・不正、不快感を与えるなどの禁止コンテンツを効果的に識別し、運営リスクを回避できるようにサポートします。詳細については<a href="https://www.tencentcloud.com/document/product/436/53946">コンテンツ審査の概要</a>をご参照ください</td>
</tr>
<tr>
<td align="left">ドキュメントプレビュー</td>
<td align="left">ドキュメントプレビューを有効にすると、ファイルを画像、PDFまたはHTML5ページにトランスコードすることができ、ドキュメントコンテンツのページ表示の問題を解決することができます。詳細については<a href="https://intl.cloud.tencent.com/document/product/436/49159">ドキュメントプレビューの概要</a>をご参照ください</td>
</tr>
<tr>
<td align="left">デバッグ</td>
<td align="left">エラー、異常、警告情報を記録します</td>
</tr>
</tbody></table>


2. 設定完了後に、**設定を保存**をクリックすれば完了です。



## **Wordpress添付ファイルのCOSへの保存を検証する**

Wordpressで画像付きの記事を1件作成し、画像がCOSに保存されるかどうかを確認します。

1. 画像付きの記事を1件作成します。Wordpressのダッシュボードで、「記事」の左側のメニューをクリックします。

2. WordPressでデフォルトで生成される「Hello world!」の記事を編集します。

3. 右側の「+」ボタンをクリックします。

4. 画像を1枚選択してアップロードします。

5. アップロード完了後、アップロード済みの画像のURLを表示し、画像のアドレスがCOSのアドレスになっていることを確認します。例えば`https://wd-125000000.cos.ap-nanjing.myqcloud.com/2022/10/立夏-1200x675.jpeg`などで、形式が`https://<BucketName-APPID>.cos.<Region>.myqcloud.com/<ObjectKey>`となっていれば、画像がCOSバケットにアップロードされていることを表します。

6. COSコンソールにログインすると、先ほどアップロードした画像がCOSバケット内にあることを確認できます。

>? 上記のテストに成功した後、必要があれば続いて古いリソースをCOSバケットに同期させます（[COSCMDツール](https://intl.cloud.tencent.com/document/product/436/10976)または[COS Migrationツール](https://intl.cloud.tencent.com/document/product/436/15392)を使用できます）。**これを行わなければ、古いリソースをバックエンドで正常にプレビューできなくなります**。同期が完了すると、back-to-origin設定を有効化できます。下記の[back-to-originの設定](#1)をご参照ください。


## 拡張

1. CDNアクセラレーションを使用したアクセス
バケットにCDNアクセラレーションを設定したい場合は、[CDNアクセラレーションの設定](https://intl.cloud.tencent.com/document/product/436/18670)のドキュメントをご参照ください。プラグイン設定で、URLのプレフィックスをデフォルトのCDNアクセラレーションドメイン名またはカスタムアクセラレーションドメイン名に変更するだけで設定できます。
2. データベース内のリソースアドレスの置き換え
新規作成のサイトを除き、データベースには必ず古いリソースリンクアドレスが存在するため、リソースアドレスの置き換えを行う必要があります。プラグインで置き換え機能を提供しています。最初に置き換えを行う前にはバックアップを忘れないようにしてください。
 - 古いドメイン名に元のリソースドメイン名を入力します（例：`https://example.com/`）
 - 新しいドメイン名に現在のリソースドメイン名を入力します（例：`https://img.example.com/`）
3. クロスドメインアクセスの設定
対応するリソースリンクを記事に引用する際、コンソールがクロスドメインエラー`No 'Access-Control-Allow-Origin' header is present on the requested resource`を表示することがあります。これはheaderを追加していないことが原因です。クロスドメインアクセスCORSの設定でHTTP Header追加の設定を行う必要があります。設定を行うための2つの手段を次でご説明します。
 - COSコンソールで設定

>? クロスドメイン設定の操作手順に関しては、[クロスドメインアクセスの設定](https://intl.cloud.tencent.com/document/product/436/13318)のドキュメントをご参照ください。
>
 - CDNコンソールで設定
    - 全ドメイン名を許可する場合、設定は次のようになります。
```plaintext
Access-Control-Allow-Origin: *
```
    - 個人のドメイン名のアクセスのみを許可する場合、設定は次のようになります。
```plaintext
Access-Control-Allow-Origin: https://example.com
```
<span id=1></span>
4. back-to-originの設定
WordPressバックエンドメディアライブラリにリソースをアップロードしない場合は、back-to-origin有効化の設定をお勧めします。詳細な手順については、[back-to-originの設定](https://intl.cloud.tencent.com/document/product/436/31508)のドキュメントをご参照ください。
back-to-origin設定を有効化すると、クライアントがCOSソースファイルに初めてアクセスした際、COSはオブジェクトにヒットしないことを検出し、クライアントに対しHTTPステータスコード302を返してback-to-originアドレスに対応するアドレスにリダイレクトします。このときオブジェクトはオリジンサーバーからクライアントに提供され、アクセスが保証されます。同時に、COSはオリジンサーバーからこのファイルをコピーして、バケットの対応するディレクトリに保存します。2回目のアクセスの際は、COSがオブジェクトに直接ヒットし、クライアントに返します。




