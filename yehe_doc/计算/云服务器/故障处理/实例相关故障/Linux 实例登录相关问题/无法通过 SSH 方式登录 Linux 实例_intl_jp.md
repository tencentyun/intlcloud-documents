>?
>- この文章はコミュニティから寄せられたものであり、参考までにご提供します。Tencent Cloud関連製品とは関係がありません。
>- ここに記載された関連のファイル操作は、必ず慎重に実行してください。必要に応じて、スナップショット作成などの方法でデータバックアップを行うことができます。
> 

## 現象の説明
[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501)を行った際、「接続できません」または「接続に失敗しました」と表示され、Linuxインスタンスに正常にログインできません。

## 問題の特定および処理[](id:ProcessingSteps)
SSHを使用したLinuxインスタンスへのログインが失敗し、エラー情報が返された場合は、エラー情報を記録し、次のよくあるエラー情報から当てはまるものを探し、迅速に問題を特定して、手順を参照し解決することができます。

<dx-accordion>
::: SSHログインエラーUser root not allowed because not listed in AllowUsers

#### 問題の原因[](id:userNotListAllowUsers)
この問題は通常、SSHサービスがユーザーログイン制御パラメータをアクティブにし、ログインユーザーを制限しているために起こります。パラメータの説明は次のとおりです。
- **AllowUsers**：ログインが許可されているユーザーのホワイトリストであり、このパラメータが記述されているユーザーのみログインできます。
- **DenyUsers**：ログインが拒否されているユーザーのブラックリストであり、このパラメータが記述されているユーザーはすべてログインが拒否されます。
- **AllowGroups**：ログインが許可されているユーザーグループのホワイトリストであり、このパラメータが記述されているユーザーグループのみログインできます。
- **DenyGroups**：ログインが拒否されているユーザーグループのブラックリストであり、このパラメータが記述されているユーザーグループはすべてログインが拒否されます。

<dx-alert infotype="explain" title="">
拒否ポリシーの優先順位は許可ポリシーより上になります。
</dx-alert>


