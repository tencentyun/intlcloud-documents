## 概要

オブジェクト（Object）とはCloud Object Storage（COS）の基本ユニットであり、画像、ドキュメント、オーディオビデオファイルなどのあらゆるフォーマットタイプのデータであると理解することができます。バケット（Bucket）はオブジェクトのキャリアであり、各バケットには任意の数量のオブジェクトを格納できます。オブジェクトはCOSにおいて様々なストレージタイプを指定できます。詳細については、[ストレージタイプの概要](https://intl.cloud.tencent.com/document/product/436/30925)をご参照ください。

各オブジェクトはオブジェクトキー（ObjectKey）、オブジェクト値（Value）、オブジェクトメタデータ（Metadata）で構成されます。

- オブジェクトキー（ObjectKey）：オブジェクトキーはオブジェクトのバケット内での固有識別子であり、わかりやすく言えば、ファイルパスであると理解することができます。API、SDKの例では、オブジェクトの命名フォーマットは`<ObjectKey>`となります。
- オブジェクト値（Value）：アップロードしたオブジェクト自体であり、わかりやすく言えば、ファイルの内容（Object Content）であると理解することができます。
- オブジェクトメタデータ（Metadata）：一対のキーバリューペアであり、わかりやすく言えば、ファイルの変更時間、ストレージタイプなどのファイルの属性であると理解することができます。オブジェクトをアップロード後に照会することができます。


## オブジェクトキー

Tencent Cloud COS内のオブジェクトは有効なオブジェクトキーを持つ必要があります。オブジェクトキー（ObjectKey）はオブジェクトのバケット内での固有識別子です。
例：オブジェクトアクセスアドレス`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/folder/picture.jpg`において、オブジェクトキーは`folder/picture.jpg`です。

### 命名ルール

- オブジェクトキーの名称には任意のUTF-8文字を使用できます。他のアプリケーションとの間での互換性を最大限に確保するため、名前には大文字と小文字のアルファベット、数字[a-z、A-Z、0-9]およびそれらの組み合わせを使用することをお勧めします。
- コードの長さは最大850バイトまでです。
- スラッシュ`/`またはバックスラッシュ<code>\\</code>で始めることはできません。
- オブジェクトキーではASCII制御文字のうち、上矢印(↑)、下矢印(↓)、右矢印(→)、左矢印(←)をサポートしておらず、それぞれCAN(24)、EM(25)、SUB(26)、ESC(27)に対応します。
- `*`、`%`などの特殊文字を直接ファイル名に使用することはできるだけ避けます。

>? ユーザーがアップロードしたファイルまたはフォルダの名前に中国語が含まれている場合、このファイルまたはフォルダへのアクセスおよびリクエストの際、中国語部分はURL Encodeルールに従ってパーセントエンコーディングに変換されます。
> 例：`文档.doc`にアクセスする場合、オブジェクトキーは`文档.doc`ですが、実際に読みとるものはURL Encodeルールに従って変換されたパーセントエンコーディングの`%e6%96%87%e6%a1%a3.doc`となります。
> 


有効なオブジェクトキー命名の例を次に示します。
- doc/exampleobject
- my.great_photos-2016/01/me.jpg
- videos/2016/birthday/video.wmv

#### 特殊文字

文字の中には、オブジェクトキー内では16進数形式でURL内でエンコードまたは引用しなければならないものがあり、中には印刷できないものもあります。このためこのような文字はブラウザで処理できない可能性があり、特殊な処理が必要となります。特殊処理が必要な可能性がある文字は次のとおりです。

<table>
   <tr>
	 <td>,</td>
      <td>:</td>
      <td>;</td>
      <td>=</td>
   </tr>
   <tr>
      <td>&</td>
      <td>$</td>
      <td>@</td>
      <td>+</td>
   </tr>
   <tr>
      <td>?</td>
      <td>ASCII文字範囲：00-1F 16進数（0-31 10進数）および7F（127 10進数）</td>
      <td>（スペース）</td>
      <td></td>
   </tr>
</table>


また、いくつかの文字は、アプリケーションプログラム間で整合性を保つために大量の特殊処理を必要とするため、使用を避けることをお勧めします。避ける必要がある文字は次のとおりです。
<table>
   <tr>
      <td>`</td>
      <td>^</td>
      <td>"</td>
      <td>\</td>
   </tr>
   <tr>
      <td>{</td>
      <td>}</td>
      <td>[</td>
      <td>]</td>
   </tr>
   <tr>
      <td>~</td>
      <td>%</td>
      <td>#</td>
      <td>|</td>
   </tr>
   <tr>
      <td>*</td>
      <td>></td>
      <td><</td>
      <td>ASCII <br> 128-255 10進数</td>
   </tr>
</table>

### オブジェクトアクセスアドレス

オブジェクトのアクセスアドレスはバケットアクセスアドレスとオブジェクトキーで構成されます。その構造形式は`<バケットドメイン名>/<オブジェクトキー>`です。
例：オブジェクト`exampleobject.txt`を広州（華南）のバケット`examplebucket-1250000000`にアップロードする場合、`exampleobject.txt`のアクセスアドレスは`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject.txt`となります。

### フォルダとディレクトリ

COS自体にはフォルダやディレクトリの概念がないため、COSはオブジェクト`project/a.txt`をアップロードしても、`project`フォルダを作成するわけではありません。ユーザーの使用上の習慣に沿って、COSはコンソール、COS browserなどのグラフィックツールで「フォルダ」または「ディレクトリ」という表示方法を疑似的に再現しています。具体的には、キーの値が`project/`、内容が空のオブジェクトを作成することで、従来のフォルダを模した表示方法を実現します。

例：API、SDKによってオブジェクト`project/doc/a.txt`をアップロードし、区切り記号`/`で「フォルダ」の表示方式を再現すると、コンソール上で「フォルダ」`project`および`doc`が見えるようになります。このうち`doc`は`project`の1つ下のレベルの「フォルダ」であり、`a.txt`が含まれます。

>! バケット内で様々なオブジェクトが様々な分散型クラスター内にフラットに分散している場合は、あるオブジェクトキーのプレフィックス容量のサイズを直接取得することはできず、各オブジェクトのサイズを累計することでしか取得できません。
>

フォルダおよびディレクトリの削除操作を行う場合は、状況は比較的複雑になります。詳細は次のとおりです。

| 削除経路 | オブジェクトまたはフォルダの削除  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                            | 結果                                                         |
| -------- | --------------------------------- | ------------------------------------------------------------ |
| コンソール   | フォルダ`project`                  | オブジェクトキーのプレフィックスが`project/`である全オブジェクトが削除されます               |
| コンソール   | オブジェクト`project/doc/a.txt`          | `project`および`doc`フォルダは維持されます                            |
| API、SDK | オブジェクト`project/`または`project/doc/` | オブジェクト`project/doc/a.txt`は維持されます。フォルダ内のオブジェクトを一括削除したい場合は、 コードトラバーサルによってフォルダ内のオブジェクトの削除機能を実現する必要があります|


## オブジェクトメタデータ

オブジェクトメタデータはオブジェクト内の一対のキーバリューペアであり、サーバーがHTTPプロトコルによってHTML資料をブラウザに渡す前に送信する文字列で、HTTP Headerとも呼ばれます。オブジェクトのアップロード時にHTTP Headerを変更することで、ページのレスポンス形式を変更したり、キャッシュ時間の変更などの設定情報を伝達したりすることもできます。 

オブジェクトメタデータには、システムメタデータとユーザー定義のメタデータという2種類のメタデータがあります。

>? オブジェクトのHTTP Headerを変更してもオブジェクト自体は変更されません。
>

### システムメタデータ

オブジェクトの属性情報、例えばオブジェクトの変更時間、オブジェクトサイズ、ストレージタイプなどを指します。

<table>
<thead>
<tr>
<th width="25%">名称</th>
<th width="75%">説明</th>
</tr>
</thead>
<tbody><tr>
<td>Content-Length</td>
<td>RFC 2616で定義されたHTTPリクエスト内容の長さ（バイト）</td>
</tr>
<tr>
<td>Last-Modified</td>
<td>オブジェクトの作成日または前回変更日（どちらか遅い方）</td>
</tr>
<tr>
<td>x-cos-version-id</td>
<td>オブジェクトバージョンID。バケット上でバージョン管理を有効にしている場合は、オブジェクトのバージョンIDが返され、同一オブジェクトの過去のバージョンの識別に用いることができます</td>
</tr>
<tr>
<td>ETag</td>
<td>PUT Objectによってアップロードしたオブジェクトの場合は、アップロードされたファイルコンテンツのMD5値であり、マルチパートアップロードまたは過去のバージョンのAPIを使用してアップロードしたオブジェクトの場合は、アップロードされたファイルコンテンツの一意のIDです。検証機能は有していません</td>
</tr>
</tbody></table>



### ユーザー定義のメタデータ

Content-Type，Cache-Control，Expires，x-cos-meta-\* などの、オブジェクトのカスタマイズパラメータのことです。具体的な情報については[カスタムオブジェクトHeaders](https://intl.cloud.tencent.com/document/product/436/13361)をご参照ください。

<table>
<thead>
<tr>
<th width="25%">名称</th>
<th width="76%">説明</th>
</tr>
</thead>
<tbody><tr>
<td>Cache-Control</td>
<td>RFC 2616で定義されたキャッシュポリシー。オブジェクトメタデータとして保存されます</td>
</tr>
<tr>
<td>Content-Disposition,<br>Content-Encoding,<br>Content-Type</td>
<td>RFC 2616で定義されたファイル名/エンコード形式/コンテンツタイプ（MIME）。オブジェクトメタデータとして保存されます</td>
</tr>
<tr>
<td>Expires</td>
<td>RFC 2616で定義されたキャッシュ失効時間。オブジェクトメタデータとして保存されます</td>
</tr>
<tr>
<td>x-cos-acl</td>
<td>オブジェクトのアクセス制御リスト（ACL）の属性を定義します。有効値：private、public-read-write、public-read。デフォルト値：private</td>
</tr>
<tr>
<td>x-cos-grant-*</td>
<td>被付与者にある種の権限を付与します</td>
</tr>
<tr>
<td>x-cos-meta-*</td>
<td>ユーザーによるカスタマイズが許可されたヘッダー情報。オブジェクトメタデータとして返されます（サイズ制限2K）</td>
</tr>
<tr>
<td>x-cos-storage-class</td>
<td>オブジェクトのストレージレベルを設定します。列挙値：STANDARD、STANDARD_IA、ARCHIVE、デフォルト値：STANDARD</td>
</tr>
<tr>
<td>x-cos-server-side-encryption</td>
<td>オブジェクトに対しサーバー側での暗号化を有効にするかどうか、および暗号化方式を指定します</td>
</tr>
</tbody></table>


## オブジェクト操作

ユーザーはTencent Cloudコンソール、ツール、API、SDKなどの複数の方式でオブジェクトを管理することができます。

>!アップロード方式はサポートする最大アップロードファイルサイズによって、[シンプルアップロード](https://intl.cloud.tencent.com/document/product/436/14113)と[マルチパートアップロード](https://intl.cloud.tencent.com/document/product/436/14112)の2種類に分けられます。
>- シンプルアップロードを使用する場合、オブジェクトサイズは5GB以内に制限されます。
>- マルチパートアップロードを使用する場合、各パートのサイズ制限は5GB以内であり、パート数は10000未満とする必要があるため、アップロードできるオブジェクトは最大で約48.82TBとなります。制限に関するその他の説明については、[仕様と制限](https://intl.cloud.tencent.com/document/product/436/14518)をご参照ください。

オブジェクトのアップロード完了後、ユーザーはコンソール上でオブジェクトについて関連の設定を行うことができます。具体的には次の内容をご参照ください。

- [オブジェクトの検索](https://intl.cloud.tencent.com/document/product/436/13325)
- [オブジェクト情報の確認](https://intl.cloud.tencent.com/document/product/436/13326)
- [オブジェクトのアクセス権限の設定](https://intl.cloud.tencent.com/document/product/436/13327)
- [カスタムHeadersの設定](https://intl.cloud.tencent.com/document/product/436/13361)

## オブジェクトサブリソース

COSにはバケットとオブジェクトにバインドされたサブリソースがあります。サブリソースはオブジェクトに従属するものであり、サブリソースはそれ自体で存在することはなく、常に他のエンティティ（オブジェクトまたはバケットなど）にバインドされます。アクセス制御リスト（Access Control List）は特定のオブジェクトへのアクセス制御情報のリストであり、これはCOS内のオブジェクトのサブリソースです。

アクセス制御リストには、権限の被付与者およびその付与された許可を識別できる権限リストが含まれ、これによってオブジェクトへのアクセス制御を実現しています。オブジェクトの作成時に、ACLはオブジェクトを完全に制御できるオブジェクト所有者を識別します。ユーザーはオブジェクトのACLを検索することや、ACLを更新された権限リストに置き換えることができます。

>? ACLに更新があった場合は必ず現在のACLを置き換える必要があります。
>

## アクセス権限のタイプ

COSではオブジェクトに、**パブリック権限**と**ユーザー権限**という2種類の権限タイプを設定することができます。
**パブリック権限**：継承権限、プライベート読み取り/書き込みおよびパブリック読み取り/プライベート書き込みが含まれます。
- 継承権限：オブジェクトがバケットの権限を引き継ぎ、バケットのアクセス権限と一致させます。オブジェクトにアクセスした際、COSが読み取ったオブジェクトの権限がバケットの継承権限であれば、バケットの権限とマッチさせ、アクセスに応答します。何らかの新しいオブジェクトが追加された場合も、バケットの権限はデフォルトで継承されます。
- プライベート読み取り/書き込み：オブジェクトにアクセスした際、COSが読み取ったオブジェクトの権限がプライベート読み取り/書き込みであれば、バケットにどのような権限が設定されていても、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)がなければオブジェクトにアクセスできません。
- パブリック読み取り/プライベート書き込み：オブジェクトにアクセスした際、COSが読み取ったオブジェクトの権限がパブリック読み取りであれば、バケットにどのような権限が設定されていても、オブジェクトはすべて直接ダウンロードできます。

**ユーザー権限**：ルートアカウントはデフォルトではオブジェクトのすべての権限を所有しています（完全制御）。このほかCOSはサブアカウントに対するデータ読み取り、データ書き込み、権限読み取り、権限書き込み、さらには完全制御の最高権限の付与もサポートしています。

#### 適用ケース
プライベート読み取り/書き込みのバケットで、特定のオブジェクトにパブリックアクセス許可設定を行うこと、またはパブリック読み取り/書き込みのバケットで、特定のオブジェクトへのアクセスに認証が必要となるように設定することができます。
