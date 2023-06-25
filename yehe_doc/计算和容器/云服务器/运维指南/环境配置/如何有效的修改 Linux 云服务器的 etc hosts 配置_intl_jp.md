## ユースケース

2018年3月1日以降、Tencent Cloudの公式サイトにより提供するLinuxパブリックイメージには、オープンソースツールCloud-Initがプリインストールされており、インスタンス上のすべての初期化操作は Cloud-Init 経由で行われるため、インスタンス内の操作がより透過的になります。詳細については、[Cloud-Init](https://intl.cloud.tencent.com/document/product/213/19670)をご参照ください。
Cloud-Init は**毎回起動**する時に `/etc/cloud/templates/hosts.${os_type}.tmpl` テンプレートに基づいて新しいファイル `/etc/hosts` を生成し、インスタンスの元の `/etc/hosts` ファイルを上書きします。 したがって、ユーザーがインスタンス内部に `/etc/hosts` 構成を手動で変更してインスタンスを再起動すると、 `/etc/hosts` 構成が元のデフォルト構成に戻ることになりました。

## 前提条件
Tencent Cloudは、Cloud-Init の上書き操作を最適化しました。**2018年9月以降にパブリックイメージを使用して**作成されたインスタンスは、再起動後に `/etc/hosts` 構成が上書きされなくなりました。
**2018 年 9 月より前に**作成されたインスタンスの場合は、次の手順に従って変更します。

## 操作手順

### ソリューション1
1.Linux CVMにログインします。
2. 次のコマンドを実行して、 `/etc/cloud/cloud.cfg` 構成ファイル中の `- update_etc_hosts` を `- ['update-etc-hosts', 'once-per-instance']`に変更します。
```shellsession
sed -i "/update_etc_hosts/c \ - ['update_etc_hosts', 'once-per-instance']" /etc/cloud/cloud.cfg
```
3. 次のコマンドを実行して、 `/var/lib/cloud/instance/sem/`パスの下にconfig_update_etc_hostsファイルを作成します。
```shellsession
touch /var/lib/cloud/instance/sem/config_update_etc_hosts
```

### ソリューション2


<dx-alert infotype="explain" title="">
このソリューションでは、CentOS7.2 OSを例として説明します。
</dx-alert>


#### hostsテンプレートファイルのパスを取得する
1. Linux CVMにログインします。
2. 次のコマンドを実行して、システムホストテンプレートファイルを確認します。
```shellsession
cat /etc/hosts
```
hosts テンプレート ファイルは次の図に示すとおりです：
![](https://main.qcloudimg.com/raw/f51f9c53004574f72d32f5ed790c8563.png)


#### hosts テンプレートファイルを変更する


<dx-alert infotype="explain" title="">
127.0.0.1 test test の追加を例として、必要に応じて、hostsテンプレートファイルおよび/etc/hosts ファイルを変更します。
</dx-alert>


1. 次のコマンドを実行して、 hosts テンプレートファイルを変更します。
```shellsession
vim /etc/cloud/templates/hosts.redhat.tmpl
```
2. 「**i** 」を押して、編集モードに切り替えます。
3. ファイルの最後に次の内容を入力します。
```shellsession
127.0.0.1 test test
```
4. 入力が完了したら、**Esc**キーを押して、「**:wq**」と入力し、ファイルを保存して戻ります。

#### /etc/hosts ファイルを変更する
1. 次のコマンドを実行して、 `/etc/hosts`ファイルを変更します。
```shellsession
vim /etc/hosts
```
2.  **i**を押して、編集モードに切り替えます。
3. ファイルの最後に次の内容を入力します。
```shellsession
127.0.0.1 test test
```
4. 入力が完了したら、**Esc**キーを押して、「**:wq**」と入力し、ファイルを保存して戻ります。