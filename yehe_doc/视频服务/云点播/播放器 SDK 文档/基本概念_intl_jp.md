このドキュメントでは、Tencent Cloud View Cube Player（以下、「Player」と略記）のオンデマンド再生シナリオに関連する基本概念について、プレーヤーのビデオオンデマンド機能の速やかな理解および使用のために説明します。

[](id:basicConception)
## 基本概念
プレーヤーはVODプラットフォームでSuper PlayerとSuper Player Adapterの二つの方式によるオンデマンドサービスへの導入をサポートしています。

### Super Player
Super Playerは独立した完全なビデオプレーヤーで、ビデオの暗号化、サムネイルプレビュー、解像度の切り替えなどの全面的なビデオ再生機能を備えています。このプレーヤーは完全なUIと体験Demoがあると同時に、Tencent VOD業務と深く融合し、オンデマンドファイル識別「FileID」を使用してVODリソースを再生できます。また、Super PlayerはVOD全リンク動画再生品質データサービスも提供しています。Super Playerの速やかな導入について、[Super Playerチュートリアル](https://intl.cloud.tencent.com/document/product/266/38098)をご参照ください。


### Super Player Adapter
Super Player Adapterは、サードパーティープレーヤーとTencent VODリソースを接続するためのプレーヤープラグインであり、動画再生や動画暗号化などの機能を備えています。Super Player Adapterは、ユーザーのサードパーティープレーヤーに導入されると、オンデマンドファイル識別「FileID」を使用してVODリソースを再生できます。Super Player Adapterの速やかな導入について、各端末向けの導入ドキュメントをご参照ください。


[](id:choosePlayer)
## プレーヤーの選択方法
ユーザー導入の難易度を下げ、ユーザー自身の業務シーンに合わせるよう、VODユーザーがプレーヤーサービスを導入するとき、適切なプレーヤータイプを選択することをお勧めします。
![](https://qcloudimg.tencent-cloud.cn/raw/f793f98980f8f0adb38ee4292ed10d67.png)

- **Super Player**：プレーヤーが導入されていないが、オンデマンドのビデオ再生機能を速やかに構築する必要があるユーザーに適しています。プレーヤーは包括的な機能があり、導入が便利です。VODでは、Super Player導入に関する詳細なチュートリアルをユーザーに提供します。詳細については、[Super Playerチュートリアル](https://intl.cloud.tencent.com/document/product/266/38098)をご参照ください。
- **Super Player Adapter**：独自開発/サードパーティプレーヤーを使用してVODリソースを再生するユーザーに適しています。VODはお客様がスムーズに導入してVODプラットフォームリソースを使用するためのSuper Player Adapterを提供しています。

各タイプのプレーヤーをサポートするプラットフォーム端末は次のとおりです。

| プレーヤー種類     | Super Player | Super Player Adapter |
| --------- | ----- | ------------- |
| Web端末      | &#10003     | &#10003             |
| iOS端末      | &#10003     | &#10003             |
| Android端末 | &#10003     | &#10003             |
| Flutter端末  | &#10003     | \-            |
| UI        | &#10003     | \-            |
| Demo      | &#10003     | \-            |


