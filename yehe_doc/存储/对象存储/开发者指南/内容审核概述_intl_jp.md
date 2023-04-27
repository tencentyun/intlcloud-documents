## 概要

COSコンテンツ審査サービスは、画像、ビデオ、オーディオ、テキスト、ドキュメント、ウェブページなどのマルチメディアのコンテンツセキュリティのインテリジェント審査を提供するサービスです。ユーザーが、ポルノ・低俗、違法・不正、不快感を与えるなどの禁止コンテンツを効果的に識別し、運営リスクを回避できるようにサポートします。現在以下のタイプのファイル形式によるコンテンツ審査をサポートしています。

| ファイルタイプ | 仕様制限                                                     |
| -------- | ------------------------------------------------------------ |
| 画像     | <ul  style="margin: 0;"><li>png、jpeg、jpg、bmp、webp、gif 形式をサポートします。</li><li>画像サイズは5MB以下、画像サイズは20 x 20以上であること。</li></ul> |
| ビデオ     | <ul  style="margin: 0;"><li>mp4、avi、mkv、wmv、rmvb、flv、m3u8形式をサポートします。</li><li>ビデオサイズは5GB以下、フレームキャプチャー数は1万フレーム以下であること。</li></ul> |
| オーディオ     | <ul  style="margin: 0;"><li>オーディオ形式：現在mp3、wav、aac、flac、amr、3gp、m4a、wma、ogg、apeをサポートしています。</li><li>オーディオビットレート：128Kbps-256Kbps。<li>オーディオサイズ：ファイルは600MB未満。最大時間：3時間。</li></ul> |
| テキスト     | html、 txt形式をサポートします。 ファイルサイズは1MB以下。                  |
| ライブストリーミング     | <ul  style="margin: 0;"><li>サポートするライブストリーム時間：5時間以内。</li><li>サポートするライブストリームメディアプロトコル：rmtp、hls、http、httpsなどの主要プロトコル。</li></ul>     |
| ドキュメント     | ドキュメント処理サービスにより、ドキュメントを画像に変換し、審査を行います。現在pdf、ppt、excelなど、数十種類のドキュメント形式をサポートしています。詳しくは[ドキュメントプレビュー概要](https://intl.cloud.tencent.com/document/product/436/49159)をご参照ください。 |
| ウェブページ     | ウェブページファイルに対する自動検査をサポートします。OCRテキスト認識、物体検出（エンティティ、広告ロゴ、2次元コードなど）、画像認識などのいくつかの次元から、ディープラーニング技術により、ウェブページ上の不正なコンテンツを認識します。 |


>? コンテンツ審査機能は有料項目であり、Cloud Infiniteによって課金されます。詳細な課金方式についてはCloud Infinite [コンテンツ審査料金](https://cloud.tencent.com/document/product/460/58119)をご参照ください。 
>

![](https://qcloudimg.tencent-cloud.cn/raw/f4b075ccd69c4c8e9b056a3c628a7f6e.png)

審査サービスをアクティブ化すると、以下の操作が可能になります。

- 自動審査を設定すると、バケットにアップロードしたデータに対して自動審査を行い、不正データを自動凍結します
- インターフェースを呼び出し、サードパーティーデータへの審査を行います
- バケット内の過去データに対し、1回のみバッチ審査を行います

## ユースケース

SNS、eコマース、広告、ゲームなどの分野に適しています。上述のタイプのファイルに審査を行うことができます。審査タイプには、ポルノ、違法・不正および広告配信が含まれます。

## リージョン制限

サポートするリージョンは以下のとおりです

| リージョン | リージョンの略称     |
| :--- | :----------- |
| 北京 | ap-beijing   |
| 南京 | ap-nanjing   |
| 上海 | ap-shanghai  |
| 広州 | ap-guangzhou |
| 成都 | ap-chengdu   |
| 重慶 | ap-chongqing |

その他のリージョンでコンテンツ審査機能を利用される場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)して、お問い合わせください。

## 利用方法

### COSコンソールの使用

#### 自動審査

COSコンソールで自動審査サービスを起動すれば、新しくアップロードした画像、ビデオ、オーディオ、ファイル、ドキュメント、ウェブページを自動審査できます。詳しくは、[自動審査](https://cloud.tencent.com/document/product/436/47247)をご参照ください。

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3YaP402_PRELIM__%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)


#### 過去データ審査

COSコンソールで過去データ審査サービスを起動し、バケット内にすでにある画像、ビデオ、オーディオ、テキスト、ドキュメント、ウェブページについて、1回のみバッチ審査ができます。

### APIインターフェースの使用

ご提供するAPIインターフェースを使用すれば、画像、ビデオ、オーディオ、テキスト、ドキュメント、ウェブページのコンテンツ審査を行うことができます。詳しくは、以下のAPIドキュメントをご参照ください。

- [画像審査](https://intl.cloud.tencent.com/document/product/436/48537) 
- [ビデオ審査](https://intl.cloud.tencent.com/document/product/436/48249) 
- [オーディオ審査](https://intl.cloud.tencent.com/document/product/436/48262)
- [テキスト審査](https://cloud.tencent.com/document/product/436/56287)
- [ドキュメント審査](https://cloud.tencent.com/document/product/436/59378)
- [ウェブページ審査](https://cloud.tencent.com/document/product/436/63957)
- [ライブストリーミング審査](https://cloud.tencent.com/document/product/436/76259)

審査結果がセンシティブデータの場合、ご提案として、以下のいくつかの方式から1つ選んで処理を行うことが可能です。
- ファイルアクセス権限の変更はプライベート読み取りです。ユーザーのパブリックネットワークでの匿名アクセスを根絶します。権限インターフェースの変更については [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748)をご参照ください。
- ファイルをバックアップディレクトリに移動させます。ファイルの移動は、オリジナルファイルを指定ディレクトリにコピーした後、元のファイルを削除する方式で実現できます。インターフェースについては [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)および[DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)をご参照ください。
- ファイルを削除します。インターフェースについては[DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743)をご参照ください。

### SDKの使用

ご提供する各種言語のSDKを使用すれば、画像、ビデオ、オーディオ、テキスト、ドキュメント、ウェブページのコンテンツ審査を行えます。詳しくは、以下のSDKドキュメントをご参照ください。

| SDK            | ドキュメントにアクセス                                                     |
| :------------- | :----------------------------------------------------------- |
| Android SDK    | [コンテンツ審査](https://cloud.tencent.com/document/product/436/66151) |
| C SDK          | [コンテンツ審査](https://cloud.tencent.com/document/product/436/62019) |
| .NET(C#) SDK   | [コンテンツ審査](https://cloud.tencent.com/document/product/436/55328) |
| Go SDK         | [コンテンツ審査](https://cloud.tencent.com/document/product/436/55368) |
| iOS SDK        | [コンテンツ審査](https://cloud.tencent.com/document/product/436/55359) |
| Java SDK       | [コンテンツ審査](https://cloud.tencent.com/document/product/436/55380) |
| JavaScript SDK | [コンテンツ審査](https://cloud.tencent.com/document/product/436/74611) |
| PHP SDK        | [コンテンツ審査](https://cloud.tencent.com/document/product/436/61619) |
| Python SDK     | [コンテンツ審査](https://cloud.tencent.com/document/product/436/55929) |
