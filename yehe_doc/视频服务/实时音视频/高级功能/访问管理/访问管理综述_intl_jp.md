>!ここでは主に**Tencent Real-Time CommunicationTRTC **のCloud Access Management（CAM）機能関連コンテンツについて紹介します。他製品のCAM関連コンテンツについては、[CAMサポート製品]をご参照ください。(https://intl.cloud.tencent.com/document/product/598/10588)。

[CAM）](https://intl.cloud.tencent.com/document/product/598)（Cloud Access Management，**CAM**）は、Tencent Cloudが提供するWebサービスであり、主にお客様がTencent Cloudアカウントのリソースへのアクセス権限を安全に管理するのに役立ちます。CAMを使用すると、ユーザー（グループ）を作成、管理、および廃棄でき、ID管理とポリシー管理を介して、Tencent Cloudリソースへのアクセスと使用が許可されるユーザーを制御できます。

TRTCは  **CAM**に接続済みであり、開発者は自身の必要に応じてサブアカウントに適切な TRTCアクセス権限を割り当てることができます。

## はじめに

TRTC CAMを使用する前に、 CAM と TRTC の基本コンセプトについて理解する必要があります。関連する主なコンセプトは次のとおりです。

- CAM 関連：[ユーザー](https://intl.cloud.tencent.com/document/product/598/32633)、[ポリシー](https://intl.cloud.tencent.com/document/product/598/10601) 
- TRTC 関連：[アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)、[SDKAppID](https://intl.cloud.tencent.com/document/product/647/37714)

## 適用ケース

### Tencent Cloudクラウドサービスのディメンションに対する権限隔離
ある企業内にTencent Cloudを使用する部門が複数存在し、その中の A部門がTRTCへの接続のみを担当する場合。A 部門のスタッフはTRTCにアクセスする権限を持っている必要がありますが、 他のTencent Cloud製品にアクセスする権限を持つことはできません。この企業はメインアカウントを介してA 部門のためにサブアカウントを作成し、このサブアカウントに TRTC 関連権限のみを付与し、その後、このサブアカウントをA 部門が使用するよう提供します。

### TRTC アプリケーションのディメンションに対する権限隔離
ある企業内の複数業務においてTRTCを使用する場合、相互間の隔離を行う必要があります。隔離にはリソースの隔離と権限の隔離という2つの面があり、前者はTRTC アプリケーションシステムによって提供され、後者はTRTC CAMによって実現されます。この企業は業務ごとにサブアカウントを作成し、関連のTRTC アプリケーション権限を付与し、それぞれの業務と関連のあるアプリケーションにしかアクセスできないようにします。

### TRTC 操作のディメンションに対する権限隔離
ある企業の1つの業務でTRTCを使用する場合、その業務の製品オペレーターは稼働統計データを取得するため、TRTC コンソールにアクセスする必要がありますが、誤操作によって業務に影響を及ぼすことを回避するため、機密性の高い操作（Relayed Pushの変更、クラウドレコーディングのコンフィグレーションなど）を行うことを許可されていません。この場合は、まずTRTCコンソールのログインと稼働統計関連APIにアクセスする権限を持つカスタマイズポリシーを作成し、その後、サブアカウントを作成し、上述のポリシーとのバインディングを行い、このサブアカウントを製品オペレーターに提供します。

## 権限の粒度
CAMのコア機能は次のように表現することができます：**あるアカウントがあるリソースに対して実施する何らかの操作を許可または禁止します**。TRTC CAMは[リソースレベルの承認](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B)をサポートし、リソースの粒度は [TRTC アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)、操作の粒度は [TencentCloud API](https://intl.cloud.tencent.com/product/api)であり、[サーバー API](https://intl.cloud.tencent.com/document/product/647/34260) とTRTC コンソールへのアクセス時に使用する可能性のあるAPIを含みます。



## 能力の制限
- TRTC CAMのリソース粒度は [アプリケーション](https://intl.cloud.tencent.com/document/product/647/37714)であり、より細かい粒度のリソース（アプリケーション情報、コンフィグレーション情報など）に対する承認をサポートしていません。
- TRTC CAMはプロジェクトをサポートしていませんので、 [タグ](https://intl.cloud.tencent.com/document/product/651/13335) を介してクラウドサービスリソースを管理することを推奨します。
