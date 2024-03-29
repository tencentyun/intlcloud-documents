TencentOS Server（Tlinux、TSと略記）は、クラウドシナリオのためにTencent Cloudによって開発されたLinux OSです。特定の機能とパフォーマンスの最適化を提供し、CVMインスタンスのアプリケーションにより高いパフォーマンスとより安全で信頼性の高い動作環境を提供します。TSは、Linuxカーネルに基づいて独自に開発および設計されており、OS分野でTencentの技術的蓄積を10年以上蓄積しており、Tencentの内部の大規模サービスによって長年にわたって検証および洗練されています。Tencentの内部OSの99％以上を占めています。Tencentのすべてのサービスをカバーしています。同時に、Tencentは、ソーシャルネットワーキング、ゲーム、金融支払い、AI、セキュリティなど、中国で最も多様なサービスエコシステムを備えており、安定性、セキュリティ、互換性、パフォーマンスなどのコア機能が完全に検証されています。コミュニティOSバージョンと比較して、TSは、安定性、パフォーマンス、コンテナのインフラストラクチャなどのコア機能の点で全面的に強化および最適化されており、企業に安定的かつ可用性の高いサービスを提供しています。このシステムは、サービスの厳しい負荷要件を満たし、最高のクラウドOSの作成に取り組み、CentOSよりも優れたエンタープライズクラスOSのソリューションでもあります。

TSは現在使用可能であり、ユーザーモード環境はCentOSと互換性があります。CentOSで開発されたアプリケーションはTSで直接実行できます。


## ユースケース
TSは、標準型、コンピューティング型、メモリ型、ハイIO型など、ほとんどの標準型に適しています。また、Cloud Physical Machine (CPM) 2.0および高性能コンピューティングクラスターもサポートしています。

<dx-alert infotype="notice" title="">
TSを使用してGPUインスタンスを実行する必要がある場合、対応するGPUドライバーをインストールしてください。
</dx-alert>


## TSの優位性
- **非常に安定し、数千万のノードによって検証されている**
TSは、大規模なサービスによって長期間にわたって実地テストを受けており、合計で数千万のデプロイがあり、全体の可用性は99.999%に達しています。
- **完全に最適化された、パフォーマンスがより高い**
深く最適化された高性能OSは、システム内のさまざまなソフトウェアを最適化しており、通常のサービスパフォーマンスは50%以上向上しています。Tencent Cloudを介してTSを使用すると、より高いパフォーマンスを得ることができます。
- **オープンソースと互換性があり、クラウド上のより優れたOS**
100%オープンソースのLinuxリリースバージョンです。ユーザーモードは、CentOSとの互換性を維持し、安定性とパフォーマンスの面でより多くの利点があります。クラウド上のCentOSのより優れた代替手段です。
- **クラウド向けに生じて、特別にカスタマイズされる**
オープンスタンダードベースに基づいた最新の仮想化およびクラウドネイティブツールを含み、さまざまなワークロードに適したクラウド向けに開発されています。
- **安全でコンプライアンス、ダウンタイムゼロのリカバー**
セキュリティラボは、システムセキュリティを保護します。システムレベルのセキュリティを強化し、さまざまな脆弱性をタイムリーに修正し、ホットパッチ修復をサポートして不要なダウンタイムを回避できます。



### TSのイメージバージョン
現在、TencentCloudには、ユーザーが選択できる3つのTSイメージがあります：

<table>
<tr>
<th width="35%">イメージバージョン</th>
<th>説明</th>
</tr>
<tr>
<td>TencentOS Server 3.1</td>
<td>CentOS 8ユーザーモードと完全に互換性があり、コミュニティ5.4 LTSカーネルに基づいて深く最適化されたtkernel4バージョンをサポートします。</td>
</tr>
<tr>
<td>TencentOS Server 2.4</td>
<td>CentOS 7ユーザーモードと完全に互換性があり、コミュニティ4.14 LTSカーネルに基づいて深く最適化されたtkernel3バージョンをサポートします。</td>
</tr>
<tr>
<td>TencentOS Server 2.4（TK4）</td>
<td>CentOS 7ユーザーモードと完全に互換性があり、コミュニティ5.4 LTSカーネルに基づいて深く最適化されたtkernel3バージョンをサポートします。</td>
</tr>
</table>



## TSカーネル
TencentOS Server kernel（tkernelと略記）は、リリースバージョンからデカップリングされ、現在のメインカーネルは2つのバージョンに分けられます。
- コミュニティ5.4 LTSに基づいて深く最適化されたtkernel4（tk4と略記）。
- コミュニティ4.14 LTSに基づいて深く最適化されたtkernel3（tk3と略記）。
詳細については、[TencentOS kernel githubウェアハウス](https://github.com/Tencent/TencentOS-kernel)をご参照ください。

## TencentOS Serverの使用 

### クラウド上の使用
インスタンスの作成または既存インスタンスOSのリインストールのときに、パブリックイメージを選択し、対応するバージョンのOpenCloudOSを使用することを選択できます。操作の詳細については、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)および[システムのリインストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

### ローカルエクスペリエンス
次の方法によってTSをローカルでエクスペリエンスできます：
- TencentOS Server 2.4 ：[iso](http://mirrors.tencent.com/tlinux/2.4/iso/)および[qcow](http://mirrors.tencent.com/tlinux/2.4/images/)。
- TencentOS Server 3.1  ：[iso](http://mirrors.tencent.com/tlinux/3.1/iso/)および[qcow](http://mirrors.tencent.com/tlinux/3.1/images/)。



## サービスと更新
Tencent Cloudは、TSメジャーバージョンごとに5年以上、定期的なイメージの更新、新機能と最適化の導入、タイムリーなセキュリティの脆弱性の修正、バグの修正などを含むメンテナンスと更新を提供します。ストックサーバーは、yumを介してアップグレードし、脆弱性の修正をタイムリーに完了できます。
TSの詳細を理解する必要がある場合、アプレットからTencent Cloud　Assistantに相談してください。

