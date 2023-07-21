

Cloud Object Storage（COS）とは、Tencent Cloudが提供する、大量のファイルを保存するための分散型ストレージサービスです。ユーザーはネットワークを介していつでもデータを保存および確認することができます。Tencent Cloud COSはすべてのユーザーに対し、拡張性に優れ、低コストで、信頼性と安全性の高いデータストレージサービスの使用を可能にします。

COSはコンソール、API、SDKおよびツールなどの多様な方式で、簡単かつスピーディーに接続でき、大量のデータの保存と管理を実現します。COSでは任意の形式のファイルのアップロード、ダウンロードおよび管理が可能です。 Tencent Cloudは直感的なWeb管理インターフェースを提供しており、また全国に広がるCDNノードによってファイルダウンロードのアクセラレーションを行うことができます。



## 製品の機能

COSは、幅広い企業および個人ユーザー向けにデータ管理、リモート障害復旧、データアクセスアクセラレーション、データ処理などの機能を提供し、様々なシナリオをカバーします。詳細は、[機能の概要](https://intl.cloud.tencent.com/document/product/436/8186)のドキュメントをご参照ください。

## 基本概念

Tencent Cloud COSについてさらによく理解していただけるよう、次のいくつかの用語の概念をご説明します。

- [バケット（bucket）](https://intl.cloud.tencent.com/document/product/436/13312) ：オブジェクトのキャリアであり、オブジェクトを入れておくための「容器」と理解することができます。1つのバケットには無数のオブジェクトを格納できます。
- [オブジェクト（Object）](https://intl.cloud.tencent.com/document/product/436/13324)：COSの基本ユニットであり、画像、ドキュメント、オーディオビデオファイルなどのあらゆるフォーマットタイプのデータを理解することができます。
- [リージョン（Region）](https://intl.cloud.tencent.com/document/product/436/6224)：Tencent Cloudのホスティングデータセンターが分布する地域です。COSのデータはこれらのリージョンのバケット内に保存されます。
- [アクセスドメイン名（Endpoint）](https://intl.cloud.tencent.com/document/product/436/6224)：バケットに保存されたオブジェクトに、ユーザーはアクセスドメイン名を通じてアクセスし、オブジェクトをダウンロードすることができます。
- [ストレージタイプ（StorageClass）](https://intl.cloud.tencent.com/document/product/436/30925)：COS内のオブジェクトのストレージレベルとアクティビティレベルのことです。COSは、標準ストレージ（マルチAZ）、低頻度ストレージ（マルチAZ）、INTELLIGENT_TIERINGストレージ（マルチAZ）、INTELLIGENT_TIERINGストレージ、標準ストレージ、低頻度ストレージ、アーカイブストレージ、ディープアーカイブストレージという複数のストレージタイプを提供しています。それぞれのストレージタイプは異なる業務シナリオに適しており、異なる特性（オブジェクトのアクセス頻度、アクセスレイテンシーなど）を持っています。各ストレージタイプの詳細については、[ストレージタイプの概要](https://intl.cloud.tencent.com/document/product/436/30925)をご参照ください。



## COSの利用方法

### 初心者向け（入門編）

COSでは、COSの理解や活用に役立つツールやビデオガイドなど、豊富で包括的なラーニングパスを提供しています。詳細については[初心者向け（入門編）COS](https://www.tencentcloud.com/products/cos)をご参照ください。


### 利用方法

COSはユーザーに対し様々な利用方法をご提供しています。具体的な説明は下表をご参照ください。

<table>
<thead>
<tr>
<th align="left" width="30%">クイックスタート方式</th>
<th align="left" width="70%">機能説明</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/32955">コンソール</a></td>
<td align="left" width="70%">COSコンソールは、COSユーザーのための、最も簡単でスタートしやすい操作方法です。ユーザーはコードを記述したりプログラムを実行したりする必要はなく、COSコンソールから直接COSサービスを利用できます。</td>
</tr>
<tr>
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





## COSはどのように課金されますか。

COSのデフォルトの課金方式は従量課金（後払い）となります。また一部の課金項目はお得な割引のあるリソースパック（前払い）方式で充当することもできます。詳細については、[課金概要](https://intl.cloud.tencent.com/document/product/436/16871)のドキュメントをご参照ください。


