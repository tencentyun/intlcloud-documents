Player SDKは2022年9月19日にモバイル端末向けのバージョン10.7をリリースします。このバージョンではインターフェース`startPlay`の名称が変更になります。

`startPlay`インターフェースはSDKの再生機能の設定時に使用するもので、再生の開始を表します。具体的な変更は次のとおりです。

- VOD再生インターフェース`TXVodPlayer`の再生開始インターフェース名が`startPlay`から`startVodPlay`に変更されます。詳細については、[API-iOS-VOD再生](https://www.tencentcloud.com/document/product/266/47844)、[API-Android-VOD再生](https://www.tencentcloud.com/document/product/266/47851)、[API-Flutter-VOD再生](https://www.tencentcloud.com/document/product/266/42099)をご参照ください。
- CSS再生インターフェース`TXLivePlayer`の再生開始インターフェース名が`startPlay`から`startLivePlay`*に変更されます。*詳細については、[API-iOS-CSS再生](https://www.tencentcloud.com/document/product/266/47841#.E6.92.AD.E6.94.BE.E5.9F.BA.E7.A1.80.E6.8E.A5.E5.8F.A3)、[API-Android-CSS再生](https://www.tencentcloud.com/document/product/266/47850#.E6.92.AD.E6.94.BE.E5.9F.BA.E7.A1.80.E6.8E.A5.E5.8F.A3)をご参照ください。

>?
>- モバイル端末向け10.7より低いバージョンのSDKでこのインターフェースを使用している場合は、今回の変更による影響はありません。
>- モバイル端末向け10.7以上のバージョンのSDKでこのインターフェースを使用している場合は、今回の変更にご注意ください。

ユーザーの皆様には、Tencent Cloud View Cube製品に信頼をお寄せいただき、また、日頃よりご愛顧を賜り厚く御礼申し上げます。ご不明な点がございましたら、お気軽に[お問い合わせ](https://intl.cloud.tencent.com/contact-us)ください。

2022-09-19

Tencent Cloud
