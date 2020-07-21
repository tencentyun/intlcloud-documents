<style> table th:first-of-type { width: 200px; } </style>

CDNサービスはさまざまなカスタム設定をサポートしているため、ビジネスニーズに応じて設定し、CDNアクセラレーション効果を最適化します。

## 基本設定
| 設定名                                    | 機能説明                |
| ---------------------------------------- | ------------------- |
| [基本情報](https://intl.cloud.tencent.com/document/product/228/7864) | ドメイン名の所属プロジェクト、サービスリージョンとサービスタイプの変更をサポートします。|
| [オリジンサーバー設定](https://intl.cloud.tencent.com/document/product/228/6289) | ドメイン名のオリジンサーバー設定には、オリジンサーバー基本情報、back to originリクエストプロトコル、back to origin Host とホットバックアップオリジンサーバー設定が含まれており、スムーズなback to originを確保できます。中国本土/中国本土以外の異なる設定をサポートします。  |


## アクセス制御
| 設定名                                      | 機能説明                      |
| ---------------------------------------- | ------------------------- |
| [フィルターパラメーターの設定](https://intl.cloud.tencent.com/document/product/228/35316)  | ノードがユーザーのアクセスURLの「？」の後のパラメーターを無視するかどうかを指定します。 |
| [リンク不正アクセス防止の設定](https://intl.cloud.tencent.com/document/product/228/6292) | HTTP refererのブラックリスト/ホワイトリスト設定します。中国本土/中国本土以外の異なる設定をサポートします。     |
| [IPブラックリスト/ホワイトリストの設定](https://intl.cloud.tencent.com/document/product/228/6298) | IPブラックリスト/ホワイトリストの設定をサポートすることで、アクセスコントロールを実現します。     |
| [IPアクセス頻度制限の設定](https://intl.cloud.tencent.com/document/product/228/6420) | 単一IP、単一ノードのアクセス頻度制限の設定をサポートします。      |
| [ビデオドラッグの設定](https://intl.cloud.tencent.com/document/product/228/8111)|   ビデオドラッグ設定の有効化をサポートします。              |
| [認証設定](https://intl.cloud.tencent.com/document/product/228/35237) | URL認証を設定します。中国本土/中国本土以外の異なる設定をサポートします。|


## キャッシュの有効期限の設定
| 設定名                                  | 機能説明              |
| ---------------------------------------- | ----------------- |
| [キャッシュの有効期限の設定](https://intl.cloud.tencent.com/document/product/228/35317)  | 指定したリソースのキャッシュ有効期限ルールを設定できます。|
| [ステータスコードキャッシュの設定](https://intl.cloud.tencent.com/document/product/228/35318)| 403および404ステータスコードのキャッシュ期間を設定できます。   |
| [HTTPヘッダーキャッシュの設定](https://intl.cloud.tencent.com/document/product/228/35319) | ヘッダーのキャッシュポリシーを設定できます。         |

## back to origin設定
| 設定名                                    | 機能説明                |
| ---------------------------------------- | -------------------- |
| [Range back to origin設定](https://intl.cloud.tencent.com/document/product/228/7184) | Range パートback to originを有効/無効にできます。  |
| [301/302リダイレクトの設定](https://intl.cloud.tencent.com/document/product/228/7183) | オリジンサーバーが301/302ステータスコードが戻された場合、リクエストをリダイレクトするかどうかを設定できます。|
| [back to originタイムアウト時間の設定](https://intl.cloud.tencent.com/document/product/228/35227) | back to origin TCP接続のタイムアウト時間と、back to originのデータ読み込みのタイムアウト時間を設定して、スムーズなback to originを確保します。 |


## 高度な設定

| 設定名                                    | 機能説明                             |
| ---------------------------------------- | -------------------------------- |
| [帯域幅制限の設定](https://intl.cloud.tencent.com/document/product/228/7541)  | ドメイン名に対し、帯域幅の上限値を設定します。上限に達すると、CDNサービスが無効になり、アクセス要求がオリジンサーバーに転送されます。中国本土/中国本土以外の異なる設定をサポートします。|
| [HTTPS設定](https://intl.cloud.tencent.com/document/product/228/35212) | HTTPSを設定することで、安全な加速を実現します。HTTPSの強制リダイレクト、HTTP2.0アクセス およびOCSPステープリング設定の有効/無効の設定をサポートします。   |
| [SEO最適化設定](https://intl.cloud.tencent.com/document/product/228/35219) | SEO最適化設定を有効にして、検索エンジンの重みの安定性を確保できます。       |
| [HTTPヘッダの設定](https://intl.cloud.tencent.com/document/product/228/35320) |HTTPヘッダの設定を追加します。                |


