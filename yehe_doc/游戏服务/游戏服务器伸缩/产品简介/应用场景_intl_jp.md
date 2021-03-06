GSEは異なるゲームの多様なシナリオを使用することができます。各ゲームシナリオは以下のとおりです。

### 対戦サーバー
対戦サーバーは通常は数分、10数分で対戦を終了し、最長でも1時間を超えません。毎日正午と夜にピークになります。ゲームユーザーのオフピーク時には、サーバーを使用する必要がありません。GSEを使用すると、ピーク/オフピーク時にサーバーを瞬時に拡張/縮小できるため、コストを大幅に抑えることができます。さらに、GSEでは毎回対戦に最も近いリージョンを割り当てて対戦させることができ、ネットワークの安定および対戦の公平性が確保されます。

テーブルゲーム、ターン制/ストラテジー、リアルタイム対戦ゲームに適しています。ゲームサーバーセッションを作成すると、このセッションは1つのルーム、1つのサービスを表し、ゲームサーバーセッションのプレイヤーは、対戦したり、チャットしたりしてコミュニケーションすることができます。




### メッセージPUSH 
一般的に使用されるゲームフレームワークでは、クライアントとサーバーは長期的な接続を保持し、サーバーはメッセージをリアルタイムでクライアントにプッシュする必要があります。通常、プッシュ通知はゲームのコアモジュールです。

プッシュ通知ではデプロイ中に以下の問題が発生する可能性があります。
- ネットワーク障害、多数のプッシュ通知が送信されない。
- 大半のプッシュ通知は数台のハイスペックサーバーを使用しており、1台でもサーバーに障害が発生すると、サービスに大きな影響を与える。

GSEを使用すると、最低コストでクロスリージョンの障害復旧が可能になります。特定のリージョンで障害が発生した場合、他のリージョンにすばやく切り替えることができます。プッシュ通知サービスは複数のサーバーに分散されているため、1つのサーバーで障害が発生した場合でも影響を受ける範囲が小さく、他のサーバーにすばやく切り替えることができます。



