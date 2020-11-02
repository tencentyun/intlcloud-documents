
Tencent Linux（略称は Tlinux）はTencentがクラウドシナリオ用に開発されたLinux OSであり、特別な機能とパフォーマンスの最適化を提供し、CVMインスタンスのアプリケーションに高性能、安全で信頼性の高い実行環境を提供します。Tencent Linuxは無料で使用でき、 CentOS（ディストリビューション）で開発されたアプリケーションはTencent Linux で直接実行できます。Tencent Cloudは、継続的な更新、メンテナンス、およびテクニカルサポートをユーザーに提供します。

## ユースケース
Tencent Linux は次のシナリオに適しています：
- Tencent Linuxは、ほとんどのCVMインスタンスに適しています。
- インスタンスを起動する時、Tlinuxを使用して、関連する操作をユーザーデータ（すなわち userdata の方式）経由でcloud-initに転送し、インスタンスを起動する時に動的構成の目的を達成できます。

## 主な機能

</table>
	<tr><th>機能タイプ</th><th>機能説明</th></tr>
	<tr><td><b>カーネルのカスタマイズ</b></td><td>カーネルコミュニティによって長い間サポートされてきたバージョン4.14.105に基づいてカスタマイズして、クラウドシナリオに適用可能な新機能を追加し、カーネルのパフォーマンスを改善して、かつ重大な欠陥を修正します。</td></tr>
	<tr><td><b>コンテナのサポート</b></td><td>Tencent Linuxは、強化された分離と最適化されたパフォーマンスを提供することにより、コンテナーシナリオを最適化します：<ul style="margin: 0;"><li>meminfo、vmstat、cpuinfo、stat、loadavg などの分離</li><li> tcp_no_delay_ack、tcp_max_orphansなどのsysctl分離。</li><li>大量のファイルシステムとネットワークのバグ修正。</li></ul></td></tr>
	<tr><td><b>パフォーマンスの最適化</b></td><td>コンピューティング、ストレージおよびネットワークサブシステムが最適化されます。<ul style="margin: 0;"><li> XFSメモリ割り当てを最適化して、xfs kmem_alloc障害アラームを解決します。</li><li>受信したネットワークパケットのメモリ割り当てを最適化して、大量のUDPパケットを受信したときのメモリの使用量が多すぎる問題を解決します。</li><li>システムページキャッシュのメモリ使用量を制限して、最適なパフォーマンスを維持し、メモリ不足（OOM）エラー発生を防止します。</li></ul></td></tr>
	<tr><td><b>ソフトウェアパッケージ</b></td><td><ul style="margin: 0;"><li> CentOS 7 バージョンのソフトウェアパッケージに基づいてカスタマイズされています。</li><li>ユーザーモードのソフトウェアパッケージはCentOS 7と互換性があり、Tencent Linuxで直接使用できます。</li><li> Yellowdog Updater、Modified（YUM）経由で更新およびインストールします。</li><li>YUM を通してepel-release パッケージをインストールした後、 epelリポジトリのソフトウェアパッケージを利用できます。</li></ul></td></tr>
	<tr><td><b>欠陥のサポート</b></td><td><ul style="margin: 0;"><li>Kdump機能は、OSがクラッシュした場合に提供されます。</li><li>カーネルライブパッチがサポートされています。</li></ul></td></tr>
	<tr><td><b>セキュリティアップデート</b></td><td>Tencent Linuxは、セキュリティと機能を強化するために定期的なアップデートを提供しています。</td></tr>
</table>

## Tencent Linux2.4
### ユーザーモード環境
ユーザーモードのソフトウェアパッケージは、CentOS 7の最新バージョンとの互換性があります。CentOS 7バージョンのソフトウェアパッケージは、Tencent Linux2.4で直接使用できます。

### システムサービスと最適化設定
#### システムサービス
- `tlinux-irqaffinity`：Tencent Linux上のIRQアフィニティサービス。
- `tlinux-bootlocal`：Tencent Linux bootlocalサービス。起動時に `/etc/rc.d/boot.local`スクリプトを自動実行します。

#### システムツール
`tencent-tools`：システム管理に使用されるtos（t）コマンドです。サポートされているパラメーターは次のとおりです。
```bash
tos version 2.2
Usage:
	tos TencentOS Server System Management Toolset
	tos -u|-U| update [rpm_name]Update the system 
	tos -i|-I| install rpm_nameinstall rpms
	tos -s|-S| showShow the system version
	tos -c|-C| check [rpm_name]Check the modified rpms
	tos -f yum | fix yumFix yum problems
	tos -f dns | fix dnsFix DNS problems
	tos -a|-A | analyzeAnalyze the system performance 
	tos set dnsSet DNS
	tos set irqSet irqaffinity, restart irqaffinity service
	tos -cu| check-updateCheck available package updates
	tos -b|-B| backup [ reboot ]Backup the system online, or reboot to backup 
	tos -r|-R| recover|reinstallRecover or Reinstall the system
	tos -h|-H| helpShow this usage
	tos -v|-V| versionShow the script version
```

#### システム設定
- **pam**：強力なパスワードポリシーを設定します。
- **`/etc/bashrc` 変更：bashの表示を最適化します。
- **`/etc/hosts`**：TENCENT64とTENCENT64.siteを追加します。
- **`/root/.bashrc`**：設定を最適化します。

#### Tencent Linux 2.4カーネル
Tencent Linux 2.4は、Longterm 4.14 長期サポート版カーネルを使用します。詳細については、[TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel)をご参照ください。


##  Tlinux を取得する
次の方法を使用して、TencentLinuxを入手して使用できます。
- CVMインスタンスを作成する時、パブリックイメージを選択し、対応するTencent Linux バージョンを選択します。
詳細については、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
- 作成済みのCVMインスタンスは、システムの再インストールにより現在のOSをTencent Linuxに変更できます。
詳細な操作については、[システムの再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

## リリース説明
| リリース時間 | イメージバージョン | 説明 |
|---------|---------|---------|
| 2019年9月17日 | Tencent Linux release 2.4 (Final) | イメージ ID：img-hdt9xxkt<br>カーネルバージョン：4.14.105<br>地域：すべての地域 |


## テクニカルサポート
- Tencent Cloudは Tencent Linux に次のテクニカルサポートを提供します：
Tencent Cloudは、 YUMリポジトリでセキュリティアップデートを提供し、 `yum update` コマンドを実行するだけで、Tlinuxを最新バージョンに更新できます。
- Tencent Linuxは、クラウドシナリオ用に設計されたオペレーティングシステムイメージです。Tencent Cloudは、Tencent Linuxの使用中に発生した問題を解決するための支援を提供します。
