### TencentOS Serverとは何ですか。
TencentOS Server（別名Tencent Linux、略称はTSまたはtlinux）はTencentがクラウドシナリオのために研究開発したLinux オペレーティングシステムです。特定の機能および性能を最適化し、CVMインスタンスのアプリケーションプログラムに高性能で安全かつ信頼性の高い運用環境を提供します。
TencentOS ServerにはTencentOSチームが研究開発したTencent OSカーネルが含まれ、クラウド環境の高度なカスタマイズを基に最新のLinuxイノベーションを市場に投入し、各種エンタープライズソフトウェアに抜群の性能、高いスケーラビリティと信頼性を提供します。TencentOS Serverは無料で使用でき、ユーザーは引き続きTencentOSチームによる更新メンテナンスとテクニカルサポートを受けることができます。

### TencentOS Serverにはどのような特徴がありますか。
TencentOS Server製品の特徴は次のとおりです。
- 高度にカスタマイズされ、箱から出してすぐに使用でき、複雑な設定が不要です。
- セキュリティコンプライアンス、ホットパッチをサポートし、ダウンタイムなしで修復します。
- 長期的なサポートを提供し、強力な運営サポートチームを擁し、完全なオープンソースです。
- クラウドシナリオ向けに設計され、完全に最適化された高性能なOSです。

### 他のLinux オペレーティングシステムに比べ、TencentOS Serverにはどのようなメリットがありますか。
CentosやUbuntuなどのリリース版と比較した場合のTencentOS Serverの主なメリットは次のとおりです。
- Tencentの10数年にわたる大量の内部業務の検証と研鑽の結晶です。
- 権威あるカーネルエキスパートチームがサポートします。
- 重要な性能の最適化とクラウドおよびコンテナシナリオ向けのカスタム特性を具備し、箱から出してすぐに使用できます。
- 強力な運営サポートチームを擁し、少額の費用で強力なビジネスサポートを受けられます。

### TencentOS Serverにはどのようなバージョンがありますか。
現在、次の2つのバージョンがあります。
- TencentOS Server 2 (TS2)：CentOS7の最新ユーザーステータスパッケージをベースにしています。
- TencentOS Server 3 (TS3)：RHEL8の最新ユーザーステータスパッケージをベースにしています。

TencentOS ServerユーザーステータスソフトウェアパッケージはRHELと100%バイナリー互換です。

### TencentOS Serverのカーネルにはどのようなバージョンがありますか。
TencentOS Serverのカーネル（略称TK）には次の2つのバージョンがあります。
- TK3：コミュニティ4.14longtermカーネルバージョンをベースにしています。
- TK4：コミュニティ5.4longtermカーネルバージョンをベースにしています。

TKのコードはGitHubで取得できます。詳細については、[Tencent OS-kernel](https://github.com/Tencent/Tencent OS-kernel)をご参照ください。

### TencentOS Serverのライフサイクルはどのくらいですか。
TencentOS Server各バージョンのライフサイクルは次のとおりです。bugfixとセキュリティパッチの更新はライフサイクルが終了するまで継続的に提供されます。
- TencentOS Server 2リリース版：2024年12月31日までサポートされます。
- TencentOS Server 3リリース版：2029年12月31日までサポートされます。

### Tencent CloudでのTencentOS Serverはどのように使用しますか。
Tencent CloudはTencentOS Serverの2つバージョンのパブリックイメージを提供しています。Linux オペレーティングシステムのCVMを作成する際に、TencentOS Serverのイメージバージョンを選択して使用することができます。

### TencentOS ServerはどのようなCVMインスタンスタイプをサポートしていますか。
TencentOS ServerはCVMインスタンスタイプの大部分をサポートしています。[CVM購入ページ](https://buy.intl.cloud.tencent.com/cvm?tab=custom&regionId=1&projectId=-1) でイメージを選択して使用を開始することができます。

### CVMでTencentOS Serverを使用する場合、料金がかかりますか。
かかりません。TencentOS Server自体は無償で使用でき、CVMの運用料金を支払う必要があるだけです。

### TencentOS Server使用後のソフトウェアのインストールとアップグレード方法は。
TencentOS Serverリリース版は、`yum` コマンドまたはTencentOS Serverに付属の`t`コマンドを使用してソフトウェアパッケージを管理できます。なお、TencentOS Server3は、`dnf`コマンドを使用してもソフトウェアパッケージを管理できます。

### ローカルでTencentOS Serverをインストールして使用できますか。
できます。TencentOS Serverリリース版ISOはTencent Cloudソフトウェアソースに移動してダウンロードを実行できます（[ここをクリックしてダウンロード](http://mirrors.tencent.com/tlinux/2.4/iso/) TencentOS Server 2、[ここをクリックしてダウンロード](http://mirrors.tencent.com/tlinux/3.1/iso/x86_64/) TencentOS Server 3）。
ローカルサーバーまたはvirtualboxなどの仮想マシンにインストールして使用できます。

### TencentOS Serverのソースコード を確認できますか。
TencentOS Server は完全なオープンソースです。[Tencent Cloudソフトウェアソース](http://mirrors.tencent.com/) に移動してソースコードパッケージを取得できます。またシステムで`yum downloader --source glibc`コマンドを使用して取得することもできます。

### TencentOS Server は32ビットアプリケーションプログラムとライブラリをサポートしていますか。
現時点ではサポートしていません。TencentOS Server2はyumを介した一部の32ビットソフトウェアパッケージのインストールのみをサポートしています。

### TencentOS Serverはシステムのセキュリティをどのように保証していますか。
TencentOS ServerバージョンはRHEL7とRHEL8とバイナリー互換であり、RHELのセキュリティ仕様に準拠しています。Tencent Cloudは次の面からTencentOS Serverシステムのセキュリティを保証しています。
- Tencentが自社開発した脆弱性スキャンツールと業界標準の脆弱性スキャンとセキュリティ検査ツールを使用して、定期的にセキュリティスキャンを実施します。
- Tencent Securityチームと共同で、TencentOS Serverのセキュリティスキャンとセキュリティ強化をサポートします。
- RHELとコミュニティのCVEパッチを定期的に評価し、ユーザーステータスソフトウェアパッケージを定期的に更新して、セキュリティの脆弱性を修復します。
- Tencent CloudのCloud Workload Protection機能を介してシステムのセキュリティヘルスチェックを定期的に実行し、ユーザーにセキュリティ警告と修復方法を通知します。



