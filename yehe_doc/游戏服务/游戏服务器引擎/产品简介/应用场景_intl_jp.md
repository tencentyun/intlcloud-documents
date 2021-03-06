Game Server Elastic-scalingは各ゲームの様々なシナリオに応用できます。各ゲームシナリオは以下の通りです。


### 対戦サーバー
対戦サーバーは通常、数分～数十分、長くても1時間以内で対局を終了します。トラフィックは毎日正午と夕方がピークとなりますが、ゲームユーザーのオフピーク時は、サーバーを使用する必要はありません。GSEによりコストを大幅に下げられます。ピーク時はスケールアウト、オフピーク時はスケールインが実行されます。このほかGSEは、毎回一番近い地域を対局にアサインして対戦することができるため、ネットワークの安定性と対戦の公平性が保障されます。

テーブルゲーム、ターン性/戦略、リアルタイム対戦類のゲームに適用されます。ゲームサーバーセッションを作成について、そのセッションはルーム、サービスを意味します。プレイヤーたちはゲームサーバーセッションで戦闘、チャットなどの通信をします。




### メッセージプッシュ 
よく使うゲームフレームでクライアントとサーバーは持続的なコネクションを維持する必要があります。サーバーはクライアントにリアルタイムでメッセージプッシュを行うことができます。一般的にメッセージプッシュはゲームのコアモジュールです。

メッセージプッシュのデプロイレベルで発生する問題：
- ネットワークの不具合、メッセージの大部分がプッシュ送信できないこと。
- 多くのメッセージプッシュが数台の高構成サーバーを使用しているため、1台のサーバーの不具合が影響する範囲が大きいこと。

GSEを使用すると、コストを最低に抑えながらの災害復旧が可能であり、不具合が生じても、すぐに他の地域のサーバーに切り換えることができます。メッセージプッシュは複数のサーバー上に分散されます。このため、1台のサーバーに不具合が生じても影響は限定的であるほか、すぐに他のサーバーに切り換えることができます。



