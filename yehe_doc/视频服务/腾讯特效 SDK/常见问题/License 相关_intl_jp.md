License使用の過程で、次のような疑問が生じる場合があるかもしれません。その場合はこちらの回答を参考にしてください。

[](id:q1)

### License、License KeyとTencent Effect SDKとの関係はなんですか。

Tencent Effect SDKを合法的に使用するには、Tencentに許可されたLicenseを取得する必要があります。Licenseは、SDKを試用または購入する前に取得する必要のある許可です。Licenseの許可なしに製品を使用すると、権利侵害と見なされます。テストLicenseと公式Licenseの2種類のLicenseを取得できます。

SDKは、サービス全体に固有のソフトウェアパッケージ、ソフトウェアフレームワーク、OSなどを使用してアプリケーションソフトウェアを構築するための開発ツールのセットです。TencentからSDKを使用するためのLicenseを取得すると、License KeyとLicense URL情報のペアを取得します。Tencent Effect機能を有効にするには、SDKの対応する位置に有効な認証License KeyとLicense URLを入力する必要があります。

[](id:q2)

### Tencent Effectの正式版Licenseを取得するにはどうすればよいですか。

業務の中でTencent Effect SDK機能を使用したい場合は、課金概要を参照し、ニーズに合ったSDKパッケージを選択して購入することができます。該当のSDKパッケージを購入するとLicenseのロック解除権限を取得でき、パッケージの購入後にTencent Cloud View Cubeコンソールでバインドすることで、対応する機能を使用できます。具体的な操作については、[正式版Licenseの購入](https://www.tencentcloud.com/document/product/1143/50266#.E8.B4.AD.E4.B9.B0.E6.AD.A3.E5.BC.8F.E7.89.88-license)をご参照ください。

[](id:q3)

### Licenseの有効期限はいつまでですか。期限切れとなった後はどのようにLicenseを更新しますか。

- **テスト版License**の有効期間は、審査で承認された後、Licenseが発行された日から数えて1か月間（28日間）となります。例えば、2022年1月1日にテスト版Licenseを申請し、2022年1月2日に承認されて自動的にLicenseが発行された場合、テスト版Licenseは2022年1月31日の00:00:00に期限切れとなります。
- **正式版License**の有効期間は、Licenseをバインドした日から数えて1年間（365日間）となります。例えば、2022年1月1日に正式版Licenseをバインドした場合、正式版Licenseは2023年1月2日の00:00:00に期限切れとなります。
- 正式版Licenseが期限切れとなった後は、再度Licenseを購入して更新を行う必要があります。正式版Licenseの更新ガイドについては、[正式Licenseの更新](https://www.tencentcloud.com/document/product/1143/50266#.E6.9B.B4.E6.96.B0.E6.AD.A3.E5.BC.8F.E7.89.88-license-.E6.9C.89.E6.95.88.E6.9C.9F)をご参照ください。

[](id:q4)

### 発行後のLicenseはパッケージ名を変更できますか。

テスト版Licenseの場合は、AndroidのPackage NameとiOSのBundle IDを変更することができます。

正式版Licenseは一度追加してバインドすると、Package NameとBundle IDを変更することはできません。

[](id:q5)

### Licenseのサポートするパッケージ名の数はいくつですか。権限承認できる台数はいくつですか。

1つのLicenseを追加するごとに、Bundle IDとPackage Nameという2つの異なるパッケージ名をサポートします。アカウント全体で追加できるLicenseの数に制限はありません。現時点ではLicenseが権限承認できる端末の台数にも制限はありません。

[](id:q6)

### Tencent Effect SDKのアップグレード・ダウングレードはどのようにすればよいですか。

Tencent Cloud SDKは全部で14のバージョンを提供しています。各バージョンの機能の違いについては、[課金概要](https://intl.cloud.tencent.com/document/product/1143/45371)をご参照ください。正式版Licenseが期限切れとなってから、よりシーンのニーズに合ったバージョンを購入して切り替えることができます。現在のLicenseが有効期間内の場合、SDKのアップグレード・ダウングレードはサポートしていません。

テスト版Licenseはパッケージの最上級バージョンであるS1 - 04の権限を統一して発行しており、SDKのすべての機能を試すことができます。 テスト期間終了前に、ユースケースにマッチした正式版SDKおよびLicenseに切り替えることができます。

### ルートアカウントからサブアカウントに対し権限承認を行いましたが、Tencent Effect関連の権限が見つからないのはなぜですか。
<img src="https://qcloudimg.tencent-cloud.cn/raw/281d3924082074812e3bcf3b33811685.png" style="zoom:50%;" />

vcubeを検索して、Tencent Effect関連の操作に対する権限を承認することができます。
- サブアカウントに対し、License照会の権限のみを提供する必要がある場合は、QcloudVCUBEReadOnlyAccessポリシーの権限を承認してください。
- サブアカウントに対し、すべてのLicense操作権限を提供する必要がある場合は、QcloudVCUBEFullAccessポリシーの権限を承認してください。

