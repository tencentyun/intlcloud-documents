>!ここでは主に**Tencent Real-Time Communication(TRTC)**のCloud Access Management(CAM)機能関連コンテンツについて紹介します。他製品のCAM関連コンテンツについては、[CAMサポート製品](https://intl.cloud.tencent.com/document/product/598/10588)をご参照ください。

[CAM](https://intl.cloud.tencent.com/document/product/598)（Cloud Access Management、**CAM**）は、Tencent Cloudが提供するWebサービスであり、主にお客様がTencent Cloudアカウントのリソースへのアクセス権限を安全に管理するのに役立ちます。CAMを使用すると、ユーザー（グループ）を作成、管理、および廃棄でき、ID管理とポリシー管理を介して、Tencent Cloudリソースへのアクセスと使用が許可されるユーザーを制御できます。

TRTCは**CAM**に接続済みであり、開発者は自身の必要に応じてサブアカウントに適切な TRTCアクセス権限を割り当てることができます。 

## はじめに

TRTC CAMを使用する前に、 CAMとTRTCの基本コンセプトについて理解する必要があります。関連する主なコンセプトは次のとおりです。

- CAM関連：[ユーザー](https://intl.cloud.tencent.com/document/product/598/32633)、[ポリシー](https://intl.cloud.tencent.com/document/product/598/10601) 
- TRTC関連：[アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)、[SDKAppID](https://intl.cloud.tencent.com/document/product/647/37714)

## 適用ケース

### Tencent Cloudクラウドサービスのディメンションに対する権限隔離
ある企業内にTencent Cloudを使用する部門が複数存在し、その中のA部門がTRTCへの接続のみを担当する場合。A部門のスタッフはTRTCにアクセスする権限を持っている必要がありますが、 他のTencent Cloud製品にアクセスする権限を持つことはできません。この企業はルートアカウントを介してA部門のためにサブアカウントを作成し、このサブアカウントにTRTC関連権限のみを付与し、その後、このサブアカウントをA部門が使用するよう提供します。

### TRTCアプリケーションのディメンションに対する権限隔離
ある企業内の複数業務においてTRTCを使用する場合、相互間の隔離を行う必要があります。隔離にはリソースの隔離と権限の隔離という2つの面があり、前者はTRTCアプリケーションシステムによって提供され、後者はTRTC CAMによって実現されます。この企業は業務ごとにサブアカウントを作成し、関連のTRTCアプリケーション権限を付与し、それぞれの業務と関連のあるアプリケーションにしかアクセスできないようにします。

### TRTC操作のディメンションに対する権限隔離
ある企業の1つの業務でTRTCを使用する場合、その業務の製品オペレーターは稼働統計データを取得するため、TRTCコンソールにアクセスする必要がありますが、誤操作によって業務に影響を及ぼすことを回避するため、機密性の高い操作（Relayed Pushの変更、クラウドレコーディングのコンフィグレーションなど）を行うことを許可されていません。この場合は、まずTRTCコンソールのログインと稼働統計関連APIにアクセスする権限を持つカスタムポリシーを作成し、その後、サブアカウントを作成し、上述のポリシーとのバインディングを行い、このサブアカウントを製品オペレーターに提供します。

## 権限の粒度
CAMのコア機能は、**特定のアカウントが特定のリソースに対して何らかの操作を実行することを許可または禁止する**と表すことができます。TRTC CAMでは、[リソースレベルの承認](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B)をサポートし、リソースの粒度は[TRTCアプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)です。操作の粒度は[Tencent Cloud API](https://intl.cloud.tencent.com/product/api)であり、[サーバーAPI](https://intl.cloud.tencent.com/document/product/647/34260) とTRTCコンソールにアクセスするときに使用する可能性のあるAPIを含みます。詳しい説明は、[権限付与可能なリソースと操作](https://intl.cloud.tencent.com/document/product/647/39549)をご参照ください。



## 機能の制限
- TRTC CAMのリソース粒度は [アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)であり、より細かい粒度のリソース（アプリケーション情報、コンフィグレーション情報など）に対する承認をサポートしていません。
- TRTC CAMではプロジェクトをサポートしていません。[タグ](https://intl.cloud.tencent.com/document/product/651/13335)を用いて、クラウドサービスのリソースを管理することを推奨します。
