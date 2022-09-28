## 概要

[WordPress](https://cn.wordpress.org/)は、PHP言語を使用して開発されたブログプラットフォームです。ユーザーは、PHPとMySQLデータベースをサポートするサーバーに、自分のウェブサイトを設置することができます。また、WordPressをコンテンツ管理システム(CMS)として使用することも可能です。

WordPressは強力な機能と拡張性を備えています。それは主にプラグインの多さによるもので、機能を拡充しやすく、ウェブサイトが備えるべき機能を基本的に完備しており、サードパーティプラグインによってすべての機能を実現することができます。

ここでは、プラグインを使用してリモート添付ファイルを実装し、WordPressのメディアライブラリ添付ファイルをTencent Cloudの[Cloud Object Storage（COS）](https://www.tencentcloud.com/products/cos)に保存する方法についてご説明します。

COSは高い拡張性、低コスト、高い信頼性と安全性などの特徴を備えています。メディアライブラリ添付ファイルをCOSに保存すると次のようなメリットがあります。

- 添付ファイルの信頼性が高まります。
- サーバーが添付ファイルのために追加のストレージスペースを用意する必要がありません。
- ユーザーが画像添付ファイルを確認する際は直接COSサーバーに接続するため、サーバーのダウンストリーム帯域幅/トラフィックを占有せず、ユーザーのアクセス速度がより速くなります。
- Tencent Cloudの[Content Delivery Network（CDN）](https://www.tencentcloud.com/products/cdn)と併用することで、ユーザーの画像添付ファイル表示速度がさらに早くなり、ウェブサイトのアクセス速度が最適化されます。

## 準備作業

1. WordPressブログプラットフォームを構築します。
 - [WordPress公式ホームページ](https://cn.wordpress.org/download/)でWordPressの最新バージョンをダウンロードし、インストールガイドを確認することができます。

2. **パブリック読み取り・プライベート書き込み**のバケットを作成します。バケットのリージョンはWordPressブログプラットフォームのCVMの実行リージョンと同一にすることをお勧めします。作成の詳細については、[バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)のドキュメントをご参照ください。
3. 作成したバケットを**バケットリスト**から見つけ、そのバケット名をクリックし、バケットのページに進みます。

4. 左側ナビゲーションバーで**概要**をクリックし、アクセスドメイン名を確認して記録します。


## プラグインのインストールと設定

### プラグインのインストール

WordPressバックエンドで**プラグイン > プラグインのインストール**をクリックし、プラグインのインストールを開始します。プラグインは次の2種類の方法で取得し、インストールすることができます。

 - バックエンドで**tencentcloud-cos**を直接検索してインストールします（使用を推奨）。
 - [Github](https://github.com/Tencent-Cloud-Plugins/tencentcloud-wordpress-plugin-cos)から最新のreleasesソースコードをダウンロードし、WordPressバックエンドにアップロードしてインストールするか、またはソースコードをWordPressのプラグインディレクトリ`wp-content/plugins`に直接アップロードしてから、バックエンドで有効化することができます。

### プラグインの設定

1. WordPressの左側ナビゲーションバーの**Tencent Cloudの設定**をクリックし、ページ内でCOSの関連情報を設定します。設定の説明については次の表をご覧ください。
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
<td align="left">有効にすると、ソースファイルをローカルに保存しません。有効にしないことをお勧めします</td>
</tr>
<tr>
<td align="left">サムネイル禁止</td>
<td align="left">有効にすると、対応するサムネイルファイルをアップロードしません。有効にしないことをお勧めします</td>
</tr>
<tr>
<td align="left">Cloud Infinite</td>
<td align="left">Cloud Infiniteサービスを有効にすると、画像の編集、圧縮、形式変換、ウォーターマーク追加などの操作を行うことができます。詳細については、<a href="https://www.tencentcloud.com/products/ci">Cloud Infinite製品の紹介</a>をご参照ください</td>
</tr>
<tr>
<td align="left">デバッグ</td>
<td align="left">エラー、異常、警告情報を記録します。有効化を選択できます</td>
</tr>
</tbody></table>
2. 設定完了後に、**設定を保存**をクリックすれば完了です。
3. 新しいファイルをアップロードしてテストを行います。添付ファイルの詳細、添付ファイル画像のURLを確認し、添付ファイル画像のURLがTencent Cloud COSを指していることを確認します。

>? 上記のテストに成功した場合は、続いて古いリソースをCOSバケットに同期させる必要があります（[COSCMDツール](https://intl.cloud.tencent.com/document/product/436/10976)または[COS Migrationツール](https://intl.cloud.tencent.com/document/product/436/15392)を使用できます）。**これを行わなければ、古いリソースをバックエンドで正常にプレビューできなくなります**。同期が完了すると、back-to-origin設定を有効化できます。以下を参照して[back-to-originの設定](#1)を行うことができます。
>

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