#### 解決方法
1. [処理手順](#ProcessingSteps1)を参照し、SSHで設定した`sshd_config`ファイルに進み、 設定を確認します。
2. ユーザーログイン制御パラメータを削除し、SSHサービスを再起動すれば完了です。


#### 処理手順[](id:ProcessingSteps1)
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. 以下のコマンドを実行し、VIMエディタを使用して`sshd_config`設定ファイルに進みます。
```shell
vim /etc/ssh/sshd_config
```
3. **i**を押して編集モードに入り、以下の設定を探して削除するか、または各行の先頭に`#`を追加してコメントします。
```shell
AllowUsers root test
DenyUsers test
DenyGroups test
AllowGroups root
```
4. **Esc**を押して編集モードを終了し、**:wq**を入力して変更を保存します。
5. 実際に使用するOSに応じて以下のコマンドを実行し、SSHサービスを再起動します。
  - CentOS
```shell
systemctl restart sshd.service
```
  - Ubuntu
```shell
service sshd restart
```

SSHサービスを再起動すると、SSHを使用してログインできるようになります。詳細については<a href="https://intl.cloud.tencent.com/document/product/213/32501">SSHを使用してLinuxインスタンスにログイン</a>をご参照ください。


::: 
::: SSHログインエラーDisconnected:No supported authentication methods available

#### 現象の説明[](id:noSupportesAuthentication)
SSHを使用してログインする際に、次のエラー情報が表示されます。
```
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
sshd[10826]: Connection closed by xxx.xxx.xxx.xxx.
Disconnected:No supported authentication methods available.
```

#### 問題の原因
SSHサービスによって`PasswordAuthentication`パラメータが変更され、パスワード認証ログインが無効になったことが原因です。


#### 解決方法
1. [処理手順](#ProcessingSteps2)を参照し、SSHで設定した`sshd_config`ファイルに進みます。
2. `PasswordAuthentication`パラメータを変更し、SSHサービスを再起動すれば完了です。


#### 処理手順[](id:ProcessingSteps2)
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. 以下のコマンドを実行し、VIMエディタを使用して`sshd_config`設定ファイルに進みます。
```shell
vim /etc/ssh/sshd_config
```
3. ** i **を押して編集モードに入り、`PasswordAuthentication no`を`PasswordAuthentication yes`に変更します。
4. **Esc**を押して編集モードを終了し、**:wq**を入力して変更を保存します。
5. 実際に使用するOSに応じて以下のコマンドを実行し、SSHサービスを再起動します。
  - CentOS
```shell
systemctl restart sshd.service
```
  - Ubuntu
```shell
service sshd restart
```
SSHサービスを再起動すると、SSHを使用してログインできるようになります。詳細については<a href="https://intl.cloud.tencent.com/document/product/213/32501">SSHを使用してLinuxインスタンスにログイン</a>をご参照ください。

:::
::: SSHログインエラーssh_exchange_identification: read: Connection reset by peer

#### 現象の説明[](id:connectionResetByPeer)
SSHを使用してログインする際に、エラー情報「ssh_exchange_identification: read: Connection reset by peer」が表示されます。もしくは次のエラー情報が表示されます。
- "ssh_exchange_identification: Connection closed by remote host"
- "kex_exchange_identification: read: Connection reset by peer"
- "kex_exchange_identification: Connection closed by remote host"


#### 問題の原因
このタイプの問題が発生する原因は多くありますが、よくある原因は次の数種類です。
- ローカルアクセス制御によって接続が制限されている
- Fail2banやdenyhostなど、何らかの侵入防止ソフトウェアによってファイアウォールルールが変更された
- sshd設定で最大接続数が制限されている
- ローカルネットワークに問題がある


#### 解決方法
[処理手順](#ProcessingSteps3)を参照し、アクセスポリシー、ファイアウォールルール、sshd設定、ネットワーク環境などいくつかの面から問題を特定し、解決します。



#### 処理手順[](id:ProcessingSteps3)


#### アクセスポリシー設定の確認と調整
Linuxでは`/etc/hosts.allow`および`/etc/hosts.deny`ファイルによってアクセスポリシーを設定することができ、2つのファイルはそれぞれ許可ポリシーと拒否ポリシーに対応しています。例えば、`hosts.allow`ファイルでホスト信頼ルールを設定し、`hosts.deny`ファイルでその他のすべてのホストを拒否することができます。`hosts.deny`を例にとると、拒否ポリシーの設定は次のようになります。
```
in.sshd:ALL			# すべてのssh接続を拒否
in.sshd:218.64.87.0/255.255.255.128	# 218.64.87.0—-127のsshを拒否
ALL:ALL				# すべてのTCP接続を拒否
```


[VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)し、`/etc/hosts.deny`ファイルおよび`/etc/hosts.allow`ファイルを確認し、確認結果に基づいて次の処理方法を選択してください。
 - 設定に誤りがあった場合は必要に応じて変更してください。変更後すぐに有効になります。
 - 未設定、または設定に誤りがなかった場合は、次の手順に進んでください。

<dx-alert infotype="explain" title="">
アクセスポリシーを設定していない場合、デフォルトのファイルはすべてブランクであり、すべての接続が許可されています。
</dx-alert>




#### iptablesファイアウォールルールの確認
Fail2banやdenyhostなど、何らかの侵入防止ソフトウェアの使用を含めて、iptablesファイアウォールルールが変更されたかどうかを確認します。以下のコマンドを実行して、ファイアウォールがSSH接続を拒否したことがあるかどうかを確認します。
```
sudo iptables -L --line-number
```
 - SSH接続が拒否されていた場合は、対応するソフトウェアのホワイトリストなどの関連ポリシーによって、ご自身で設定を行ってください。
 - SSH接続が拒否されていなかった場合は、次の手順に進んでください。


#### sshd設定の確認と調整
1. 以下のコマンドを実行し、VIMエディタを使用して`sshd_config`に進み、ファイルを設定します。
```
vim /etc/ssh/sshd_config
```
2. `MaxStartups`の値を調整する必要があるかどうかを確認します。`sshd_config`設定ファイル内の`MaxStartups`によって許可する最大接続数を設定します。短時間に多くの接続を確立したい場合は、この値を適宜調整する必要があります。
 - 調整が必要な場合は、以下の手順を参照して変更してください。
    1. ** i **を押して編集モードに入り、変更完了後に**Esc**を押して編集モードを終了し、**:wq**を入力して変更を保存します。
<dx-alert infotype="explain" title="">
MaxStartupsは10:30:100がデフォルト設定であり、SSH保護プロセスの、アイデンティティ認証を経ない同時接続の最大数を指定します。10:30:100とは、10番目の接続以降、接続数が100に達するまで、30%の確率（漸増）で新たな接続を拒否することを表します。
</dx-alert>
    2. 以下のコマンドを実行し、sshdサービスを再起動します。
```
service sshd restart
```
 - 調整の必要がない場合は、次の手順に進んでください。


### ネットワーク環境のテスト
1. [プライベートIPアドレス](https://intl.cloud.tencent.com/document/product/213/5225)を使用してログインしているかどうかを確認します。
  - 「はい」の場合は、[パブリックIP](https://intl.cloud.tencent.com/document/product/213/5224)に切り替えてから再度試してください。
  - 「いいえ」の場合は、次の手順に進んでください。
2. 他のネットワーク環境を使用して、正常に接続されるかをテストします。
  - 「はい」の場合は、インスタンスを再起動後にVNCを使用してインスタンスにログインしてください。
  - 「いいえ」の場合は、テスト結果に基づいてネットワーク環境の問題を解決してください。


ここまででSSHログインの問題が解決されていない場合は、システムカーネルに異常が生じているか、またはその他の潜在的な原因による可能性があります。問題の処理を進めるため、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してご連絡ください。
:::
::: SSHログインエラーPermission denied, please try again

#### 現象の説明[](id:permissionDenied)
rootユーザーがSSHを使用してLinuxインスタンスにログインする際、エラー情報「Permission denied, please try again」が表示されます。


#### 問題の原因
システムによってSELinuxサービスがアクティブ化されたか、またはSSH サービスによって`PermitRootLogin`設定が変更されたことによるものです。


#### 解決方法
[処理手順](#ProcessingSteps4)を参照し、SELinuxサービスおよびSSH設定ファイル`sshd_config`の`PermitRootLogin`パラメータを確認し、問題の原因を確認して問題を解決します。

#### 処理手順[](id:ProcessingSteps4)


#### SELinuxサービスの確認と無効化
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. 以下のコマンドを実行し、現在のSELinuxのサービスステータスを確認します。
```
/usr/sbin/sestatus -v 
```
返されたパラメータが`enabled`であれば有効な状態であり、`disabled`であれば無効な状態です。有効な状態であれば次のように表示されます。
```
SELinux status:       enabled
```
3. 実際の状況に応じて、SELinuxサービスを一時的または永続的に無効化します。
  - SELinuxサービスを一時的に無効化
以下のコマンドを実行し、SELinuxサービスを一時的に無効化します。変更はリアルタイムに有効となり、システムまたはインスタンスを再起動する必要はありません。
```
setenforce 0
```
  - SELinuxサービスを永続的に無効化
以下のコマンドを実行し、SELinuxサービスを無効化します。
```
sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
```
<dx-alert infotype="notice" title="">
- このコマンドはSELinuxサービスがenforcing状態の場合にのみ適用されます。
- コマンド実行後にシステムまたはインスタンスを再起動し、変更を有効にする必要があります。
</dx-alert>


#### sshd設定の確認と調整
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. 以下のコマンドを実行し、VIMエディタを使用して`sshd_config`設定ファイルに進みます。
```shell
vim /etc/ssh/sshd_config
```
3. ** i **を押して編集モードに入り、`PermitRootLogin no`を`PermitRootLogin yes`に変更します。
>?
>- `sshd_config`でこのパラメータが設定されていない場合、rootユーザーログインがデフォルトで許可されます。
>- このパラメータはrootユーザーがSSHを使用してログインする場合にのみ影響し、rootユーザーがその他の方法でインスタンスにログインする場合には影響しません。
>
4. **Esc**を押して編集モードを終了し、**:wq**を入力して変更を保存します。
5. 以下のコマンドを実行して、SSHサービスを再起動します。
```shell
service sshd restart
```
SSHサービスを再起動すると、SSHを使用してログインできるようになります。詳細については<a href="https://intl.cloud.tencent.com/document/product/213/32501">SSHを使用してLinuxインスタンスにログイン</a>をご参照ください。
:::
::: SSHログイン時エラーToo many authentication failures for root

#### 現象の説明[](id:tooManyFailures)
SSHを使用してログインする際、ログイン時にパスワードを複数回入力すると、エラー情報「Too many authentication failures for root」が返され、接続が中断されます。

#### 問題の原因
間違ったパスワードを複数回連続して入力し、SSHサービスのパスワードリセットポリシーをトリガーしたことが原因です。


#### 解決方法
1. [処理手順](#ProcessingSteps5)を参照し、SSHで設定した`sshd_config`ファイルに進みます。
2. SSHサービスのパスワードリセットポリシーの`MaxAuthTries`パラメータ設定を確認して変更し、SSHサービスを再起動すれば完了です。


#### 処理手順[](id:ProcessingSteps5)
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. 以下のコマンドを実行し、VIMエディタを使用して`sshd_config`設定ファイルに進みます。
```shell
vim /etc/ssh/sshd_config
```
3. 以下に類似した設定が含まれていないか確認します。
```
MaxAuthTries 5
```
<dx-alert infotype="explain" title="">
- このパラメータはデフォルトではアクティブになっておらず、ユーザーが毎回SSHを使用してログインする際に、間違ったパスワードを連続して入力できる回数を制限するために用いられます。設定した回数を超えるとSSH接続が切断され、関連のエラー情報が表示されます。ただし、関連のアカウントはロックされず、SSHログインを再び使用することができます。
- 実際の状況に応じて、設定を変更するかどうかを決定してください。変更が必要な場合は`sshd_config`設定ファイルのバックアップを作成しておくことをお勧めします。
</dx-alert>
4. **i**を押して編集モードに入り、以下の設定を変更するか、または行の先頭に`#`を追加してコメントします。
```
MaxAuthTries <間違ったパスワードの入力を許可する回数>
```
5. **Esc**を押して編集モードを終了し、**:wq**を入力して変更を保存します。
6. 以下のコマンドを実行し、SSHサービスを再起動します。
```shell
service sshd restart
```
SSHサービスを再起動すると、SSHを使用してログインできるようになります。詳細については<a href="https://intl.cloud.tencent.com/document/product/213/32501">SSHを使用してLinuxインスタンスにログイン</a>をご参照ください。

:::
::: SSH起動時エラーerror while loading shared libraries

#### 現象の説明[](id:errorLibraries)
LinuxインスタンスがSSHサービスを起動すると、以下に類似したエラー情報がsecureログファイル内に表示されるか、または直接返されます。
- "error while loading shared libraries:  libcrypto.so.10: cannot open shared object file: No such file or directory"
- "PAM unable to dlopen(/usr/lib64/security/pam_tally.so): /usr/lib64/security/pam_tally.so: cannot open shared object file: No such file or directory"


#### 問題の原因
SSHサービスの稼働が依存する関連のシステムライブラリファイルが失われたか、または権限設定などの異常によるものです。


#### 解決方法
[処理手順](#ProcessingSteps6)を参照して、システムライブラリファイルを確認し、修復を行います。



#### 処理手順[](id:ProcessingSteps6)
<dx-alert infotype="explain" title="">
ここではlibcrypto.so.10ライブラリファイルの異常処理を例にとりますが、その他のライブラリファイル異常の処理方法もこれに類似しています。実際の状況に応じて操作を行ってください。
</dx-alert>



#### ライブラリファイル情報を取得する
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. 以下のコマンドを実行し、libcrypto.so.10ライブラリファイル情報を確認します。
```
ll /usr/lib64/libcrypto.so.10
```
以下に類似した情報が返された場合、`/usr/lib64/libcrypto.so.10`は`libcrypto.so.1.0.2k`ライブラリファイルのソフトリンクであることを表します。
```
lrwxrwxrwx 1 root root 19 Jan 19  2021 /usr/lib64/libcrypto.so.10 -> libcrypto.so.1.0.2k
```
2. 以下のコマンドを実行し、`libcrypto.so.1.0.2k`ライブラリファイル情報を確認します。
```
ll /usr/lib64/libcrypto.so.1.0.2k
```
以下に類似した情報が返されます。
```
-rwxr-xr-x 1 root root 2520768 Dec 17  2020 /usr/lib64/libcrypto.so.1.0.2k
```
3. 正常なライブラリファイルのパス、権限、グループなどの情報を記録し、以下の方法で処理を行います。
	 - [ライブラリファイルの検索と置換](#findAndReplace)
	 - [外部ファイルのアップロード](#fileUpload)
	 - [スナップショットロールバックによるリカバリ](#snapshotRollback)



#### ライブラリファイルの検索と置換[](id:findAndReplace)
1. 以下のコマンドを実行し、`libcrypto.so.1.0.2k`ファイルを検索します。
```
find / -name libcrypto.so.1.0.2k
```
2. 返された結果に基づいて以下のコマンドを実行し、ライブラリファイルを正常なディレクトリにコピーします。
```
cp <手順1で取得したライブラリファイルの絶対パス> /usr/lib64/libcrypto.so.1.0.2k
```
3.以下のコマンドを順に実行し、ファイルの権限、所有者、グループを変更します。
```
chmod 755 /usr/lib64/libcrypto.so.1.0.2k
```
```
chown root:root /usr/lib64/libcrypto.so.1.0.2k
```
4. 以下のコマンドを実行し、ソフトリンクを作成します。
```
ln -s /usr/lib64/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.10
```
5. 以下のコマンドを実行し、SSHサービスを起動します。
```
service sshd start
```


#### 外部ファイルのアップロード[](id:fileUpload)
1. FTPソフトウェアにより、他の正常なサーバー上の`libcrypto.so.1.0.2k`のライブラリファイルを、目的のサーバーの`\tmp`ディレクトリにアップロードします。
<dx-alert infotype="explain" title="">
ここでは目的のサーバーの`\tmp`ディレクトリへのアップロードを例にとりますが、実際の状況に応じて変更することができます。
</dx-alert>
2. 以下のコマンドを実行し、ライブラリファイルを正常なディレクトリにコピーします。
```
cp /tmp/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.1.0.2k
```
3.以下のコマンドを順に実行し、ファイルの権限、所有者、グループを変更します。
```
chmod 755 /usr/lib64/libcrypto.so.1.0.2k
```
```
chown root:root /usr/lib64/libcrypto.so.1.0.2k
```
4. 以下のコマンドを実行し、ソフトリンクを作成します。
```
ln -s /usr/lib64/libcrypto.so.1.0.2k /usr/lib64/libcrypto.so.10
```
5. 以下のコマンドを実行し、SSHサービスを起動します。
```
service sshd start
```


#### スナップショットロールバックによるリカバリ[](id:snapshotRollback)
インスタンスシステムディスクの過去のスナップショットをロールバックすることで、ライブラリファイルをリカバリすることができます。詳細については、[スナップショットからのデータロールバック](https://intl.cloud.tencent.com/document/product/362/5756)をご参照ください。

<dx-alert infotype="notice" title="">
- スナップショットロールバックを行うと、スナップショット作成後のデータが失われる場合がありますので、慎重に操作してください。
- SSHサービスが正常に稼働するまで、スナップショット作成時間の近い方から遠い方の順に、一度ずつロールバックを試すことをお勧めします。ロールバックを行ってもSSHサービスが正常に稼働しない場合は、それらの時点でシステムにすでに異常が生じていたことを意味します。
</dx-alert>

:::
::: SSHサービス起動時エラー fatal: Cannot bind any address
#### 現象の説明[](id:cannotBindAddress)
LinuxインスタンスがSSHサービスを起動すると、以下に類似したエラー情報がsecureログファイル内に表示されるか、または直接返されます。
```
FAILED.
fatal: Cannot bind any address.
address family must be specified before ListenAddress.
```


#### 問題の原因
SSHサービスの`AddressFamily`パラメータ設定が不適切なことによるものです。`AddressFamily`パラメータは運用時に使用するプロトコルスイートの指定に用いられます。パラメータがIPv6のみを設定し、一方でシステム内ではIPv6がアクティブになっていない、またはIPv6の設定が無効になっている場合、この問題が起こる可能性があります。


#### 解決方法
1. [処理手順](#ProcessingSteps7)を参照して、SSHで設定した`sshd_config`ファイルに進み、 設定を確認します。
2. `AddressFamily`パラメータを変更し、SSHサービスを再起動すれば完了です。



#### 処理手順[](id:ProcessingSteps7)
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. 以下のコマンドを実行し、VIMエディタを使用して`sshd_config`設定ファイルに進みます。
```
vim /etc/ssh/sshd_config
```
3. 以下に類似した設定が含まれていないか確認します。
```
AddressFamily inet6
​``` よく用いられるパラメータの説明は次のとおりです。
 - **inet**：IPv4プロトコルスイートを使用します。デフォルト値です。
 - **inet6**：IPv6プロトコルスイートを使用します。
 - **any**：IPv4およびIPv6プロトコルスイートを同時にアクティブにします。
4. **i**を押して編集モードに入り、次の設定に変更するか、または行の先頭に`#`を追加してコメントします。 
```
AddressFamily inet
```
<dx-alert infotype="notice" title="">
`AddressFamily`パラメータは`ListenAddress`より前に設定しなければ有効になりません。
</dx-alert>
5. **Esc**を押して編集モードを終了し、**:wq**を入力して変更を保存します。
6. 以下のコマンドを実行し、SSHサービスを再起動します。
```shell
service sshd restart
```
SSHサービスを再起動すると、SSHを使用してログインできるようになります。詳細については<a href="https://intl.cloud.tencent.com/document/product/213/32501">SSHを使用してLinuxインスタンスにログイン</a>をご参照ください。

:::
::: SSHサービス起動時エラー Bad configuration options

#### 現象の説明[](id:badConfigureOptions)
LinuxインスタンスがSSHサービスを起動すると、以下に類似したエラー情報がsecureログファイル内に表示されるか、または直接返されます。
```
/etc/ssh/sshd_config: line 2: Bad configuration options:\\ 
/etc/ssh/sshd_config: terminating, 1 bad configuration options
```


#### 問題の説明
設定ファイルにファイルコードまたは設定エラーなどの異常が存在することによるものです。


#### 解決方法
処理手順で提示される以下の処理項目を参照し、sshd_config`設定ファイルを修復します。
- [エラー情報に対応した設定ファイル変更](#changeSetting)
- [外部ファイルのアップロード](#upload)
- [SSHサービスの再インストール](#installSSH)
- [スナップショットロールバックによるリカバリ](#rollBack)


#### 処理手順


#### エラー情報に対応した設定ファイル変更[](id:changeSetting)
エラー情報の中でエラーのある設定が明確に示されている場合は、VIMエディタによって`/etc/ssh/sshd_config`設定ファイルを直接変更することができます。他のインスタンスの正しい設定ファイルを参照し、変更を行うことができます。


#### 外部ファイルのアップロード[](id:upload)
1. FTPソフトウェアにより、他の正常なサーバー上の`/etc/ssh/sshd_config` のライブラリファイルを、目的のサーバーの`\tmp`ディレクトリにアップロードします。
<dx-alert infotype="explain" title="">
ここでは目的のサーバーの`\tmp`ディレクトリへのアップロードを例にとりますが、実際の状況に応じて変更することができます。
</dx-alert>
2. 以下のコマンドを実行し、ライブラリファイルを正常なディレクトリにコピーします。
```
cp /tmp/sshd_config /etc/ssh/sshd_config
```
3.以下のコマンドを順に実行し、ファイルの権限、所有者、グループを変更します。
```
chmod 600 /etc/ssh/sshd_config
``` ```
chown root:root /etc/ssh/sshd_config
```
4. 以下のコマンドを実行し、SSHサービスを起動します。
```
service sshd start
```


#### SSHサービスの再インストール[](id:installSSH)
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. 以下のコマンドを実行し、SSHサービスをアンインストールします。
```
rpm -e openssh-server
```
3. 以下のコマンドを実行し、SSHサービスをインストールします。
```
yum install openssh-server
```
4. 以下のコマンドを実行し、SSHサービスを起動します。
```
service sshd start
```

#### スナップショットロールバックによるリカバリ[](id:rollBack)
インスタンスシステムディスクの過去のスナップショットをロールバックすることで、ライブラリファイルをリカバリすることができます。詳細については、[スナップショットからのデータロールバック](https://intl.cloud.tencent.com/document/product/362/5756)をご参照ください。

<dx-alert infotype="notice" title="">
- スナップショットロールバックを行うと、スナップショット作成後のデータが失われる場合がありますので、慎重に操作してください。
- SSHサービスが正常に稼働するまで、スナップショット作成時間の近い方から遠い方の順に、一度ずつロールバックを試すことをお勧めします。ロールバックを行ってもSSHサービスが正常に稼働しない場合は、それらの時点でシステムにすでに異常が生じていたことを意味します。
</dx-alert>



:::
</dx-accordion>


<br>
問題がまだ解決されていない場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してご連絡いただき、サポートを受けてください。

