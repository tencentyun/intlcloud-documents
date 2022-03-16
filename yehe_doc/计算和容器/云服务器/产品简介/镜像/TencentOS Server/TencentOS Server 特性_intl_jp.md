## カーネルカスタマイズ
カーネルコミュニティにより長期間サポートされるバージョンに基づきカスタマイズしました。クラウドのシナリオに適した特徴が追加され、カーネル性能が改善され、重大なバグが修正されました。

## Container Servicesにおけるパフォーマンスの最適化
Container Servicesに対する最適化が実行されました。以下のような隔離強化およびパフォーマンス最適化特性を提供します。
- meminfo、vmstat、cpuinfo、stat、loadavgなどの隔離。
- Sysctl隔離。例えばtcp_no_delay_ack、tcp_max_orphans。
- 大量のファイルシステムおよびネットワークのBUGFIX。
- IPVSモードの高並列処理ケースで、接続を再利用すると接続異常が発生する問題が解決されました。
- IPVSモードがハイスペックノード（多コア数）の時、IPVSルールが過度にネットワークグリッチを生成する問題が解決されました。
- コンテナが密集するケースで（単一ノード上のコンテナ量が比較的多い）、cAdvisorがmemcgを読み取るときにカーネルステータスが長くなりすぎ、ネットワークグリッチが発生する問題が解決されました。
- Podが大きい（占有コア数が多く、単一コア占有率が高い）ハイスペックノード（多コア数）のケースで、CPUのCLBによりネットワークグリッチが発生する問題が解決されました。
- 高並列処理ケースで、TCP接続監視（例えば、単独のデプロイcAdvisor設定がTCP接続を監視）によりネットワーク周期ジッターが発生する問題が解決されました。
- ネットワーク受信パケットのソフトウェア割り込みを最適化し、ネットワークパフォーマンスが改善されました。

## Container Servicesカスタマイズの特徴
### Container Servicesリソース表示の隔離
- ホストレベルスイッチの追加：カーネルでは類似のLXCFS特性がすでに実現しています。ユーザーはノードでLXCFSファイルシステムをデプロイしてPOD specを変更する必要はありません。ノードでグローバルスイッチ（`sysctl -w kernel.stats_isolated=1`）を有効にして、`/proc/cpuinfo`および`/proc/meminfo`等のファイルを取得するだけで、Container Services隔離をオンにすることができます。
<dx-alert infotype="notice" title="">
TencentOS Server 2.4バージョンのみが`kernel.stats_isolated`パラメータをサポートしており、TencentOS Server 2.4（TK4）および3.1以降のバージョンではサポートしていません。
</dx-alert>
- Container Servicesレベルのスイッチの追加：類似のノード監視コンポーネント等の特殊コンテナのために、Container Servicesレベルのスイッチ`kernel.container_stats_isolated`を追加しました。ホストレベルのスイッチを有効にする時は、Container Servicesの起動スクリプトでContainer Servicesレベルのスイッチを閉じると（`sysctl -w kernel.container_stats_isolated=0`）、Container Servicesで`/proc/cpuinfo`および`/proc/meminfo`ファイルを読み取る時にホスト情報を取得することができます。

### カーネルパラメータの隔離
以下のカーネルパラメータのnamespace化隔離を実現します。
- `net.ipv4.tcp_max_orphans`
- `net.ipv4.tcp_workaround_signed_windows`
- `net.ipv4.tcp_rmem`
- `net.ipv4.tcp_wmem`
- `vm.max_map_count`

### Container Servicesのデフォルトカーネルパラメータの最適化
Container Servicesネットワークのnamespace中の`net.core.somaxconn`のデフォルト値を4096に調整して、高並列処理の状況で半接続キューが一杯になるパケットロスの問題が減少します。

## パフォーマンスの最適化
Compute、Storage、およびNetworkingのサブシステムは、以下を含めてすべて最適化済みです。
- xfsメモリ割り当てを最適化して、xfs kmem_alloc割り当て失敗のアラームを解決しました。
- ネットワーク受信パケット大容量メモリの割り当て問題を最適化して、UDPパケットが大きい時にメモリ占有が多すぎる問題を解決しました。
- システムpage cacheの占有メモリ率を制限して、メモリの不足が業務に影響するパフォーマンスまたはOOMを回避するようにしました。

## ソフトウェアパッケージサポート
- TencentOS Server 2ユーザーステータスのソフトウェアパッケージは最新版のCentOS 7との間で互換性を有しています。CentOS 7バージョンのソフトウェアパッケージはTencentOS Server 2.4で直接使用することができます。
- TencentOS Server 3ユーザーステータスのソフトウェアパッケージは最新版のRHEL 8との間で互換性を有しています。そのため、RHEL 8バージョンのソフトウェアパッケージは、TencentOS Server 3.1でそのまま使用することができます。
- YUMを使用したソフトウェアパッケージのアップデートおよびインストールをサポートします。
- YUMを介してepel-releaseパッケージをインストールすると、epelソース内のソフトウェアパッケージを使用することができます。

## バグのサポート
- オペレーティングシステムクラッシュ後のkdumpカーネルコアダンプ機能を提供します。
- カーネルのホットパッチアップグレード機能を提供します。

## セキュリティ更新
TencentOS Serverは定期的に更新を実行し、セキュリティおよび機能を強化します。
