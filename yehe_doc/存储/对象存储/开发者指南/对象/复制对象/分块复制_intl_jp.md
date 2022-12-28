## ユースケース

5GBを超えるオブジェクトをコピーしたい場合は、マルチパートコピーのメソッドを選択して実現する必要があります。マルチパートアップロードのAPIを使用して新しいオブジェクトを作成し、Upload Part - Copyの機能を使用して、x-cos-copy-sourceヘッダーを付けてソースオブジェクトを指定します。これには次のフローが含まれます。

1. マルチパートアップロードするオブジェクトを初期化します。
2. ソースオブジェクトのデータをコピーします。x-cos-copy-source-rangeヘッダーを指定できます。1回にコピーできるデータは最大5GBまでです。
3. マルチパートアップロードが完了します。

>?Tencent Cloud COSが提供するSDKを使用すると、マルチパートコピー機能を簡単に利用できます。

## 利用方法

### REST APIの使用

REST APIを直接使用してマルチパートコピーリクエストを送信できます。次のAPIドキュメントをご参照ください。

- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287)
- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742)
- [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740)

### SDKの使用

SDKのパートコピーメソッドを直接呼び出すことができます。下記の各言語のSDKドキュメントをご参照ください。


- [Android SDK](https://intl.cloud.tencent.com/document/product/436/37674#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [C SDK](https://www.tencentcloud.com/document/product/436/44872)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31522#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [.NET(C#) SDK](https://www.tencentcloud.com/document/product/436/40171)
- [Go SDK](https://www.tencentcloud.com/document/product/436/44064)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/37683#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31534#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [JavaScript SDK](https://intl.cloud.tencent.com/document/product/436/31538#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31710#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31542#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31546#.E5.A4.8D.E5.88.B6.E5.88.86.E5.9D.97)
- [Mini Program SDK](https://www.tencentcloud.com/document/product/436/43885)
