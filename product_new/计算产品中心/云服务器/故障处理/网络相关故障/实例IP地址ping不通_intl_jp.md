## 故障事象

ローカルホストはインスタンスにpingが通らない場合は、以下のような原因が考えられます：
- ターゲットサーバーの設定が正確ではない
- ドメイン名の解析が正確ではない
- リンク故障

ローカルネットワークが正常に動作していることを前提として（他のウェブサイトにpingが正常に実行される）、下記の操作によりトラブルシューティングを実施します：
- [インスタンスはパブリックIPアドレスを設定したかどうかの確認](#isConfigurePublicIP)
- [セキュリティグループ設定を確認する](#CheckSecurityGroupSetting)
- [システム設定を確認する](#CheckOSSetting)
- [ドメイン名はICP申告にあるかどうかを確認する](#CheckDomainRegistration)
- [ドメイン名解析を確認する](#CheckDNS)
- [その他の操作](#OtherOperations)

## 処理手順

<span id="isConfigurePublicIP"></span>
### インスタンスはパブリックIPアドレスを設定したかどうかの確認

> インスタンスはパブリックIPアドレスを保有する場合のみ、Internet上の他のコンピュータと相互接続することができます。パブリックIPアドレスを保有していない場合、プライベートIPは外部からインスタンスへのpingが通りません。
>
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index) にログインします。
2.「インスタンスリスト」画面で、pingを実行したいインスタンスID/インスタンス名を選択して、このインスタンスの詳細画面にに入ります。
3.「ネットワーク情報」欄で、インスタンスはパブリックIPアドレスを設定したかどうかを確認します。
 - はい、[セキュリティグループ設定を確認](#CheckSecurityGroupSetting)してください。
 - いいえ、[Elastic パブリッIPをバインド](https://intl.cloud.tencent.com/document/product/213/16586) してください。

<span id="CheckSecurityGroupSetting"></span>
### セキュリティグループ設定を確認する

セキュリティグループとは、仮想ファイアウォールであり、関連付けられたインスタンスのインバウンドとアウトバウンドトラフィックを制御することができます。セキュリティグループのルールは、プロトコル、ポート及びポリシーなどを指定することができます。pingはICMPプロトコルを使用するため、インスタンスを関連付けたセキュリティグループは、ICMPを許可するかどうかをご確認ください。以下の操作を実行して、インスタンスが使用したセキュリティグループ、及び詳細なインバウンドルールとアウトバウンドルールを確認します：
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index) にログインします。
2.「インスタンスリスト」画面で、セキュリティグループ設定を必要とするインスタンスID/インスタンス名を選択して、このインスタンスの詳細画面に入ります。
3.【セキュリティグループ】タブを選択して、インスタンスのセキュリティグループ管理画面に入ります。
4. インスタンスが使用するセキュリティグループ、及び詳細なインバウンドルールとアウトバウンドルールを確認することにより、インスタンスを関連付けたセキュリティグループはICMPを許可するかどうかを判断します。
 - はい、[システム設定を確認](#CheckOSSetting) してください。
 - いいえ、ICMPプロトコルのポリシーを[許可]に設定します。

<span id="CheckOSSetting"></span>
### システム設定を確認する

インスタンスのOSタイプを判断して、確認方式を選択します。
- Linux OSは、[Linuxカーネルパラメータ及びファイアウォール設定を確認](#CheckLinux)してください。
- Windows OSは、[Windowsファイアウォール設定を確認](#CheckWindows) してください。

<span id="CheckLinux"></span>
#### Linuxカーネルパラメータ及びファイアウォール設定を確認する

> Linuxシステムは、ping通信の許可をカーネル及びファイアウォール設定の両方により决定します。いずれかを使用禁止とした場合は、pingパケットが「Request timeout」になります。

##### ーネルパラメータicmp_echo_ignore_allを確認する

1. インスタンスにログインします。
2. 下記のコマンドを実行して、システムのicmp_echo_ignore_all設定を確認します。
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - 戻された結果は0である場合、システムはすべてのICMP Echoリクエストを許可することを表します。[ファイアウォール設定を確認](#CheckLinuxFirewall) してください。
 - 戻された結果は1である場合、システムはすべてのICMP Echoリクエストを拒否することを表します。[ステップ3](#Linux_step03) を実行してください。
3. <span id="Linux_step03">下記のコマンドを実行して、カーネルパラメータicmp_echo_ignore_allの設定を修正します。</span>
```
echo "1" >/proc/sys/net/ipv4/icmp_echo_ignore_all　　
```

<span id="CheckLinuxFirewall"></span>
##### ファイアウォール設定を確認する

下記のコマンドを実行して、現在のサーバーのファイアウォールルール及び対応するICMPルールを禁止されているかどうかを確認します。
```
iptables -L
```
- 以下のような結果が戻された場合は、ICMPに対応するルールが禁止されていないことを表します。[ドメイン名はICP申告にあるかどうかを確認](#CheckDomainRegistration) してください。
```
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination  
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
```
- 戻された結果は、ICMPに対応するルールが禁止されているとした場合は、下記のコマンドを実行して、対応するルールを有効にします。
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Windows ファイアウォール設定を確認する

1. インスタンスをログインします。
2.【コントロールパネル】を開いて、【Windows Defender ファイアウォール設定】を選択します。
3.【Windows Defender ファイアウォール】インターフェースで、【詳細設定】を選択します。
4. 表示された「セキュリティが強化された Windows Defender ファイアウォール」ウィンドウで、ICMPに関するアウトバウンドとインバウンドのルールが禁止されているかどうかを確認します。
 - 下図に示すように、ICMPに関するアウトバウンドとインバウンドのルールが無効になっている場合は、ルールを有効にしてください。
 - ICMPに関するアウトバウンドとインバウンドのルールが有効になっている場合は、[ドメイン名はICP申告にあるかどうかを確認](#CheckDomainRegistration) してください。

<span id="CheckDomainRegistration"></span>
### ドメイン名はICP申告にあるかどうかを確認する

> パブリックIPアドレスへのping通信が成功したが、ドメイン名へのpingが失敗した場合は、ドメイン名はICP申告をしていない、またはドメイン名解析の問題が原因となる可能性があります。
>
中国工信部の規定により、許可を取得していない、又は登録手続きを履行していないのウェブサイトはIT情報サービスに従事してはいけません。そうでなければ法律違反となります。ウェブサイトの正常に長期的な運営に影響を与えないため、ウェブサイトを開設する場合、事前にウェブサイトのICP申告を推奨します。ICP申告が成功して、通信管理局に発行されたICP番号を取得すると、アクセスを開通できます。
- ドメイン名はICP申告をしていない場合、最初に[ドメイン名のICP申告](https://console.cloud.tencent.com/beian) を実行してください。
- Tencent Cloudのドメイン名サービスを利用している場合は、[ドメイン名サービスコンソール](https://console.cloud.tencent.com/domain) にログインして、対応するドメイン名の状況を確認することができます。
- ドメイン名は既にICP申告済みの場合、[ドメイン名の解析を確認](#CheckDNS) してください。

<span id="CheckDNS"></span>
### ドメイン名の解析を確認する

ドメイン名へのpingが通らないもうひとつの原因は、ドメイン名の解析が正確に設定されていないことです。Tencent Cloudのドメイン名サービスを利用している場合、以下の操作を実行して、ドメイン名の解析を確認することができます。
1. [ドメイン名サービスコンソール](https://console.cloud.tencent.com/domain)にログインします。
2.「マイドメイン名」管理画面で、ドメイン名解析を確認したいドメイン名の行を選択し、【解析】をクリックして、ドメイン名の解析の詳細を確認します。

<span id="OtherOperations"></span>
### その他の操作

上記の手順は問題を解決できない場合、以下の内容をご参照ください：
- ドメイン名へのpingが通らない場合は、ウェブサイト設定を確認してください。
- パブリックネットワークIPへのpingが通らない場合は、インスタンスに関する情報と双方向のMTRデータ（ローカルからCVMへ、CVMからローカルへ）を添付し、[作業依頼書を提出](https://console.cloud.tencent.com/workorder/category) してエンジニアに連絡してください。
MTRの利用方法については、[サーバーネットワーク遅延とパケットロスの処理](https://intl.cloud.tencent.com/document/product/213/14638) をご参照ください。
