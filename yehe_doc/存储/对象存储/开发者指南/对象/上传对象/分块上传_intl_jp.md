## 概要

**マルチパートアップロード**では、オブジェクト全体を複数のパートに分割してから、これらのパートをCloud Object Storage (COS)にアップロードすることが可能です。アップロードの際、これらのパートには連続した順序に従って番号が付与され、各パートは単独でアップロードすることも、任意の順序でアップロードすることもできます。最終的にCOSはパートの番号に基づいてそのオブジェクトを再度組み立てます。いずれかのパートが転送に失敗した場合も、そのパートを再転送できるため、他のパートおよびコンテンツの完全性に影響を与えません。一般的に、不安定なネットワーク環境では、単一のオブジェクトが20MBを超えるとマルチパートアップロードを優先的に検討できます。高帯域幅環境では、100MBを超えるオブジェクトについてマルチパートアップロードを実施することができます。

**マルチパートアップロード**では、大きなオブジェクトを最大で10000パートにまで分割することができます。分割するパートのサイズは一般的に1MB～5GBであり、最後の1パートは1MB未満とすることが可能です。

>? シンプルアップロード方式では最大5GBまでのファイルのアップロードのみサポートしていますが、マルチパートアップロード方式では5GBを超えるファイルのアップロードが可能です。
>

## ユースケース
マルチパートアップロードは不安定なネットワーク、または高帯域幅環境下で大きなオブジェクトをアップロードする場合に適しています。

マルチパートアップロードには次のようなメリットがあります。

- 不安定なネットワーク環境では、パートを小さくすることで、ネットワークエラーによる中断の影響を低減し、オブジェクトのアップロード継続を実現できます。
- 高帯域幅環境下では、オブジェクトのパートのアップロードを同時実行することで帯域幅ネットワークを有効活用できます。順不同のアップロードが最終的なオブジェクトの組み立てに影響することもありません。
- マルチパートアップロードを使用することで、単一の大きなオブジェクトのアップロードをいつでも一時停止し、再開することができます。終了操作を行った場合を除き、アップロードが未完了のオブジェクトは、いつでもアップロードを再開できます。
- マルチパートアップロードはオブジェクト全体のサイズがわからない状態でオブジェクトをアップロードする場合にも適しています。先にアップロードを開始し、後でオブジェクトを組み立てることで完全なサイズを取得できます。


## 利用方法

### REST APIの使用

REST APIを直接使用してマルチパートアップロードリクエストを送信できます。詳細については、次のAPIドキュメントをご参照ください。

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### SDKの使用

SDKのパート操作メソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

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
