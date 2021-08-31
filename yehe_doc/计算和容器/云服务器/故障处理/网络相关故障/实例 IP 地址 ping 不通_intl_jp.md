## 問題

ローカルホストはインスタンスにpingが通らない場合は、以下のような原因が考えられます。
- ターゲットサーバーの設定が正しくない
- ドメインの名前解決に失敗した
- リンク障害

ローカルネットワークが正常に動作している前提で（他のウェブサイトへのpingが通る）、下記の操作によりトラブルシューティングを実施します。
- [インスタンスはパブリックIPアドレスが設定されているかどうかを確認する](#isConfigurePublicIP)
- [セキュリティグループの設定を確認する](#CheckSecurityGroupSetting)
- [OSの設定を確認する](#CheckOSSetting)
- [その他の操作](#OtherOperations)

## 処理手順

<span id="isConfigurePublicIP"></span>
### インスタンスにパブリックIPアドレスが設定されているかどうかを確認する

>? インスタンスは、パブリックIPアドレスを持っている場合にのみ、Internet上の他のコンピュータと相互接続することができます。パブリックIPアドレスがないと、プライベートIPは外部からインスタンスへのpingが通りません。
>
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2.「インスタンスリスト」画面で、下図に示すように、pingするインスタンスID/インスタンス名を選択して、このインスタンスの詳細画面にに入ります。
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3.「基本情報」欄で、インスタンスにパブリックIPアドレスが設定されているかどうかを確認します。
 - はい、[セキュリティグループの設定を確認](#CheckSecurityGroupSetting)してください。
 - いいえ、[EIPをインスタンスにバインド](https://intl.cloud.tencent.com/document/product/213/16586) してください。

<span id="CheckSecurityGroupSetting"></span>
### セキュリティグループの設定を確認する

セキュリティグループとは、関連するインスタンスのインバウンドトラフィックおよびアウトバウンドトラフィックを制御する仮想ファイアウォールです。セキュリティグループのルールは、プロトコル、ポートおよびポリシーなどを指定することができます。pingはICMPプロトコルを使用するため、インスタンスに関連付けられているセキュリティグループは、ICMPを許可するかどうかをご確認ください。以下の操作を実行して、インスタンスに関連付けられているセキュリティグループ、およびインバウンドルールとアウトバウンドルールの詳細を確認できます。　
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2.「インスタンスリスト」画面で、セキュリティグループ設定を必要とするインスタンスID/インスタンス名を選択して、対象インスタンスの詳細画面に入ります。
3.【セキュリティグループ】タブを選択して、下図に示すように、対象インスタンスのセキュリティグループ管理画面に入ります。
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. インスタンスに関連付けられているセキュリティグループ、およびインバウンドルールとアウトバウンドルールの詳細を確認することにより、ICMPを許可するかどうかを判断します。
 - はい、[OSの設定を確認](#CheckOSSetting) してください。
 - いいえ、ICMPプロトコルポリシーを許可に設定してください。

<span id="CheckOSSetting"></span>
### OSの設定を確認する

インスタンスのOSタイプに基づいてチェック方法を選択します。
- Linux OSの場合は、[Linuxカーネルパラメータおよびファイアウォール設定を確認する](#CheckLinux)。
- Windows OSの場合は、[Windowsファイアウォール設定を確認する](#CheckWindows) 。

<span id="CheckLinux"></span>
#### Linuxのカーネルパラメータおよびファイアウォール設定を確認する

>? Linuxシステムがpingテストが許可されるかどうかは、カーネルとファイアウォール設定の両方により决定されます。いずれかがpingテストを禁止されている場合、「リクエストタイムアウト」が発生します。

##### カーネルパラメータicmp_echo_ignore_allを確認する

1. インスタンスにログインします。
2. 下記のコマンドを実行して、システムのicmp_echo_ignore_all設定を確認します。
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - 0が返された場合は、システムがすべてのICMP Echoリクエストを許可することを示します。この場合、[ファイアウォール設定を確認](#CheckLinuxFirewall) してください。
 - 1が返された場合は、システムがすべてのICMP Echoリクエストを拒否することを示します。この場合、[ステップ3](#Linux_step03) を実行してください。
3. <span id="Linux_step03">下記のコマンドを実行して、icmp_echo_ignore_allカーネルパラメータの設定を変更します。</span>
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all　　
```

<span id="CheckLinuxFirewall"></span>
##### ファイアウォール設定を確認する

下記のコマンドを実行して、現在のサーバーのファイアウォールルールおよび対応するICMPルールが禁止されているかどうかを確認します。
```
iptables -L
```
- 以下のような結果が返された場合は、ICMPルールが禁止されていないことを示します。[ドメイン名がICP登録されたかどうかを確認](#CheckDomainRegistration) してください。
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
- 返された結果は、ICMPルールが禁止されている場合は、下記のコマンドを実行して、対応するルールを有効にします。
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Windows ファイアウォール設定を確認する

1. インスタンスにログインします。
2.【コントロールパネル】を開いて、下図に示すように、【Windows Defender ファイアウォール設定】を選択します。
3.「Windows Defender ファイアウォール」画面で、下図に示すように、【詳細設定】を選択します。
4. 表示された「セキュリティが強化された Windows Defender ファイアウォール」画面で、ICMPに関するアウトバウンドとインバウンドのルールが禁止されているかどうかを確認します。
 - 下図に示すように、ICMPに関するインバウンドルールとアウトバウンドルールが禁止されている場合は、これらのルールを有効にします。


<span id="OtherOperations"></span>
### その他の操作

上記の手順でも問題を解決できない場合、以下の内容をご参照ください。
- ドメイン名へのpingが通らない場合は、ウェブサイトの設定を確認してください。
- パブリックIPへのpingが通らない場合は、インスタンスに関する情報と双方向のMTRデータ（ローカルサーバーからCVMへ、およびCVMからローカルサーバーへ）を添付し、[チケットを提出](https://console.cloud.tencent.com/workorder/category) してエンジニアにお問い合わせください。
MTRの使用方法の詳細については、[サーバーネットワーク遅延とパケットロスの処理](https://intl.cloud.tencent.com/document/product/213/14638) をご参照ください。
