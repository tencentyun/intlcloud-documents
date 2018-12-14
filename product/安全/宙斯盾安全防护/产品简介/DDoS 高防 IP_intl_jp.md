##DDoS高保護IPアドレスとは？
DDoS高保護IPは、DDoS攻撃に対するインターネットサービス防御の主な製品であり、トラフィックの多いDDoS攻撃に効果的に対処できます。高保護IPは、地域と回線の次元によって豊富な防衛リソースを提供できます。サービスの地域とネットワークに基づいて自分に合ったリソースを選ぶことができます。現時点では、国内BGPと非BGP高保護IPを提供することができ、中国国外には中国香港、西アメリカ、日本、韓国、シンガポールなどの地域があります。Tencent Cloudの高保護 IPは最大でTレベルの攻撃トラフィックを処理できます。

##使用シナリオ
DDoS高保護IPは、Tencent CloudおよびTencent Cloud以外のすべてのクラウド仮想マシンに対応します。

##保護原則
DDoS高保護IPは、プロキシ転送モードで実サーバを保護します。サービストラフィックは、高保護IPに直接アクセスしてから、実サーバにトラフィック転送します。DDoS攻撃が発生する場合、攻撃トラフィックが高保護IPを通過するとき、保護システムはフィルタリングとクリーニングを実行し、クリーニングサービストラフィックをサービスサーバーにトラフィック転送して、DDoS攻撃シナリオでのサービスの可用性を確保します。

##なぜDDoS高保護IPを選ぶのですか？
-実際の実サーバIPの非表示
DDoS高保護IPは、プロキシ転送モードで実サーバIPにサービストラフィックを転送し、実サーバIPを非表示にします。攻撃トラフィックは消去され、実サーバは保護されます。
-超広帯域幅の保護
DDoS高保護IPは、クラウド内外のサーバーに対してTレベルの保護を提供し、トラフィックの多いDDoS攻撃やCC攻撃を簡単に防御します。
>**注意：**
>より高度な帯域幅の保護を設定する必要がある場合は、カスタマーサービスに連絡してください。
-単一IP、パッケージの購入をサポートします
DDoS高保護IPは、1つまたは複数の異なる回線のIPをワンタイム購入することができます。これは柔軟に購入し、さまざまなサービスシナリオで使用できます。サービスの需要が主に特定のキャリアラインである場合は、単一のIP保護を直接購入することができます。パッケージは、ユーザーが異なるネットワーク間でのアクセスをしないように、複数の回線保護を提供します。
-フレキシブル課金
お金を節約するために、毎月プリペイドによる最低保証保護+日ごとの支払いによる柔軟な保護を提供し、実際の攻撃量に応じて課金します。詳細は、[課金の説明](https://cloud.tencent.com/document/product/685/15263)を参照してください。

##使用時に注意を払うべきこと
DDoS高保護IPは、保護のために高保護IPをサービスIPとしてリリースすることで実サーバIPを非表示にします。ユーザーの実サーバが攻撃され、実サーバIPが公開されている場合は、、実サーバIPの機密性を確保し、攻撃者が直接実サーバを攻撃できないように、DDoS高保護IPサービスを購入してから、実サーバIPを交換することをお勧めします。Tencent Cloud Virtual Machine IPの場合は、[Tencent Cloud Virtual Machine IPアドレスの変更方法](https://cloud.tencent.com/document/product/685/18802)を参照してください。

##DDoS高保護IPの設定方法
[Aegis Anti-DDoS Console](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fgamesec)にログインして、左のディレクトリで【DDos高保護IP】をクリックし、【高保護IPを購入】を選択します。操作の詳細は、[DDoS高保護IP](https://cloud.tencent.com/document/product/685/15264)を参照してください。
