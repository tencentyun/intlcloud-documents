COS Select機能は、COS上に保存されたオブジェクトを構造化問い合わせ言語（SQL）によってフィルタリングすることで、オブジェクトを検索してユーザーが必要とするデータを取得するために役立てるものです。COS Select機能によってオブジェクトデータをフィルタリングすることで、COSの転送データ量を削減することができ、そのデータの検索に必要なコストと遅延を減少させることができます。

COS Select機能は現在CSV、JSON、Parquet形式によるストレージオブジェクトの検索、GZIPまたはBZIP2で圧縮されたオブジェクト（CSV、JSON形式のオブジェクトのみ）の検索をサポートしています。また、COS Select機能は結果の形式をCSVまたはJSONに指定することができるほか、結果の記録の区切り形式を決定することができます。

リクエストの中でSQL式をCOSに伝達することができます。COS Selectは現時点では一部のSQL式のみサポートしています。COS SelectがサポートするSQL式についての詳しい情報は、[SQL関数](https://intl.cloud.tencent.com/document/product/436/32474)のドキュメントをご参照ください。

COSコンソール、API、SDK、COSCMDなどの方法でSQL照会を実行することができます。COSコンソールを使用したファイル検索には一定の制限があり、検索できるファイルは最大128Mまでで、返されるデータ量は40MBに限られる点に注意が必要です。より多くのデータを検索したい場合は、その他の方法を使用して行ってください。

>?
>- COS Selectがサポートするデータタイプおよび現在の予約フィールドについて詳しくお知りになりたい場合は、[データタイプ](https://intl.cloud.tencent.com/document/product/436/32476)および[予約フィールド](https://intl.cloud.tencent.com/document/product/436/32475)をご参照ください。
>- 現在検索機能は中国大陸のパブリッククラウドリージョンのみサポートしており、他のリージョンでは現時点ではこの機能をサポートしていません。

## 使用制限

COS Selectを使用する際は次の制限があります。

- 照会するオブジェクトの`cos:GetObject`権限を有している必要があります。ルートアカウントはデフォルトでこの権限を有しています。
- 標準ストレージタイプのオブジェクトの検索のみサポートします。
- SQL式の長さは最大256KBまでです。
- 検索結果の中の1つのレコードの長さは最大1MBまでです。

COS Select機能は現在次のSQL句をサポートしています。

- SELECTステートメント
- FROM句
- WHERE句
- LIMIT句

>?SQL句に関する詳細情報については、[Selectコマンド](https://intl.cloud.tencent.com/document/product/436/32473)をご参照ください。

COS Selectが現在サポートしている関数は次のとおりです。

- 集計関数：AVG関数、COUNT関数、MAX関数、MIN関数、SUM関数など。
- 条件関数：COALESCE関数、NULLIF関数など。
- 変換関数：CAST関数など。
- 日付関数：DATE_ADD関数、DATE_DIFF関数、EXTRACT関数、TO_STRING関数、TO_TIMESTAMP関数、UTCNOW関数など。
- 文字列関数：CHAR_LENGTH関数、CHARACTER_LENGTH関数、LOWER関数、SUBSTRING関数、TRIM関数、UPPER関数など。

>?SQL関数に関する詳細情報については、[SQL関数](https://intl.cloud.tencent.com/document/product/436/32474)をご参照ください。

COS Selectは現在次の演算子をサポートしています。

- 論理演算子：`AND，NOT，OR`
- 比較演算子：`<，>，<=，>=，=，<>，!=，BETWEEN，IN`
- パターンマッチ演算子：`LIKE`
- 算術演算子：`+，-，*，%`

>?演算子に関する詳細情報については、[演算子](https://intl.cloud.tencent.com/document/product/436/32477)をご参照ください。



## 検索リクエストの発行

コンソール、API、SDKなどの複数の方式を使用して検索リクエストを発行することができます。

- コンソールを使用する場合は、[データ検索](https://intl.cloud.tencent.com/document/product/436/32538)のドキュメントを参照して操作を行うことができます。
- APIを使用する場合は、SELECT Object ContentAPIドキュメントをご参照ください。
- SDKを使用する場合は、[SDKの概要](https://intl.cloud.tencent.com/document/product/436/6474)で、必要なSDKインターフェースを選択することができます。

## よくあるご質問

照会の実行を試した際に問題が発生した場合、COS Selectはエラーコードおよび関連のエラーメッセージを返します。                      
