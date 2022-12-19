Cloud Object Storage（COS）は署名付きURLを使用したオブジェクトのアップロード、ダウンロードをサポートしています。その原理は、URLに署名を埋め込んで署名付きリンクを生成するものです。署名の有効期限によって、署名付きURLの有効期間を管理することができます。

署名付きURLを使用してダウンロードを行い、一時URLを取得してファイル、フォルダの一時的な共有に用いることができます。あるいは長い署名有効期間を設定することで、長期間有効なURLを取得し、ファイルの長期的な共有に用いることもできます。詳細については、[ファイルの共有](#ファイルの共有)をご参照ください。

また、署名付きURLを使用してアップロードを行うこともできます。詳細については、[ファイルのアップロード](#ファイルのアップロード)をご参照ください。

<span id="ファイルの共有"></span>
## ファイルの共有（ファイルのダウンロード）

COSはオブジェクトの共有をサポートしています。署名付きURLを使用することで、ファイルやフォルダを他のユーザーと期限付きで共有することができます。署名付きURLの原理は、署名をオブジェクトURLに埋め込んで結合するものです。その後の署名生成アルゴリズムについては、[リクエスト署名](https://intl.cloud.tencent.com/document/product/436/7778)をご参照ください。

バケットはデフォルトではプライベート読み取りであり、オブジェクトのURLから直接ダウンロードしようとするとアクセスエラーが表示されます。オブジェクトURLの後に有効な署名を結合すると、**署名付きURL**を取得できます。署名にはID情報が含まれるため、署名付きURLはオブジェクトのダウンロードに用いることができます。

>?やむを得ずパーマネントキーを使用して署名付きURLを生成する場合は、リスク回避のため、パーマネントキーの権限の範囲をアップロードまたはダウンロード操作のみに限定することをお勧めします。また、生成した署名の有効期間を、今回のアップロードまたはダウンロード操作に必要な最短の期限までに設定し、指定した署名付きURLの有効期限が過ぎるとリクエストが中断するようにします。失敗したリクエストは新しい署名を申請後に再度実行する必要があります。中断からの再開はサポートしていません。

```
// オブジェクトURL
https://test-12345678.cos.ap-beijing.myqcloud.com/test.png

// 署名付きURL（署名値を結合したオブジェクトURL）
https://test-12345678.cos.ap-beijing.myqcloud.com/test.png?q-sign-algorithm=sha1&q-ak=xxxxx&q-sign-time=1638417770;1638421370&q-key-time=1638417770;1638421370&q-header-list=host&q-url-param-list=&q-signaturexxxxxfxxxxxx6&x-cos-security-token=xxxxxxxxxxxx
```
次にファイル共有の方法をいくつかご紹介します。これらの方法は本質的にはすべて署名を自動生成し、オブジェクトURLの後ろに結合することで、ダウンロードやプレビューに直接用いることができる一時リンクを生成するものです。


### 一時リンクのクイック取得（有効期間1～2時間）

コンソールまたはCOSBrowserツールによってオブジェクトの一時リンクをクイック取得することができます。

#### コンソール（Webページ）

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、バケット名をクリックし、「ファイルリスト」に進み、オブジェクトの**詳細**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/aff68724b740f962e39cf1167ac2cb5b.png)
2. オブジェクトの詳細ページに進み、一時リンクをコピーします。有効期間は1時間です。
![](https://qcloudimg.tencent-cloud.cn/raw/6b6b17a56e82af5c5af9143338806fc3.png)

#### COSBrowser（クライアント）

ドキュメント[ファイルリンクの発行](https://intl.cloud.tencent.com/document/product/436/32565)を参照し、ルートアカウントキーを使用して最長2時間の一時リンクを取得することができます。サブアカウントキーを使用する場合は、最長1.5日間の一時リンクを取得することができます。

### 時間をカスタマイズした一時リンクの取得

#### 署名ツールの使用

**適するケース：プログラミングに不慣れなユーザー**

操作手順は次のとおりです。
1. ファイルリンク：[COSコンソール]( https://console.cloud.tencent.com/cos5)にログインし、オブジェクトの詳細から、署名のない「オブジェクトアドレス」を取得します。
2. [APIキー管理](https://console.cloud.tencent.com/cam/capi)からSecretIdとSecretKeyを取得します。
3. COS署名ツールをクリックし、署名リンクを取得します。
有効期間：秒、分、時間、日レベルの設定をサポートします。


#### SDKを使用した署名付きURLの一括取得

**適するケース：一時リンクを一括取得したい場合、プログラミングの基礎を習得したユーザー**

コンソールおよびCOSBrowserから取得する一時リンクは有効期間が短いため、より長時間の一時リンクが必要な場合は、SDKを使用して署名付きURLを生成し、署名の有効期間の管理を実現することもできます。生成メソッドについては[署名付きURLによるダウンロード権限承認](https://intl.cloud.tencent.com/document/product/436/14116)を参照し、使いやすい開発言語を選択してください。

署名付きURLの生成には一時キーまたはパーマネントキーを使用することができます。両者の違いは、一時キーの最長有効期間は36時間以内であり、パーマネントキーには有効期限がないという点です。このことは署名付きURLの有効期間に間接的な影響を与えます。

**パーマネントキーを使用した署名付きURLの生成（任意の期間）**

パーマネントキーには有効期限がないため、署名付きURLの有効期間は設定した署名の有効期間によって決まります。SDKの署名付きURL生成メソッドを直接呼び出すことができます。操作手順は次のとおりです。
1. secret_id、secret_key、regionなどを入力してclientを初期化します。
2. バケット名、オブジェクト名、署名の有効期間を入力し、時間をカスタマイズした署名付きURLを生成します。詳細については下記の各言語のSDKドキュメントをご参照ください。
<table>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37680">Android SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31520">C SDK</td>
<td><a href="https://cloud.tencent.com/document/product/436/35163">C++ SDK</td>
<td><a href="https://cloud.tencent.com/document/product/436/32873">.NET SDK</a>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31528">Go SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37690">iOS SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31536">Java SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31540">JavaScript SDK</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32455">Node.js SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31544">PHP SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31548">Python SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31711">ミニプログラムSDK</a></td>
</tr>
</table>


**一時キーを使用した署名付きURLの生成（36時間以内）**

フロントエンドデータの直接転送のケースでは、一時キーの使用が必要な場合が多くあります。一時キーの説明と生成ガイドについては次をご参照ください。
- [一時キーを使用したCOSアクセス](https://intl.cloud.tencent.com/document/product/436/45242)
- [一時キーの生成および使用ガイド](https://intl.cloud.tencent.com/document/product/436/14048)
- [COSへのフロントエンド直接転送に用いる一時キーのセキュリティガイド](https://intl.cloud.tencent.com/document/product/436/35265)

一時キーは最長36時間までであり、署名付きURLの有効期間は設定した署名の有効期間と一時キーの有効期間の最小値から決定されます。設定した署名の有効期間をX、一時キーの有効期間をY、リンクの実際の有効期間をTとします。
```
T=min(X,Y)。X<=36のため、T<=36です。
```
一時キーを使用して署名付きURLを生成するには、次の2つの手順が必要です。
1. [一時キーの取得](https://intl.cloud.tencent.com/document/product/436/14048#.E8.8E.B7.E5.8F.96.E4.B8.B4.E6.97.B6.E5.AF.86.E9.92.A5)を行います。
2. 一時キーを取得すると、パーマネントキーに類似した関数を使用して署名付きURLを生成できるようになります。一時キーを使用してclientを初期化する場合、SecretId、SecretKeyの入力のほかにtokenも入力し、パラメータ`x-cos-security-token`も含める必要があることに注意が必要です。詳細については、下記の各言語のSDKドキュメントをご参照ください。
<table>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37680">Android SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31520">C SDK</td>
<td><a href="https://cloud.tencent.com/document/product/436/35163">C++ SDK</td>
<td><a href="https://cloud.tencent.com/document/product/436/32873">.NET SDK</a>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31528">Go SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37690">iOS SDK</a>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31536">Java SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31540">JavaScript SDK</a></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32455">Node.js SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31544">PHP SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31548">Python SDK</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31711">ミニプログラムSDK</a></td>
</tr>
</table>

<span id="ファイルのアップロード"></span>
## フォルダの共有

フォルダは一種の特殊なオブジェクトであり、コンソールまたはCOSBrowser ツールを使用してフォルダを共有することができます。詳細については、[フォルダの共有](https://intl.cloud.tencent.com/document/product/436/42387)をご参照ください。

## ファイルのアップロード
第三者がオブジェクトをバケットにアップロードできるようにし、なおかつ相手にCAMアカウントまたは一時キーなどの方法を使用させたくない場合は、署名付きURLを使用して署名を第三者に渡し、一時的なアップロード操作を完了させることができます。有効な署名付きURLを受領した人は誰でもオブジェクトをアップロードできます。

>?やむを得ずパーマネントキーを使用して署名付きURLを生成する場合は、リスク回避のため、パーマネントキーの権限の範囲をアップロードまたはダウンロード操作のみに限定することをお勧めします。また、生成した署名の有効期間を、今回のアップロードまたはダウンロード操作に必要な最短の期限までに設定し、指定した署名付きURLの有効期限が過ぎるとリクエストが中断するようにします。失敗したリクエストは新しい署名を申請後に再度実行する必要があります。中断からの再開はサポートしていません。

- 手段1：SDKを使用した署名付きURLの生成
各言語のSDKがアップロード署名付きURLの生成メソッドを提供しています。生成メソッドについては、[署名付きURLによるアップロード権限承認](https://intl.cloud.tencent.com/document/product/436/14114)を参照し、使いやすい開発言語を選択してください。
- 手段2：ご自身での署名リンクの結合
署名付きURLは実際にはオブジェクトURLの後に署名を結合したものです。このため、SDK、署名生成ツールなどによってご自身で署名を生成し、URLと署名を結合して署名リンクとし、オブジェクトのアップロードに用いることもできます。ただし、署名生成のアルゴリズムは複雑なため、一般的な状況ではこの方法の使用は推奨されません。
