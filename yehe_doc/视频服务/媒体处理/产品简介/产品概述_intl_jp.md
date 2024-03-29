Media Processing Service（MPS）は、クラウドオーディオビデオ処理サービスの一種です。Tencentが長年培ってきたオーディオビデオ分野での研究成果をベースに、高性能のエンコード機能を提供し、ストレージと帯域幅コストの大幅な削減や、すべてのプラットフォームでの再生を実現できます。また、ビデオスクリーンキャプチャ、オーディオビデオエンハンスメント、コンテンツ理解、コンテンツ審査などの機能も提供し、様々なシーンでのビデオ処理ニーズに対応できます。

## 製品アーキテクチャ
コンソール、SDKまたはAPIアップロード方式により、ビデオソースファイルをCloud Object Storage（COS）のバケットにアップロードし、MPSの**サービスオーケストレーション**メカニズムによってメディア処理タスクの自動実行をトリガーすることができます。さらにCloud Message Queueによるメディア処理イベント通知の受信もサポートし、トランスコードタスクの実行の様子を速やかに把握することができます。MPS製品のアーキテクチャ図を次に示します。

<img src="https://qcloudimg.tencent-cloud.cn/raw/4efd48508c63bb8169f9cad585240ce0.png" style="box-shadow: none;">