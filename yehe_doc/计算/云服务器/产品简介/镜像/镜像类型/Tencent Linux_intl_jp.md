TencentOS Server（別名、Tencent Linux。略称、TSまたはtlinux）はTencentがクラウドシナリオ用に開発されたLinux OSであり、特別な機能とパフォーマンスの最適化を提供し、CVMインスタンスのアプリケーションに高性能、安全で信頼性の高い実行環境を提供します。TencentOS Serverは無料で使用でき、 CentOS（ディストリビューション）で開発されたアプリケーションは TencentOS Serverで直接実行できます。Tencent OSチームは、継続的な更新、メンテナンス、およびテクニカルサポートをユーザーに提供します。

## ユースケース

TencentOS Serverは次のシナリオに適しています：

- TencentOS Serverは、ほとんどのCVMインスタンスに適しています。
- インスタンスを起動するとき、関連する操作をユーザーデータ（すなわち userdata の方式）経由でcloud-initに転送し、インスタンスを起動する時に動的構成の目的を達成できます。

## TencentOS Server 2.4環境の説明

### ユーザーモード環境

ユーザーモードのソフトウェアパッケージは、CentOS 7の最新バージョンとの互換性があります。CentOS 7バージョンのソフトウェアパッケージは、 TencentOS Server 2.4で直接使用できます。

### システムサービスと設定の最適化

#### システムサービス

- `tlinux-irqaffinity`：TencentOS Server上のIRQアフィニティサービス。
- `tlinux-bootlocal`：TencentOS Server bootlocalサービス。起動時に`/etc/rc.d/boot.local`スクリプトを自動実行します。

#### システムツール

`tencent-tools`：tos（略称、t）コマンドは、システム管理に使用されます。サポートされているパラメーターは次のとおりです。

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

- **pam**：パスワードの複雑さを増やす。
- **`/etc/bashrc` 変更**：bashの表示を最適化します。
- **`/etc/hosts`**：TENCENT64とTENCENT64.siteを追加します。
- **`/root/.bashrc`**：設定を最適化します。

#### TencentOS Server 2.4 カーネル

TencentOS Server は、コミュニティLongterm 4.14 長期サポート版カーネルを使用します。詳細については、[TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel)をご参照ください。


## TencentOS Serverを取得する

次の方法を使用して、TencentOS Serverを入手して使用できます。

- CVMインスタンスを作成する時、パブリックイメージを選択し、対応するTencentOS Server バージョンを選択します。
  詳細については、 [インスタンスの作成](http://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
- 作成済みのCVMインスタンスは、システムの再インストールにより現在のOSをTencentOS Serverに変更できます。
  詳細な操作については、[システムの再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。

## リリース説明

| リリース時間      | イメージバージョン                                                 | バージョンの説明                                                   |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 2019年9月17日 | TencentOS Server 2.4、元の名前 ：Tencent linux release 2.4 (Final) | イメージ ID：img-hdt9xxkt<br>カーネルバージョン：4.14.105<br>地域：すべての地域 |


## テクニカルサポート

Tencent CloudはTencentOS Serverに次のテクニカルサポートを提供：

 - YUM ソースでセキュリティ更新（Security Updates）を提供し、 `yum update` コマンドを実行するだけで、Tlinuxを最新バージョンに更新できます。
- TencentOS Server はカーネルコミュニティによって長期的にサポートされている4.14.105バージョンに基づいてクラウドシナリオ用に設計されたオペレーティングシステムイメージです。Tencent Cloudは、 TencentOS Serverの使用中に発生した問題を解決するための支援を提供します。
