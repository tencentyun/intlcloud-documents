ファイルをCOS（Cloud Object Storage）に保存する際、先にオブジェクトを保存するためのバケットを作成する必要があります。バケットの作成は、コンソール、ツール、APIまたはSDK方式で行うことができます。

バケットを作成すると、そのバケットにオブジェクトをアップロードできるようになります。また、バケットに他の機能を設定することもできます。例えば、[静的ウェブサイトの設定](https://intl.cloud.tencent.com/document/product/436/14984)、[バケットタグの設定](https://intl.cloud.tencent.com/document/product/436/30928) 、[バケット暗号化の設定](https://intl.cloud.tencent.com/document/product/436/33455)などです。その他の設定ガイドについては、[コンソールの概要](https://intl.cloud.tencent.com/document/product/436/11365)をご参照ください。


## 制限事項

1. 同一のルートアカウント下に作成できるバケット数は最大200個までです。
2. バケットはいったん作成すると、バケット名および所属リージョンの変更はできません。
3. 同一のルートアカウントにおけるバケット名は固有であり、リネームもサポートしていません。
4. バケット名は小文字アルファベットおよび数字、すなわち[a-z，0-9]、ダッシュ「-」およびそれらの組み合わせのみサポートしています。バケット名の最大文字数は、**[リージョンの略称](https://intl.cloud.tencent.com/document/product/436/6224)**および**APPID**の文字数の影響により、組み合わせたリクエストドメイン名全体の文字数合計が最大60文字までとなります。例えば、リクエストドメイン名`123456789012345678901-1250000000.cos.ap-beijing.myqcloud.com`の場合は合計60文字です。
5. バケット名は「-」を先頭または末尾にすることはできません。


## 利用方法

### COSコンソールの使用

COSコンソールを使用してバケットを作成することができます。詳細については、[バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)のコンソールドキュメントをご参照ください。

### ツールの使用

COSBrowserツール、COSCMDツールなどを使用してバケットを作成することができます。詳細については、[ツールの概要](https://intl.cloud.tencent.com/document/product/436/6242)をご参照ください。

### REST APIの使用

REST APIを直接使用してバケット作成リクエストを送信できます。 詳細については、[PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738)のAPIドキュメントをご参照ください。

### SDKの使用

SDKのバケット作成メソッドを直接呼び出すことができます。詳細については、下記の各言語のSDKドキュメントをご参照ください。

- [Android SDK](https://intl.cloud.tencent.com/document/product/436/31463)
- [C SDK](https://intl.cloud.tencent.com/document/product/436/31464)
- [C++ SDK](https://intl.cloud.tencent.com/document/product/436/31465)
- [.NET SDK](https://intl.cloud.tencent.com/document/product/436/30595)
- [Go SDK](https://intl.cloud.tencent.com/document/product/436/31466)
- [iOS SDK](https://intl.cloud.tencent.com/document/product/436/31467)
- [Java SDK](https://intl.cloud.tencent.com/document/product/436/31468)
- [Node.js SDK](https://intl.cloud.tencent.com/document/product/436/31469)
- [PHP SDK](https://intl.cloud.tencent.com/document/product/436/31470)
- [Python SDK](https://intl.cloud.tencent.com/document/product/436/31471)
- [ミニプログラムSDK](https://intl.cloud.tencent.com/document/product/436/30609)

