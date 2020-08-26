
Tencent Linux（略称は Tlinux）はTencentがクラウドシナリオ用に開発されたLinux OSであり、特別な機能とパフォーマンスの最適化を提供し、CVMインスタンスのアプリケーションに、高性能、安全、信頼性の高い実行環境を提供します。Tencent Linux は無料で使用でき、 CentOS（リリースバージョン）で開発されたアプリケーションは直接 Tencent Linux で実行できます。Tencent Cloudは、継続的な更新、メンテナンス、およびテクニカルサポートをユーザーに提供します。

## ユースケース
Tencent Linux は下記にユースケースに適用します：
- BM 2.0サーバーを含み、ほとんどのCVMの各仕様のインスタンス。
- インスタンスを起動する時、Tlinuxを使用して、関連する操作をユーザーデータ（すなわち userdata の方式）経由でcloud-initに転送し、インスタンスを起動する時に動的構成の目的を達成できます。

## 主な機能

<table>
	<tr><th>機能タイプ</th><th>機能内容</th></tr>
	<tr><td><b>カーネルのカスタマイズ</b></td><td>カーネルコミュニティが長い間サポートしてきた4.14.105バージョンに基づいてカスタマイズして、クラウドシナリオに適用可能な新機能を追加し、カーネルのパフォーマンスを改善して、かつ重大な欠陥を修正します。</td></tr>
	<tr><td><b>コンテナのサポート</b></td><td>コンテナのシナリオに対し最適化を行い、隔離の強化とパフォーマンス最適化機能を提供します：<ul style="margin: 0;"><li>meminfo、vmstat、cpuinfo、stat、loadavg などの隔離</li><li>Sysctl 隔離、例えば tcp_no_delay_ack、tcp_max_orphans</li><li>大量のファイルシステムとネットワークのバグ修正</li></ul></td></tr>
	<tr><td><b>パフォーマンスの最適化</b></td><td>コンピューティング、ストレージおよびネットワークサブシステムが最適化されます。<ul style="margin: 0;"><li> XFS kmem_allocエラーアラームを解決するために、XFSメモリ割り当てを最適化しました。</li><li>受信したネットワークパケットのメモリ割り当てを最適化して、 UDP パケットの容量が大きい時、メモリの過剰占有問題を解決します</li><li>システム page cacheが占有するメモリの割合を制限して、メモリ不足のため業務パフォーマンスに影響するのを回避します。</li></ul></td></tr>
	<tr><td><b>ソフトウェアパッケージ</b></td><td><ul style="margin: 0;"><li> CentOS 7 バージョンのソフトウェアパッケージに基づいてカスタマイズしました</li><li>ユーザーソフトウェアパッケージはCentOS 7と互換性があり、このバージョンのユーザーソフトウェアが直接 Tencent Linux 環境で利用できます</li><li> Yellowdog Updater、Modified（YUM）経由で更新およびインストールします。</li><li> YUM を通して epel-release パッケージをインストールした後、 epel ソースでのソフトウェアパッケージを利用できます</li></ul></td></tr>
	<tr><td><b>欠陥のサポート</b></td><td><ul style="margin: 0;"><li>Kdump機能は、OSがクラッシュした場合に提供されます。</li><li>カーネルのライブパッチアップグレード機能を提供します</li></ul></td></tr>
	<tr><td><b>セキュリティ更新</b></td><td>encent Linuxは、セキュリティと機能を強化するために定期的な更新を提供しています。</td></tr>
</table>

## リリース説明

| リリース時間 | イメージバージョン | バージョン説明 |
|---------|---------|---------|
| 2019年9月17日 | Tencent Linux release 2.4 (Final) | イメージ ID：img-hdt9xxkt<br>カーネルバージョン：4.14.105<br>リリースリージョン：すべてのリージョン |

##  Tlinux を取得する
[CVMコンソール](https://console.cloud.tencent.com/cvm)で Tencent Linux パブリックイメージを提供しました、 Tlinuxは以下の方法で入手して利用できます。
- CVMインスタンスを作成する時、パブリックイメージを選択し、対応するTencent Linux バージョンを選択します。
詳細については、 [インスタンスの作成](http://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
- 作成済みのCVMインスタンスは、システムの再インストールにより現在のOSを Tencent Linuxに変更できます。
詳細な操作については、[システムの再インストール](http://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

## テクニカルサポート
Tencent Cloudは Tencent Linux に次のテクニカルサポートを提供します：
- Tencent Cloudは、YUMリポジトリでセキュリティアップデートを提供します。 `yum update`コマンドを実行してTlinuxをアップグレードできます。
- Tencent Linuxは、カーネルコミュニティで長期的にサポートされているカーネルバージョン4.14.105に基づいて、クラウド環境に合わせてカスタマイズされたOSイメージです。Tencent Cloudは、Tlinuxの使用中に発生する問題に対するテクニカルサポートを提供します。
