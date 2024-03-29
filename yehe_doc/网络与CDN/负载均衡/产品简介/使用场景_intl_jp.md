CLBは主に以下のシーンに適用します。
- トラフィックの分配。ロードバランシングによって高アクセス量の業務を複数のCVMに分散させます。
- 単一点障害の解消。一部のCVMが使用できなくなった場合、CLBは障害の発生したCVMインスタンスを自動的にブロックし、アプリケーションシステムの正常な動作を保障します。
- 水平スケーリング。業務の発展の必要性に応じてアプリケーションシステムのサービス機能を拡張します。各種Web ServerおよびApp Serverに適用可能です。
- グローバルなロードバランシング。グローバルなマルチリージョンロードバランシングをサポートし、異なるリージョン間の障害復旧を保障します。

## トラフィックの分配と単一点障害の解消
ロードバランシングによって業務トラフィックを複数のCVMに分散させることができます。
- 業務のクライアントがCLBにアクセスします。
- 複数のCVMによってハイパフォーマンスで可用性の高いサービスプールを構成し、CLBが業務トラフィックをこれらのCVMに転送します。
- 1台もしくは数台のCVMが使用できなくなった場合、CLBは障害の発生したCVMインスタンスを自動的にブロックし、正常に実行中のCVMインスタンスにリクエストを分配することで、アプリケーションシステムの正常な動作を保障します。
- 業務を複数のアベイラビリティーゾーンにデプロイしている場合は、バックエンドサーバー層におけるマルチアベイラビリティーゾーン障害復旧を保障できるように、1台のCLBを同時に複数のアベイラビリティーゾーンのCVMインスタンスにバインドすることをお勧めします。
- セッション維持機能によって、同一のクライアントのリクエストを同一のバックエンドCVMに転送し、アクセス効率を高めることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/af522691e22caa4cc6160a7fe17880d8.svg)

## 水平スケーリング
CLBは[Auto Scaling](https://intl.cloud.tencent.com/document/product/377)との組み合わせによって、CVMインスタンスをニーズに応じて作成およびリリースすることができます。
- 自動スケーリングポリシーを設定してCVMインスタンス数を管理し、インスタンス環境のデプロイを完了するとともに、業務の安定した円滑な実行を保証することができます。需要のピーク時にはCVMインスタンス数を自動的に増やし、パフォーマンスが影響を受けないようにします。需要が比較的少ないときは、CVMインスタンス数を減らしてコストを抑えます。
- EC業界の「11月11日（独身の日）」、「6月18日」などの大型セールイベントでは、Webアクセス量が瞬時に10倍に跳ね上がる場合もありますが、それは数時間程度しか持続しません。CLBとAuto Scalingを使用することで、ITコストを最大限に節約することが可能です。
![](https://qcloudimg.tencent-cloud.cn/raw/38d3f5c690ecb3344e75af20431d5986.svg)

## グローバルロードバランシング
DNS解決DNSPodとの組み合わせによって、業務トラフィックをグローバルな各リージョンのCLBに解決し、マルチサイトアクティブおよび異なるリージョン間の障害復旧を保障します。
- 異なるリージョンにCLBインスタンスをデプロイし、それぞれに対応するリージョンのCVMをバインドすることができます。
- DNS解決DNSPodを使用して、ドメイン名を各リージョンのCLB VIPに解決します。
- 業務トラフィックをドメイン名解決およびCLBによって複数のリージョンの複数のCVMに転送することで、グローバルなロードバランシングを実現します。
- あるリージョンが使用できなくなった場合は、対応するリージョンのCLB VIPの解決を一時的に停止することで業務への影響が避けられます。
![](https://qcloudimg.tencent-cloud.cn/raw/5a71a839a2aa222e16b878e28c26c7db.svg)


