Content Delivery Network（CDN）を使用してCloud Object Storage（COS）のアクセラレーションを行うことで、バケット内のコンテンツを広範囲にダウンロード、配信することができます。特に、同一のコンテンツを繰り返しダウンロードするユースケースに適しています。back-to-origin認証機能を使用すると、CDNを使用したプライベート読み取りバケット内のコンテンツのアクセラレーションを実現できます。CDN認証機能を使用すると、コンテンツを正当なユーザーにのみダウンロード可能とすることができ、ダウンロードを開放することに伴うデータセキュリティおよびトラフィックコストなどの問題を防ぐことができます。


>?CDNアクセラレーションドメイン名を有効にした場合、CDNアクセラレーションドメイン名を使用してデータのダウンロードやアクセスを行うと、CDN back-to-originラフィックとCDNトラフィックが発生します。詳しくは、[COSをCDNオリジンサーバーとした場合発生するトラフィック](https://intl.cloud.tencent.com/document/product/436/33776)をご参照ください。


## Content Delivery Network

#### CDNの定義

CDNは既存のInternet上に追加された新しいネットワークアーキテクチャのレイヤーであり、世界各国に分布する高性能なアクセラレーションノードで構成されます。これらの高性能なサービスノードは一定のキャッシュポリシーに従ってお客様の業務コンテンツを保存しており、お客様のユーザーがある業務コンテンツをリクエストすると、リクエストがユーザーから最も近いサービスノードにスケジューリングされ、サービスノードから直接迅速にレスポンスすることで、ユーザーのアクセス遅延を効果的に低減し、可用性を向上させます。

CDNはキャッシュおよびback-to-origin行為を行います。すなわち、ユーザーがあるURLにアクセスしたとき、エッジノードに解決されてもレスポンスを必要とするキャッシュコンテンツにヒットしなかった場合、またはキャッシュが期限切れの場合は、オリジンサーバーに戻ってレスポンスを必要とするコンテンツを取得するものです。

#### 適用ケース

- レスポンス遅延およびダウンロード速度に対する要件が比較的厳しいケース。
- 地域、国、大陸を越えて数GBから数TBのデータを転送する必要があるケース。
- 同一のコンテンツを集中的に繰り返しダウンロードする必要があるケース。

#### セキュリティのタイプ

- back-to-origin認証：ユーザーのリクエストしたデータがエッジノードでキャッシュにヒットしなかった場合、CDNはback-to-originを行ってデータ内容を取得する必要があります。COSをオリジンサーバーとして使用し、back-to-origin認証を有効にすると、CDNエッジノードは特殊なサービスIDを使用してCOSオリジンサーバーにアクセスし、プライベートアクセスバケット内のデータの取得とキャッシュを実現することができます。
 - CDNサービス権限承認：CDNエッジノードはCDNサービス権限承認を追加することにより、特殊なサービスIDを使用してCOSオリジンサーバーにアクセスすることができるようになります。CDNサービス権限承認を追加してからでなければ、back-to-origin認証は有効化できません。
- CDN認証設定：ユーザーがエッジノードにアクセスしてキャッシュデータを取得する際、エッジノードは認証設定ルールに基づいて、URLアクセスにおけるID認証フィールドを検証することで、権限のないアクセスを防止し、リンク不正アクセス防止を実現し、エッジノードのキャッシュデータの安全性と信頼性を高めます。

## COSのアクセスノード

#### アクセスノードの定義

アクセスノードとはユーザーがバケットを作成する際、バケットのリージョンおよび名称に基づいて、システムが自動的にバケットに割り当てるアクセスドメイン名であり、このドメイン名によってバケット内のデータにアクセスすることができます。

静的ウェブサイト機能を有効にすると、静的ウェブサイトのアクセスノードを1つ追加で取得でき、それはデフォルトのアクセスノードとは性質の異なる、特殊な設定のレスポンス内容を表示するために用いられます。

#### アクセスノード

- アクセスノード：ユーザーがバケットを作成すると、COSはバケットに対し自動的に1つのXMLアクセスノードを割り当てます。 このアクセスノードの形式は&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.comであり、RESTful APIによるアクセスに適用されます。ユーザーはアクセスドメイン名によって、また[APIドキュメント](https://intl.cloud.tencent.com/document/product/436/7751)の実行ルールを確認してバケットの設定を行ったり、オブジェクトのアップロード、ダウンロード操作を行ったりすることができます。
- 静的ウェブサイトノード：コンソール上のバケット基本設定画面で静的ウェブサイトのホスティング機能を有効にすることができ、有効にすると1つのアクセスノードが提供されます。アクセスノードの形式は&lt;BucketName-APPID>.cos-website.&lt;Region>.myqcloud.comです。静的ウェブサイトは特殊なインデックスページ（IndexPage）、エラーページ（ErrorPage）およびリダイレクトなどをサポートしており、サポートはオブジェクトのダウンロード系の操作のみとなります。ユーザーは静的ウェブサイトのドメイン名によってコンテンツを取得できます。

#### アクセス権限

- パブリック読み取り：バケットをパブリック読み取りに設定すると、バケットのアクセスドメイン名によって誰でもそのバケットにアクセスすることができます。ユーザーがパブリック読み取りバケットをオリジンサーバーとしてback-to-originを行う場合は、CDNアクセラレーションを直接有効化でき、CDN認証およびback-to-origin認証を使用する必要はありません。
- プライベート読み取り：バケットをプライベート読み取りに設定すると、ユーザーはアクセスポリシーを作成することによってアクセス者を管理でき、これにはCDNサービス権限承認の管理なども含まれます。ユーザーがプライベート読み取りバケットをオリジンサーバーとしてback-to-originを行う場合、back-to-origin認証を有効にしていてもCDN認証を有効にしていなければ、権限範囲外の人がCDNによって直接バケットにアクセスすることが可能になってしまいます。このため、プライベート読み取りバケットについては、**CDN認証とback-to-origin認証を同時に有効にすることでデータの安全性を保障するよう強く推奨します**。

## CDNアクセラレーションを使用したCOSアクセス

ユーザーはカスタムCDNアクセラレーションドメイン名によって、COSへのアクセラレーションアクセスを行うことができます。ユーザーは初めにICP登録済みのカスタムドメイン名をご自身で準備し、オリジンサーバーをCOSバケットに指定することで、カスタムCDNアクセラレーションドメイン名を使用したバケット内のオブジェクトに対するアクセラレーションアクセスを実現できます。

>?Tencent Cloud CDNのアクセラレーションドメイン名はデフォルトではIPアドレスを提供しません。ドメイン名の解決状況を確認したい場合は、digコマンドを使用して照会することができます。

#### パブリック読み取りバケット

バケットをパブリックアクセス許可に設定すると、CDN back-to-originをCOSアクセスノードに設定した場合、back-to-origin認証を有効にしなくても、CDNエッジノードがバケット内のオブジェクトデータを取得してキャッシュすることが可能です。

CDNコンソールで[認証設定](https://intl.cloud.tencent.com/document/product/228/35237)を有効にして、バケット内のデータを**限定的に**保護することも引き続き可能です。CDNのこの機能を有効にしているかどうかにかかわらず、バケットのアクセスドメイン名を知っているユーザーはバケット内のすべてのオブジェクトにアクセス可能なためです。CDN認証設定の違いによる、ドメイン名のパブリック読み取りバケットに対するアクセス機能の違いについては次の表をご参照ください。

| CDN認証設定 | CDNアクセラレーションドメイン名アクセス | COSドメイン名アクセス | 一般的なケース                                        |
| ------------ | ---------------- | ------------ | ----------------------------------------------- |
| 無効（デフォルト） | アクセス可           | アクセス可       | 全サーバーでパブリックアクセス許可、CDNとオリジンサーバーどちらからのアクセスも可       |
| 有効         | URLを使用した認証が必要  | アクセス可       | CDNアクセスに対してはリンク不正アクセス防止が有効、ただしオリジンサーバーアクセスは保護されないため非推奨 |

#### プライベート読み取りバケット

バケットがデフォルトのプライベート読み取りである場合、CDN back-to-originをCOSアクセスノードに設定すると、CDNエッジノードは**データの取得とキャッシュが一切できなくなります**。このため、CDNサービスIDをバケットアクセスポリシー（Bucket Policy）に追加するとともに、そのIDによる次の操作の実行を許可する必要があります。

- GET Object：オブジェクトのダウンロード
- HEAD Object：オブジェクトメタデータの照会
- OPTIONS Object：クロスドメイン設定のプリフライトリクエスト

[CDNコンソール](https://console.cloud.tencent.com/cdn)と[COSコンソール](https://console.cloud.tencent.com/cos5)はいずれもワンクリックでの権限承認機能をご提供しています。**CDNサービス権限承認の追加**をクリックすれば完了です。この操作の完了後、**back-to-origin認証**オプションを有効にする必要があります。これでCDNエッジがこのサービスIDを使用してCOS内のデータにアクセスできるようになります。

>!
>- バケットがプライベート読み取りに設定されている場合は、必ず権限承認を追加し、back-to-origin認証を有効にしてください。これを行わなければCOSはアクセスを拒否します。
>- CDNエッジは各ルートアカウントにつき、1つのサービスアカウントを生成します。このため、アカウントの権限承認はアクセラレーションドメイン名が所属するルートアカウントに対してのみ有効であり、異なるアカウント間でバインドしたアクセラレーションドメイン名はアクセスが拒否されます。

CDNサービス権限承認を追加し、back-to-origin認証を有効にすると、CDNエッジノードはデータを直接取得およびキャッシュできるようになります。このため、プライベートデータの保護が必要な場合は、[認証設定](https://intl.cloud.tencent.com/document/product/228/35237)を有効にして、バケット内のデータを保護することを強く推奨します。CDN認証設定の違いによる、ドメイン名のプライベート読み取りバケットに対するアクセス機能の違いについては次の表をご覧ください。

| CDN認証設定 | CDNアクセラレーションドメイン名アクセス | COSドメイン名アクセス    | 一般的なケース                            |
| ------------ | ---------------- | --------------- | ----------------------------------- |
| 無効（デフォルト） | アクセス可           | COSを使用した認証が必要 | CDNドメイン名に直接アクセス可能、オリジンサーバーデータ保護   |
| 有効         | URLを使用した認証が必要  | COSを使用した認証が必要 | 全リンクのアクセスを保護、CDN認証リンク不正アクセス防止をサポート |

