## 現象の説明
VNCを使用してCVMに正常にログインできず、ログインパスワードを入力する前にエラーメッセージ「Account locked due to XXX failed logins」が表示される（下図参照）。
![](https://main.qcloudimg.com/raw/0dcc0c3b62a36ba0f269e629a3365564.png)

## 考えられる原因
VNCを使用したログインでは`/etc/pam.d/login`というpamモジュールを呼び出して検証を行います。一方、login設定ファイルには`pam_tally2.so`モジュールの認証が存在します。`pam_tally2.so`モジュールの機能は、LinuxユーザーがN回連続して誤ったパスワードを入力してログインを行った場合、自動的にX分間ロック、または永続的にロックを行うものです。このうち永続的なロックは手動で解除する必要があり、これを行わなければロックされたままとなります。

ログインの失敗が設定された試行回数を超えた場合、ログインアカウントは一定の時間ロックされるほか、総当たり攻撃が行われた場合はアカウントがロックされてログインできなくなる可能性もあります。下図は設定されているログイン試行可能回数です。
![](https://main.qcloudimg.com/raw/806c1d8ccded0746f5457320df479177.png)
`pam_tally2`モジュールのパラメータの説明は以下の表のとおりです。
<table>
<tr>
<th>パラメータ</th><th>説明</th>
</tr>
<tr>
<td><code>deny=n</code></td>
<td>ログイン失敗回数がn回を超えた後はアクセスが拒否されます。</td>
</tr>
<tr>
<td><code>lock_time=n </code></td>
<td>ログイン失敗後にロックされる時間（秒）。</td>
</tr>
<tr>
<td><code>un lock_time=n</code></td>
<td>ログイン失敗回数が制限を超えた後、ロック解除に要する時間。</td>
</tr>
<tr>
<td><code>no_lock_time </code></td>
<td>ログファイル <code>/var/log/faillog</code> 中に <code>.fail_locktime</code> フィールドが記録されていません。</td>
</tr>
<tr>
<td><code>magic_root   </code></td>
<td>rootユーザー（uid=0）がこのモジュールを呼び出した場合、カウンターの数値は増えません。</td>
</tr>
<tr>
<td><code>even_deny_root </code></td>
<td>rootユーザーのログイン失敗回数がdeny=n回を超えた後はアクセスが拒否されます。</td>
</tr>
<tr>
<td><code>root_unlock_time=n  </code></td>
<td> <code>even_deny_root</code> に対応するオプション。このオプションを設定した場合の、rootユーザーのログイン失敗回数が制限を超えた後のロック時間。</td>
</tr>
</table>

## 解決方法
1. [処理手順](#ProcessingSteps)を参照し、login設定ファイルに入り、`pam_limits.so`モジュール設定に一時的なコメントを付加します。
2. アカウントがロックされた原因を確認し、セキュリティポリシーを強化します。

[](id:ProcessingSteps)

## 処理手順

1. SSHを使用したCVMインスタンスへのログインを試してください。詳細については[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501)をご参照ください。
	- ログインに成功した場合は次の手順に進みます。
	- ログインに失敗した場合は、単一ユーザーモードを使用する必要があります。
2. ログイン成功後、次のコマンドを実行してログ情報を確認します。
```
vim /var/log/secure
```
このファイルは一般的にセキュリティに関する情報の記録に用いられ、このうち大部分の記録はユーザーのCVMログインの関連ログです。下図のように、情報の中から`pam_tally2`のあるエラーメッセージを取得することができます。
![](https://main.qcloudimg.com/raw/f45fb4564cfea44f0210a6e9b7124b73.png)
3. 順に次のコマンドを実行し、`/etc/pam.d`に入り、ログの中のpamモジュールエラーのキーワード`pam_tally2`を検索します。
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "pam_tally2" -l
```
下図のような情報が表示される場合は、`login`ファイルにおいてこのパラメータが設定されていることを表します。
![](https://main.qcloudimg.com/raw/a5d272e11a88d4f9cee347244fb98441.png)
4. 次のコマンドを実行し、`pam_tally2.so`モジュール設定に一時的なコメントを付加します。設定を完了すると、ログインできるようになります。
```
sed -i "s/.*pam_tally.*/#&/" /etc/pam.d/login
```
4. アカウントのロックが人為的な誤操作によるものか、総当たり攻撃によるものかを確認します。総当たり攻撃によって起こった場合は、次の方法でセキュリティポリシーを強化することを推奨します。
 - CVMのパスワードを変更し、大文字、小文字、特殊記号、数字を組み合わせた12～16桁の複雑なランダムパスワードを設定します。詳細については、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)をご参照ください。
 - CVM内の使われていないユーザーを削除します。
 - sshdのデフォルトの22ポートを1024～65525の間の他の非常用ポートに変更します。詳細については、[CVMリモートデフォルトポートの変更](https://intl.cloud.tencent.com/document/product/213/35376)をご参照ください。
 - CVMのセキュリティグループに関連付けられているルールを管理し、業務およびプロトコルに必要なポートのみをオープンにし、すべてのプロトコルおよびポートをオープンにはしないことを推奨します。詳細については、[セキュリティグループルールの追加](https://intl.cloud.tencent.com/document/product/213/34272)をご参照ください。
 - mysql、redisなどのパブリックネットワークにコアアプリケーションサービスポートへのアクセスを開放することは推奨しません。 関連するポートをローカルアクセスに変更、または外部ネットワークアクセス禁止にすることができます。
 - 「雲鏡」、「雲鎖」などの保護ソフトウェアをインストールし、リアルタイムアラームを追加して、異常なログイン情報を速やかに取得できるようにします。


