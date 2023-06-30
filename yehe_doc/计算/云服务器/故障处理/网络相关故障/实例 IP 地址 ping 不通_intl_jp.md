## 障害の現象

ローカルホストからインスタンスにpingが通らない場合は、以下のような原因が考えられます：
- ターゲットサーバーの設定が正しくない
- ドメイン名が正しく解析されていない
- リンク障害

ローカルネットワークが正常に動作している前提で（他のウェブサイトへのpingが通る）、下記の操作によりトラブルシューティングを実施します：
- [インスタンスにはパブリックIPアドレスが設定されているかを確認](#isConfigurePublicIP)
- [セキュリティグループの設定を確認](#CheckSecurityGroupSetting)
- [システム設定を確認](#CheckOSSetting)
- [その他の操作](#OtherOperations)

## 実施手順


- インスタンスにはパブリックIPアドレスが設定されているかを確認します[](id:isConfigurePublicIP)

<dx-alert infotype="explain" title="">
インスタンスにパブリックIPアドレスが設定されている場合のみ、Internet上の他のコンピュータと通信できます。インスタンスにパブリックIPアドレスが設定されていない場合、プライベートIPアドレスでは外部からインスタンスへのpingが通りません。
</dx-alert>


1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2.「インスタンスリスト」画面で、下図に示すように、pingを実行したいインスタンスID/インスタンス名を選択し、下図にしめされているように、そのインスタンスの詳細画面に入ります：
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3.「ネットワーク情報」欄で、インスタンスにパブリックIPアドレスが設定されているかを確認します。
   - 設定されている場合、[セキュリティグループの設定を確認](#CheckSecurityGroupSetting)してください。
   - 設定されていない場合、[EIPでクラウドリソースをバインディング](https://intl.cloud.tencent.com/document/product/213/16586)してください。


### セキュリティグループの設定を確認します[](id:CheckSecurityGroupSetting)

セキュリティグループは仮想ファイアウォールであり、関連付けられているインスタンスのインバウンドトラフィックとアウトバウンドトラフィックを制御することができます。セキュリティグループのルールでは、プロトコル、ポート、ポリシーなどを指定することができます。pingはICMPプロトコルを使用するため、インスタンスと関連を付けたセキュリティグループではICMPを許可しているかを確認する必要があります。以下の操作を実施し、インスタンスで使用されているセキュリティグループ、およびインバウンドルールとアウトバウンドルールの詳細を確認してください。
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2.「インスタンスリスト」画面で、セキュリティグループを設定するインスタンスのID/インスタンス名を選択して、そのインスタンスの詳細画面に入ります。
3.**セキュリティグループ**タブを選択し、下図に示すように、対象インスタンスのセキュリティグループ管理画面に入ります。
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. インスタンスで使用されているセキュリティグループ、およびインバウンドルールとアウトバウンドルールの詳細を確認することにより、インスタンスと関連を付けたセキュリティグループではICMPを許可しているかを判断します。
   - 許可している場合、[システム設定を確認](#CheckOSSetting)してください。
   - 許可しない場合、ICMPプロトコルのポリシーを許可するように設定してください。


### [システム設定を確認します[](id:CheckOSSetting)

インスタンスのOSタイプを判断して、確認方法を選択します。
- Linux OSの場合、[Linuxカーネルのパラメータとファイアウォールの設定を確認](#CheckLinux)してください。
- Windows OSの場合、[Windowsのファイアウォールの設定を確認](#CheckWindows)してください。ファイアウォールに問題がなければ、[Windowsのネットワーク設定をリセット](#reset)してください。


#### Linuxカーネルのパラメータとファイアウォールの設定を確認します[](id:CheckLinux)

<dx-alert infotype="explain" title="">
Linux OSではpingが許可されるかは、カーネルとファイアウォールの両方の設定によります。いずれかが禁止されている場合、pingパケットが「Request timeout」になります。
</dx-alert>

##### カーネルパラメータicmp_echo_ignore_allを確認します

1. VNCでインスタンスにログインします。詳しくは以下をご参照ください。
   - [VNCによるLinuxインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/32494)。
   - [VNCによるWindowsインスタンスへのログイン](https://intl.cloud.tencent.com/document/product/213/32496)
2. 下記のコマンドを実行し、システムのicmp_echo_ignore_allの設定を確認します。
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
   - 0が返された場合、システムではすべてのICMP Echoリクエストが許可されるため、[ファイアウォールの設定を確認](#CheckLinuxFirewall) してください。
   - 1が返された場合、システムではすべてのICMP Echoリクエストが拒否されるため、[手順3](#Linux_step03) を実施してください。

3. [](id:Linux_step03)下記のコマンドを実行し、カーネルパラメータicmp_echo_ignore_allの設定を変更します。
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all　　
```


##### ファイアウォールの設定を確認します[](id:CheckLinuxFirewall)

下記のコマンドを実行して、現在のサーバーのファイアウォールルールおよび該当するICMPルールが禁止されているかを確認します。
```
iptables -L
```
- 以下が返された場合、該当するICMPルールが禁止されていません。
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
- 返された結果は、ICMPに対応するルールが禁止されている場合は、下記のコマンドを実行して、対応するルールを有効にします。
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```


#### Windowsファイアウォールの設定を確認します[](id:CheckWindows)

1. インスタンスにログインします。
2. **コントロールパネル**を起動し、**Windows Defender ファイアウォールの設定**を選択します。
3.「Windows Defender ファイアウォール」画面で、**高度な設定**を選択します。
4. 表示された「セキュリティが強化されたWindows Defender ファイアウォール」ウィンドウで、ICMPに関するアウトバウンドとインバウンドのルールが禁止されているかを確認します。
   - 下図に示すように、ICMPに関するアウトバウンドとインバウンドのルールが無効になっている場合は、ルールを有効にしてください。

### Windowsのネットワーク設定をリセットします

1. ご利用のVPCネットワークではDHCPがサポートされているかを確認してください（2018年6月以降に作成したVPCネットワークの場合、DHCPがサポートされています）。サポートされていない場合、ネットワーク設定における静的IPが正しいかを確認してください。
2. DHCPがサポートされている場合、DHCPに割り当てられたプライベートネットワークIPが正しいかを確認してください。正しくない場合、公式サイトのログイン機能（VNCでログイン）を使用し管理者としてPowerShellを起動し、DHCPコンポーネントがIPを再取得するように、`ipconfig /release`と`ipconfig/renew`（マシンを再起動する必要はありません）を実行してみてください。
3. DHCPに割り当てられたプライベートネットワークIPが正しいが、依然としてpingが通らない場合、スタートメニューから【ファイル名を指定して実行】を起動し、` ncpa.cpl `を入力して[OK]をクリックします。ローカル接続を起動し、LANカードを無効にしてから有効にします。
4. 上記の方法を試しても問題を解決できない場合は、管理者としてCMDで以下のコマンドを実行してマシンを再起動します。
```plantext
reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles"  /f
```

### その他の操作[](id:OtherOperations)

上記の方法を試しても問題を解決できない場合、以下の内容をご参照ください。
- ドメイン名へのpingが通らない場合は、ウェブサイトの設定を確認してください。
- パブリックネットワークIPへのpingが通らない場合は、インスタンスの情報と双方向のMTRデータ（ローカルからCVMへ、CVMからローカルへ）を添付し、[チケットを提出](https://console.cloud.tencent.com/workorder/category) してエンジニアに連絡してください。
MTRの利用方法については、[サーバーネットワーク遅延とパケットロスの処理](https://intl.cloud.tencent.com/document/product/213/14638) をご参照ください。


