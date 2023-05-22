
### バケット（Bucket）

バケット（Bucket）とはオブジェクトのキャリアであり、オブジェクトを入れておくための「容器」と理解することができます。ユーザーはTencent Cloudコンソール、API、SDKなどの複数の方式によってバケットを管理し、属性を設定することができます。例えば、バケットを静的ウェブサイトのホスティング用に設定することや、バケットのアクセス権限設定などを行うことができます。

関連ドキュメントについては[バケット概要](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください。


### オブジェクト（Object）

オブジェクト（Object）とはCOSの基本ユニットです。オブジェクトはバケットに保存されます（写真をアルバムに保存するようなイメージです）。ユーザーはTencent Cloudコンソール、API、SDKなどの複数の方式によってオブジェクトを管理できます。API、SDKの例では、オブジェクトの命名フォーマットは&lt;ObjectKey>となります。

関連ドキュメントについては[オブジェクト概要](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください。


### APPID

APPIDはTencent Cloudアカウントの申請に成功すると取得できるアカウントであり、システムによって自動的に割り当てられ、固有性と唯一性を有します。[アカウント情報](https://console.cloud.tencent.com/developer)で確認できます。Tencent CloudアカウントのAPPIDは、アカウントIDとの間に唯一の対応関係を有するアプリケーションIDです。

APPIDはバケット名によく使用されます。完全なバケット名はユーザーがカスタマイズする文字列とAPPIDで構成され、間にハイフン「-」が入ります。例えば、`examplebucket-1250000000`では、1250000000がAPPIDです。

### UID

このほかに、APPIDも一時キーの発行、バケットポリシーの指定またはCloud Access Management（CAM）におけるポリシー設定時のリソース（resource）範囲指定に用いられます。この場合、APPIDは通常はUIDと表現され、両者の値は同じです。

関連ドキュメントについては、[バケット概要](https://intl.cloud.tencent.com/document/product/436/13312)、[アクセスポリシーの言語概要](https://intl.cloud.tencent.com/document/product/436/18023)、[リソース記述法](https://intl.cloud.tencent.com/document/product/598/10606)をご参照ください。


### UIN

アカウントIDを指し、APPIDとの間に唯一の対応関係を有し、かつ固有性と唯一性を有します。[アカウント情報](https://console.cloud.tencent.com/developer)で確認できます。COS製品においては、一時キーの発行、バケットポリシーの指定またはCloud Access Management（CAM）におけるポリシー設定時のリソース（resource）範囲指定に用いられます。この場合の用法はUIDと似ていますが、プレフィックスが区別されていることに注意してください。

関連ドキュメントについては、[アクセスポリシーの言語概要](https://intl.cloud.tencent.com/document/product/436/18023)、[リソース記述法](https://intl.cloud.tencent.com/document/product/598/10606)をご参照ください。

### ACL

アクセス制御リスト（ACL）はリソースに基づくアクセス管理オプションの1つであり、アクセス権限行為の説明に用いられます。
COSでは、バケットとオブジェクトへのアクセスの管理に用いられます。ACLを使用することで、他のルートアカウント、サブアカウント、ユーザーグループに対し、基本的な読み取り/書き込み権限を付与することができます。

関連ドキュメントについては、[アクセス制御の基本概念](https://intl.cloud.tencent.com/document/product/436/30581)、[ACLの概要](https://intl.cloud.tencent.com/document/product/436/30583)をご参照ください。

### CORS

Cross-Origin Resource Sharingとは、リクエストを送信するリソースが存在するオリジンが、そのリクエストの指向するリソースの存在するオリジンと異なる場合のHTTPリクエストを指します。


### SecretKey

SecretIdとSecretKeyはTencent Cloud APIキーと総称されます。ユーザーがTencent Cloud APIにアクセスしてID認証を行う際に必要なセキュリティ証明書であり、[APIキー管理](https://console.cloud.tencent.com/cam/capi)で取得することができます。SecretKeyは署名文字列の暗号化およびサーバー側の署名文字列検証に用いられるキーです。1つのAPPIDにつき、複数のTencent Cloud APIキーを作成することができます。


### SecretId

SecretIdとSecretKeyはTencent Cloud APIキーと総称されます。ユーザーがTencent Cloud APIにアクセスしてID認証を行う際に必要なセキュリティ証明書であり、[APIキー管理](https://console.cloud.tencent.com/cam/capi)で取得することができます。SecretIdはAPIを呼び出したIDを識別するために用いられます。1つのAPPIDにつき、複数のTencent Cloud APIキーを作成することができます。



### policy

ポリシー（policy）はいくつかの要素で構成され、権限承認の具体的な情報の説明に用いられます。詳細については、[アクセスポリシーの言語概要](https://intl.cloud.tencent.com/document/product/436/18023)をご参照ください。


### パブリックネットワークダウンストリームトラフィック

インターネットを通じてデータをCOSからクライアントに転送する際に発生するトラフィックを指します。 ユーザーがオブジェクトリンクからオブジェクトを直接ダウンロードした場合、または静的ウェブサイトのオリジンサーバーを介してオブジェクトを閲覧した場合に発生するトラフィックが含まれます。

### CDN back-to-originトラフィック
データをCOSからTencent Cloud Content Delivery Network（CDN）のエッジノードに転送する際に発生するトラフィックを指します。


### デフォルトドメイン名
COSオリジンサーバーのドメイン名であり、バケットの作成時に、システムがバケット名およびリージョンに基づいて自動的に生成するもので、デフォルトのアクセラレーションドメイン名と区別する必要があります。詳細については、[ドメイン名管理の概要](https://intl.cloud.tencent.com/document/product/436/18424)をご参照ください。


### デフォルトCDNアクセラレーションドメイン名

CDNアクセラレーションノードによってアクセラレーションされるドメイン名であり、システムによってデフォルトで生成されます。有効にするかどうかはユーザーが選択できます。詳細については、[ドメイン名管理の概要](https://intl.cloud.tencent.com/document/product/436/18424)をご参照ください。


### カスタムCDNアクセラレーションドメイン名
ユーザーはバケットを使用する際、登録済みのカスタムドメイン名をTencent Cloudの国内CDNアクセラレーションプラットフォームにバインドすることで、カスタムドメイン名によってバケット内のオブジェクトにアクセスすることが可能になります。詳細については、[ドメイン名管理の概要](https://intl.cloud.tencent.com/document/product/436/18424)をご参照ください。


### カスタムオリジンサーバードメイン名
ユーザーは登録済みのカスタムドメイン名を現在のバケットにバインドすることで、カスタムドメイン名によってバケット内のオブジェクトにアクセスすることが可能になります。詳細については、[ドメイン名管理の概要](https://intl.cloud.tencent.com/document/product/436/18424)をご参照ください。


### データ取得
低頻度ストレージおよびアーカイブストレージタイプはコールドデータストレージタイプです。低頻度データは、読み取りまたはダウンロードを行う場合、バックエンドが先にデータを取得してからでなければ読み取りまたはダウンロードを行うことができません。アーカイブデータは読み取りおよびダウンロードができず、この場合、データの取得は解凍（アーカイブデータを標準データに復元するプロセス）とも呼ばれます。


### マルチAZ

マルチAZ（Multiple Availability Zones）とは、Tencent Cloud COSがリリースしたマルチAZストレージアーキテクチャです。お客様のデータを都市の複数の異なるデータセンターに分散して保存します。あるデータセンターに自然災害、停電などの極端な状況による全面的な障害が発生した場合でも、マルチAZによって安定した信頼性の高いストレージサービスを引き続き提供することができます。

関連ドキュメントについては、[マルチAZの特徴の概要](https://intl.cloud.tencent.com/document/product/436/35208)をご参照ください。


### Region


リージョンとは、Tencent Cloudのホスティングデータセンターが分布する地域のことです。COSのデータはこれらのリージョンのバケット内に保存されます。

関連ドキュメントについては、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください。



