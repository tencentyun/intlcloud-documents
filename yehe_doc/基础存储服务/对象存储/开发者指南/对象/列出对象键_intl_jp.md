[オブジェクトキー（ObjectKey）](https://intl.cloud.tencent.com/document/product/436/13324)はオブジェクトのバケット内での固有識別子であり、わかりやすく言えば、ファイルパスであると理解することができます。例えば、オブジェクトキーがdoc/picture.jpgである場合、画像ファイルpicture.jpgがCloud Object Storage（COS）のdocパス（またはフォルダ）下に保存されていることを表します。

オブジェクトキーのリストアップとは、指定されたオブジェクトキーに基づいて特定のオブジェクトを検索することを指します。また、オブジェクトキーのプレフィックスに基づくオブジェクトの検索、すなわちオブジェクトキーの前半の一部（docなど）を指定して、同一のプレフィックスdocを持つすべてのオブジェクトを検索することも可能です。

## ユースケース

Tencent Cloud COSではプレフィックスの順序に従ってオブジェクトキーをリストアップすることができます。また、オブジェクトキーの中で記号「/」を使用して、従来のファイルシステムに類似した階層構造を実現することも可能です。COSはまた、区切り文字による階層構造の選択と閲覧もサポートしています。

単一バケット内のすべてのオブジェクトキーをリストアップすることができます。プレフィックスのUTF-8バイナリー順序に従ってリストアップするか、または指定のプレフィックスを選択してオブジェクトキーのリストをフィルタリングすることが可能です。例えば、パラメータ`t`を入力すると`tencent`のオブジェクトがリストアップされますが、`a`またはその他の文字をプレフィックスとするオブジェクトはスキップされます。

区切り文字`/`を入力すると、この区切り文字に基づいてオブジェクトキーが再構成されます。プレフィックスと区切り文字を組み合わせることで、フォルダ検索に類似した機能を実現することができます。

Tencent Cloud COSでは1つのバケット内に無限の数のオブジェクトを格納できるため、オブジェクトキーリストが非常に大きくなる可能性があります。管理上の利便性のため、1つのオブジェクトリストアップインターフェースは最大1000個までのオブジェクトのリストを返し、同時にインジケータによって分割の有無の通知を返します。分割が存在する場合は、次のページにもオブジェクトリストが存在することを表します。インジケータおよび区切り文字によってオブジェクトキーリストアップリクエストを複数回送信することで、すべてのオブジェクトキーをリストアップすることや、必要な内容を照会することが可能になります。

## 利用方法

### COSコンソールの使用

コンソールを使用してオブジェクトを検索することができます。詳細については、[オブジェクトの検索](https://intl.cloud.tencent.com/document/product/436/13325)のコンソールガイドドキュメントをご参照ください。

### REST APIの使用

REST APIを直接使用してオブジェクトキーリストアップリクエストを送信できます。 詳細については、[GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614)のAPIドキュメントをご参照ください。

### SDKの使用

SDKのオブジェクトリスト照会メソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37676)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31518)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30594)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31526)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37685)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546)
- [ミニプログラムSDK](https://intl.cloud.tencent.com/document/product/436/32457)
