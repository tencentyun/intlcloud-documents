## ユースケース

2018年3月1日以降、Tencent Cloudの公式サイトにより提供したパブリックLinuxイメージには、純粋なオープンソースツールCloud-Initを事前にインストールして、Cloud-Initを介してインスタンスのすべての初期化操作を実現しました。インスタンス全体の操作がより透明になりました。 詳細については、[Cloud-Init]をご参照ください。
Cloud-Init は**毎回起動する時に**`/etc/cloud/templates/hosts.${os_type}.tmpl` テンプレートに基づいて新しいファイル`/etc/hosts`を生成し、インスタンスの元の `/etc/hosts` ファイルを上書きすることにより、ユーザーがインスタンス内の`/etc/hosts` を手動で修正してインスタンスをリスタートした後、`/etc/hosts` が元のデフォルト設定に戻ることになりました。

## 前提条件
Tencent Cloudは、Cloud-Init の上書き操作を改善しました。**2018年9月以降**に作成されたインスタンスには、リスタート後に `/etc/hosts` 設定が上書きされる問題がなくなりました。
インスタンスが**2018年9月前**に作成された場合、以下の解決方法で修正してください。

## 操作手順

### 解決案1 
1.  Linux CVMにログインします。
2. 次のコマンドを実行して、 `/etc/cloud/cloud.cfg` 設定ファイルの `- update_etc_hosts` を`- ['update-etc-hosts', 'once-per-instance']`に修正します。
```
sed -i "/update_etc_hosts/c \ - ['update_etc_hosts', 'once-per-instance']" /etc/cloud/cloud.cfg
```
3. 次のコマンドを実行して、  `/var/lib/cloud/instance/sem/` ディレクトリに `config_update_etc_hosts` ファイルを作成します。
```
touch /var/lib/cloud/instance/sem/config_update_etc_hosts
```

### 解決案2
>?この解決案では、CentOS7.2 OSを例とします。
>
#### hostsテンプレートファイルのパスを取得する
1.  Linux CVMにログインします。
2. 次のコマンドを実行して、システムhostsテンプレートファイルを確認します。
```
cat /etc/hosts
```
hosts テンプレートファイルを下記画像に示すように：
![](https://main.qcloudimg.com/raw/f51f9c53004574f72d32f5ed790c8563.png)


####  hosts テンプレートファイルを修正する
>?127.0.0.1 test test の追加を例として、必要に応じて、hostsテンプレートファイルおよび/etc/hosts ファイルを修正します。
>
1. 次のコマンドを実行して、 hosts テンプレートファイルを修正します。
```
vim /etc/cloud/templates/hosts.redhat.tmpl
```
2. 「**i**」或は「**Insert**」を押して、編集モードに切り替えます。
3. ファイルの最後に次の内容を入力します。
```
127.0.0.1 test test
```
4. 入力が完了したら、「**Esc**」を押し、「**:wq**」を入力して、ファイルを保存して戻ります。

####  /etc/hosts ファイルを修正する
1. 次のコマンドを実行して、  `/etc/hosts` ファイルを修正します。
```
vim /etc/hosts
```
2. 「**i**」或は「**Insert**」を押して、編集モードに切り替えます。
3. ファイルの最後に次の内容を入力します。
```
127.0.0.1 test test
```
4. 入力が完了したら、「**Esc**」を押し、「**:wq**」を入力して、ファイルを保存して戻ります。
