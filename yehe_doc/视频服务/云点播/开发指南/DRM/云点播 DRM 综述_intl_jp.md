現在のオンラインビデオ業界が急速に発展している一方、ネット上の海賊版の横行が深刻化しており、コンテンツ著作権保有者に非常に大きな損失を与えています。そのため、コンテンツ著作権保護の重要性は言うまでもありません。

## 商用DRM

商用DRMは、再生ライセンスをベースにし、高い安全性を実装したコンテンツ著作権保護ソリューションです。端末でビデオを再生する場合、まずライセンス（ライセンスには、復号化に必要なキー、キーの有効期限、端末情報などが含まれています）を取得しなければなりません。その後、取得したライセンスに含まれたキーを使用して復号化を行い、ビデオを再生します。

商用DRMには以下のメリットがあります：
- キーが見えない：キー自体が暗号化されており、コンテンツ復号化モジュール(CDM)のみがキーを読み取れます。
- ライセンスと端末との関連付け：ライセンスは1つの端末でのみ機能し、ほかの端末では利用できません。
- ライセンスの有効期限が指定可能：ライセンスの有効期限を指定できます。
- セキュアなデコードプロセス：ハードウェアレベル(TEE)の復号化とデコードをサポートします。
- 有名なコンテンツ著作権保有者の認証あり：Widevine、FairPlayはハリウッド、ディズニーなどの有名なコンテンツ著作権保有者の認証を受けています。

現在の主流な商用DRMソリューションには、WidevineとFairPlayの2種類があります：

| 商用DRMソリューション | サポートするアダプティブストリームプロトコル | サポートする再生環境                                               |
| ------------------- | -------------------- | ---------------------------------------------------------- |
| Widevine            | HLS、DASH            | Andriod系のプレイヤーとChrome、Firefox、Edge、Operaブラウザなど |
| FairPlay            | HLS                  | iOS系のプレイヤーとSafariブラウザなど                           |

## VOD DRMソリューション

商用DRMはビデオのコンテンツに高い安全性を提供しますが、ベースのない状態で導入するのにハードルがあって難しくなっています。そのため、DRMの機能を簡単に利用できるように、VODは、DRM暗号化、商用DRMを統合するワンストップソリューションを提供します。このソリューションには、証明書管理、ライセンス配布、復号化による再生などの機能が含まれています。

VOD DRMの暗号化・復号化による再生の全体的な処理プロセスは次のとおりです：

1. <b>ビデオのアップロード</b>：サービスバックエンドは、コンソールやサーバーAPIなどを介して、ビデオをVODにアップロードします。
2. <b>ビデオ処理のトリガー</b>：ビデオをアップロードすると同時に、暗号化されたアダプティブストリームトランスコーディングを指定します。アップロード後、ビデオの暗号化プロセスが開始します。
3. <b>キーの取得</b>：アダプティブストリームへのトランスコーディングと暗号化を行います。VODは、KMSモジュールからビデオ暗号化中に使用されるキーを取得します。
4. <b>暗号化とストレージへの書き込み</b>：ビデオのアダプティブストリームへのトランスコーディングと暗号化の実行後、出力ビデオコンテンツがVODのストレージに書き込まれます。
5. <b>メディア資産の更新</b>：暗号化されたビデオ情報は、メディア資産管理モジュールに書き込まれます。
6. <b>プレーヤー署名の取得</b>：サービス端末はVODのSuper Playerと統合され、プレーヤーはサービスサーバーにプレーヤーの署名をリクエストします。
7. <b>ダウンロードアドレスのリクエスト</b>：Super Playerは、VOD再生サービスからビデオのダウンロードアドレスを取得します。
8. <b>コンテンツのダウンロード</b>：Super Playerは、ダウンロードアドレスを介してVOD CDNからコンテンツをダウンロードします。
9. <b>再生ライセンスの取得</b>：Super Playerはプレイヤー署名を持って再生ライセンスをリクエストします。
10. <b>復号化と再生</b>：Super Playerは復号化キーを使用して復号化して再生します。

![](https://qcloudimg.tencent-cloud.cn/raw/cac2fc608c14a604fd8145a8565a159a.png)

## アクセスの参考

VOD DRM暗号化機能を速やかに統合できるように、DRM暗号化ガイド[DRM暗号化ビデオの再生方法](https://intl.cloud.tencent.com/document/product/266/46642)を提供し、例を挙げて操作手順を説明しています。

