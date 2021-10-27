TencentOS Server（別名Tencent Linux、略称はTSまたはtlinux）はTencentがクラウドシーンのために開発したLinux OSであり、特定の機能を提供するとともにパフォーマンスを最適化し、CVMインスタンスにおけるアプリケーションプログラムのために高性能かつより安全で信頼性の高い運用環境をご提供します。TencentOS Serverは無料で利用でき、CentOS（およびその他のディストリビューション）上で開発されたアプリケーションプログラムをTencentOS Server上で直接運用することができます。ユーザーはTencent Cloudチームによる更新とメンテナンスおよびテクニカルサポートを引き続き受けることが可能です。

## 適用説明

TencentOS Serverは次のようなシーンに適しています。

- Cloud Physical Machine2.0を含む、ほとんどのCVMの各仕様インスタンスファミリー。
- インスタンスの起動時は、ユーザーデータ（userdataの方式）によって関連の操作をcloud-initに伝達することで、インスタンス起動時に動的設定を行えるようにする必要があります。

## TencentOS Server環境説明

### ユーザーステータス環境
- TencentOS Server 2ユーザーステータスのソフトウェアパッケージは最新版のCentOS 7との間で互換性を有しています。CentOS 7バージョンのソフトウェアパッケージはTencentOS Server 2.4で直接使用することができます。
- TencentOS Server 3ユーザーステータスのソフトウェアパッケージは最新版のRHEL 8との間で互換性を有しています。そのため、RHEL 8バージョンのソフトウェアパッケージは、TencentOS Server 3.1でそのまま使用することができます。

### システムサービスおよび設定の最適化

#### システムサービス

- `tlinux-irqaffinity`：TencentOS Serverが自動的に割り当てサービスを中断します。
- `tlinux-bootlocal`：TencentOS Server bootlocalサービスであり、起動時に自動的に `/etc/rc.d/boot.local`を実行します。

#### システムツール

`tencent-tools`：tos（略称t）コマンドであり、システム管理に使用します。サポートするパラメータは次のとおりです。

```bash
tos version 2.2
Usage:
	tos TencentOS Server System Management Toolset
	tos -u|-U| update [rpm_name]	Update the system 
	tos -i|-I| install rpm_name	install rpms
	tos -s|-S| show			Show the system version
	tos -c|-C| check [rpm_name]	Check the modified rpms
	tos -f yum | fix yum		Fix yum problems
	tos -f dns | fix dns		Fix DNS problems
	tos -a|-A | analyze		Analyze the system performance 
	tos set dns			Set DNS
	tos set irq			Set irqaffinity, restart irqaffinity service
	tos -cu| check-update		Check available package updates
	tos -b|-B| backup [ reboot ]	Backup the system online, or reboot to backup 
	tos -r|-R| recover|reinstall	Recover or Reinstall the system
	tos -h|-H| help			Show this usage
	tos -v|-V| version		Show the script version
```

#### システム設定

- **pam**：パスワードの複雑度を高めます。
- **`/etc/bashrc` 修正**：bash表示を最適化します。
- **`/etc/hosts`**：TENCENT64およびTENCENT64.siteを追加します。
- **`/root/.bashrc`**：設定を最適化します。


### TencentOS Serverカーネル
TencentOS-kernelは、4.14と5.4という2つのバージョンを提供しています。詳細については、[TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel)をご参照ください。

## リリースの説明

<table>
  <tr>
	<th>発表時間</th>
	<th style="width: 30%">イメージバージョン</th>
	<th>バージョン説明</th>
	<th>発表リージョン</th>
  </tr>
  <tr>
	<td>2021年7月13日</td>
	<td>TencentOS Server 3.1</td>
	<td>イメージID：<a href="https://console.cloud.tencent.com/cvm/image/detail?rid=16&id=img-eb30mz89">img-eb30mz89</a><br>カーネルバージョン：5.4.119</td>
	<td>全リージョン</td>
  </tr>
  <tr>
	<td>2019年9月17日</td>
	<td>TencentOS Server 2.4、旧称はTencent linux release 2.4 (Final)</td>
	<td>イメージID：<a href="https://console.cloud.tencent.com/cvm/image/detail?rid=16&id=img-hdt9xxkt">img-hdt9xxkt</a><br>カーネルバージョン：4.14.105</td>
	<td>全リージョン</td>
  </tr>
</table>


## TencentOS Serverの取得

次の方法によってTencentOS Serverを取得および使用できます。

- CVMインスタンスの作成時はパブリックイメージを選択し、TencentOS Serverの該当のバージョンを選択します。
  操作の詳細については[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
- CVMインスタンスが作成済みの場合は、システムの再インストールによって既存のOSをTencentOS Serverに変更することができます。
  操作の詳細については、[システムの再インストール](https://intl.cloud.tencent.com/document/product/213/4933)をご参照ください。


## テクニカルサポート

Tencent Cloudがご提供するTencentOS Serverのテクニカルサポートは次のとおりです。

- YUMリポジトリでセキュリティアップデート（Security Updates）を提供し、`yum update`コマンドの実行によってバージョンの更新が行えます。
- TencentOS Serverはカーネルコミュニティが長期的にサポートするバージョンをベースにしており、クラウド環境に合わせてカスタマイズされたOSイメージです。Tencent CloudはTencentOS Serverご使用の過程で発生する問題に対しテクニカルサポートを提供します。
