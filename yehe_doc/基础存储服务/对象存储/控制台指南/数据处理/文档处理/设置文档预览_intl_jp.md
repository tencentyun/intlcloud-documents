## 概要

COSコンソールによってバケット内のドキュメントをプレビューすることができます。ここではコンソールによってCOSのドキュメントプレビュー機能を使用する方法についてご説明します。ドキュメントプレビューに関する説明は、[ドキュメントプレビューの概要](https://intl.cloud.tencent.com/document/product/436/49159)をご参照ください。


>!
>- ドキュメントプレビュー機能は中国大陸のパブリッククラウドリージョンおよびシリコンバレー、バージニア、フランクフルト、シンガポールリージョンでサポートしています。このうちシンガポールとシリコンバレーリージョンは、現時点ではドキュメントの画像変換プレビューのみサポートしています。
>- ドキュメントプレビュー機能は有料項目であり、Cloud Infiniteによって課金されます。具体的な料金については[課金と価格](https://intl.cloud.tencent.com/document/product/1045/33431)をご参照ください。


## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションで**バケットリスト**をクリックし、ドキュメントプレビュー機能を有効化したいバケットをクリックし、バケット管理ページに進みます。
3. 左側の**データ処理 > ドキュメント処理**をクリックし、**ドキュメント処理**の設定項目で**編集**をクリックし、ステータスを有効に変更します。
4. 有効化すると、ドキュメントのURLにパラメータを追加する方法でプレビューを行うことができます。パラメータの使用方法と説明は次のとおりです。
```plaintext
<BucketName-APPID>.cos.<Region>.myqcloud.com/<objectkey>?ci-process=doc-preview&page=<page>&srcType=<srcType>
```
 - objectkey：オブジェクトキーです。わかりやすく言えばファイルパスのことです。
 - ci-process：Cloud Infiniteの処理機能であり、ドキュメントプレビューでは常にdoc-previewとなります。
 - page：変換したいドキュメントのページ番号です。1からカウントします。
 - srcType：ソースデータの拡張子のタイプです。現在ドキュメントの変換では、COSオブジェクトの拡張子名に基づいてソースデータのタイプを決定します。COSオブジェクトに拡張子名がない場合は、この値を設定できます。


>! URL方式を使用した場合は、シングルページのドキュメントまたはマルチページドキュメントの1ページ目のみ処理が可能です。より多くの内容をプレビューしたい場合は、[ドキュメントプレビュー API](https://intl.cloud.tencent.com/document/product/436/49404)をご利用ください。
>
