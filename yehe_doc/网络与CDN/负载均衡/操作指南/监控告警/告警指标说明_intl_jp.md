## アラートの説明
注目するインスタンス指標についてアラートを作成することで、CLBインスタンスが実行状態においてある条件に達した際、関心のあるユーザーグループに対し速やかにアラート情報を送信することができます。これにより、異常な状態を速やかに発見してそれに応じた措置を確実にとることができ、システムの安定性と信頼性を維持することができます。その他の内容については[アラートの概要](https://intl.cloud.tencent.com/document/product/248/6126)をご参照ください。
CLBのアラートポリシーには次のタイプがあります。
- パブリックネットワークリスナー
- プライベートネットワークリスナー
- サーバーポート（その他）
  - リスナーディメンション
  - サーバーポートディメンション
- サーバーポート（従来型プライベートネットワーク）
- レイヤー7プロトコル監視

## パブリックネットワークリスナー/プライベートネットワークリスナー
現在、パブリックネットワークCLBとプライベートネットワークCLBはいずれもリスナーディメンションでのアラートをサポートしています。具体的な指標は次のとおりです。

|指標 | 単位 | 説明|
|----|------|----|
|インバウンド帯域幅 | Mbps  | 統計周期内で、クライアントがパブリックネットワーク経由でCLBにアクセスする際に使用した帯域幅です。|
|アウトバウンド帯域幅 | Mbps  | 統計周期内で、CLBがパブリックネットワークにアクセスする際に使用した帯域幅です。|
|インバウンドパケット数 | 個/s  | 統計周期内で、CLBが1秒間に受信したリクエストデータパケット数です。|
|アウトバウンドパケット数 | 個/s  | 統計周期内で、CLBが1秒間に送信したデータパケット数です。|

## サーバーポート（その他）
従来型のプライベートネットワークCLBを除くすべてのCLBは、次の2つのディメンションのアラートをサポートしています。
1. リスナーディメンション
あるリスナーのバックエンドサーバーの異常ポート数を設定し、そのリスナーにバインドしたすべてのサーバーポートの異常を統計することで、設定した閾値に基づいてアラートを発出できます。下の図の設定は、選択したリスナー下のすべてのバックエンドサーバーの異常ポート数を1分に1回収集し、異常ポート数が2回連続して10個/秒を超えるとアラートをトリガーし、かつ1日1回警告することを表します。
>?リスナーディメンションのアラートをご希望の場合は、[チケット申請](https://console.cloud.tencent.com/workorder/category)を提出してください。

 - アラートオブジェクトの設定：
![](https://main.qcloudimg.com/raw/bf26227edb359e6f7acd01febbbc38c9.png)
 - トリガー条件の設定：
![](https://main.qcloudimg.com/raw/7cb8c5db9a1fb616f478e2e109d31097.png)
2. サーバーポートディメンション
あるリスナーにバインドされたあるバックエンドCVMのあるポートの異常アラートを設定し、そのポートに異常があればアラートを送信することができます。
 - アラートオブジェクトの設定：
![](https://main.qcloudimg.com/raw/e1d947188535eac4189254ba0e8a26cb.png)
 - トリガー条件の設定：
![](https://main.qcloudimg.com/raw/80e4072ba35d426e4503a7b64ea63865.png)
>!
>- バックエンドサーバーポートの異常とは、バックエンドサーバーのそのポートが使用できなくなったことをCLBが検知したことを意味します。ポート異常はわずかなネットワークジッターによってもトリガーされる場合があります。
>- リスナーディメンションの統計には、そのリスナー下のすべてのバックエンドサービスポートのステータスが含まれ、単一のアラートを閾値アラートに集約します。ネットワークジッターの影響を低減するため、リスナーディメンションのアラートを使用することをお勧めします。

## サーバーポート（従来型プライベートネットワーク）
従来型プライベートネットワークCLBではサーバーポート異常アラートを設定することができます。具体的な設定は「サーバーポート（その他）-サーバーポートディメンション」の設定と同様です。
あるリスナーにバインドされたあるバックエンドCVMのあるポートの異常アラートを設定し、そのポートに異常があればアラートを送信することができます。

## レイヤー7プロトコル監視
すべてのレイヤー7リスナー（HTTP/HTTPS）について、レイヤー7独自の監視指標を含むアラートポリシーを設定できます。具体的な指標は次のとおりです。

|指標 | 単位 | 説明|
|----|------|----|
|インバウンド帯域幅 | Mbps  | 統計周期内で、クライアントがパブリックネットワーク経由でCLBにアクセスする際に使用した帯域幅です。|
|アウトバウンド帯域幅 | Mbps  | 統計周期内で、CLBがパブリックネットワークにアクセスする際に使用した帯域幅です。|
|インバウンドパケット数 | 個/s  | 統計周期内で、CLBが1秒間に受信したリクエストデータパケット数です。|
|アウトバウンドパケット数 | 個/s  | 統計周期内で、CLBが1秒間に送信したデータパケット数です。|
|新規接続数 | 個  | 統計周期内における1分間の新規接続の個数です。 |
|アクティブ接続数 | 個  | 統計周期内における1分間のアクティブ接続の個数です。|
|平均応答時間 | ms  | 統計周期内におけるCLBの平均応答時間です。|
|最大応答時間 | ms  | 統計周期内におけるCLBの最大応答時間です。|
|2xxステータスコード | 個  | 統計周期内で、バックエンドサーバーが返した2xxステータスコードの数です。 |
|3xxステータスコード | 個  | 統計周期内で、バックエンドサーバーが返した3xxステータスコードの数です。|
|4xxステータスコード | 個  | 統計周期内で、バックエンドサーバーが返した4xxステータスコードの数です。|
|5xxステータスコード | 個  | 統計周期内で、バックエンドサーバーが返した5xxステータスコードの数です。|
|404ステータスコード | 個  | 統計周期内で、バックエンドサーバーが返した404ステータスコードの数です。|
|502ステータスコード | 個  | 統計周期内で、バックエンドサーバーが返した502ステータスコードの数です。|
|CLBが返した3xxステータスコード | 個  | 統計周期内で、CLBが返した3xxステータスコードの数です。 |
|CLBが返した4xxステータスコード | 個  | 統計周期内で、CLBが返した4xxステータスコードの数です。|
|CLBが返した5xxステータスコード | 個  | 統計周期内で、CLBが返した5xxステータスコードの数です。|
|CLBが返した404ステータスコード | 個  | 統計周期内で、CLBが返した404ステータスコードの数です。|
|CLBが返した502ステータスコード | 個  | 統計周期内で、CLBが返した502ステータスコードの数です。|

