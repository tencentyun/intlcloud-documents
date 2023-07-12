シンプルアップロードとは、ユーザーがPUT Objectインターフェースを使用してオブジェクトをアップロードすることを言います。シンプルアップロード方式は単一のリクエストに適用でき、5GB以下の単一のオブジェクトのアップロードに用いられます。

5GBを超える単一のオブジェクトのアップロードには、次の方式を用いることができます。

- コンソールを使用するアップロード：コンソールでは最大512GBまでの単一のオブジェクトのアップロードをサポートしています。詳細については、[オブジェクトのアップロード](https://intl.cloud.tencent.com/document/product/436/13321)のコンソールガイドドキュメントをご参照ください。
- API/SDKを使用するマルチパートアップロード：最大48.82TB（50000GB）までの単一のオブジェクトのアップロードをサポートしています。詳細については[マルチパートアップロード](https://intl.cloud.tencent.com/document/product/436/14112)をご参照ください。
- COSCMDツールを使用するアップロードでは最大40TBまでの単一のオブジェクトのアップロードをサポートしています。詳細については、[COSCMDツール](https://intl.cloud.tencent.com/document/product/436/10976)をご参照ください。

>? アップロードリクエストを送信する際、指定のフォルダまたはパスにアップロードしたい場合は、`/`を使用します。例えば、picture.pngをdocフォルダにアップロードする場合は、オブジェクトキーをdoc/picture.pngと設定します。
>

## ユースケース

シンプルアップロード方式は5GB以下のオブジェクトをアップロードするケースに適用できます。

高帯域幅または脆弱なネットワーク環境においては、100MBを超えるような比較的大きなオブジェクト（5GB未満であっても）をアップロードする必要がある場合は、[マルチパートアップロード](https://intl.cloud.tencent.com/document/product/436/14112)方式を優先的に使用することをお勧めします。マルチパートアップロード方式では複数の分割ファイルの転送を同時実行することが可能なためです。高帯域幅環境ではリソースを有効利用でき、脆弱なネットワーク環境では、単一の分割ファイルのアップロード失敗が他のアップロード済みのファイルに影響を与えることがなく、簡単なリトライで失敗したファイルの再アップロードが可能なため、全体的なアップロード成功率を向上させることができます。モバイル端末での脆弱なネットワーク環境におけるアップロードに関しては、[脆弱なネットワークにおけるマルチパートアップロード再開の実践](https://intl.cloud.tencent.com/document/product/436/30932)をご参照ください。


## 利用方法

### REST APIの使用

REST APIを直接使用してオブジェクトのシンプルアップロードリクエストを送信できます。 詳細については、[PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)のAPIドキュメントをご参照ください。

### SDKの使用
SDKのオブジェクトシンプルアップロードメソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。
- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/38062)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43881)


