## 現象の説明
VNCを使用してCVMにログインする際、正しいパスワードを入力しても正常にログインできず、「Module is unknown」エラーが表示される（下図参照）。
![](https://main.qcloudimg.com/raw/117961622ff73a5859a56bd890011302.png)

## 考えられる原因
VNCを使用したログインでは`/etc/pam.d/login`というpamモジュールを呼び出して検証を行います。一方、このモジュールは`/etc/pam.d/system-auth`モジュールをインポートして認証を行います。`/etc/pam.d/login`設定ファイルの内容は下図のとおりです。
![](https://main.qcloudimg.com/raw/334e393e16d8a03eec44009be9265ea9.png)
ログイン失敗の原因は`system-auth`設定ファイル中の`pam_limits.so`モジュールのモジュールパス設定にエラーがあることによる可能性があります。下図に示します。
![](https://main.qcloudimg.com/raw/36f36e0f2f5d0954f6fcebd39095d3b6.png)
<dx-alert infotype="explain" title="">
`pam_limits.so`モジュールの主な機能はユーザーのセッションの過程で各種システムリソースの使用状況を制限することです。モジュールパスはOSの実際の状況に応じて入力する必要があり、パスの入力ミスがあると対応する認証モジュールを見つけることができず、ログイン認証エラーが起こることがあります。

</dx-alert>



## 解決方法
1. [処理手順](#ProcessingSteps)を参照し、`system-auth`ファイルに入り、`pam_limits.so`モジュールパスの設定を見つけます。
2. `pam_limits.so`モジュールパスを正しい設定に修正すればOKです。 

[](id:ProcessingSteps)

## 処理手順

1. SSHを使用したCVMインスタンスへのログインを試してください。詳細については[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501)をご参照ください。
 - ログインに成功した場合は次の手順に進みます。
 - ログインに失敗した場合は、単一ユーザーモードを使用する必要があります。
2. ログイン成功後、次のコマンドを実行してログ情報を確認します。
```
vim /var/log/secure
```
このファイルは一般的にセキュリティに関する情報の記録に用いられ、このうち大部分の記録はユーザーのCVMログインの関連ログです。下図のように、情報の中から`/lib/security/pam_limits.so`のあるエラーメッセージを取得することができます。
![](https://main.qcloudimg.com/raw/8f9f992d1835a9058020b435f1ef3c99.png)
3. 順に次のコマンドを実行し、`/etc/pam.d`に入り、ログの中のpamモジュールエラーのキーワード`/lib/security/pam_limits.so`を検索します。
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "/lib/security/pam_limits.so" -l
```
下図のような情報が表示される場合は、`system-auth`ファイルにおいてこのパラメータが設定されていることを表します。
![](https://main.qcloudimg.com/raw/eab27cf686eccfeb8a8b796360010bb5.png)
4. `system-auth`ファイルに入り、`pam_limits.so`モジュールパスの設定を修正します。
例えば、64ビットのOSでは、このモジュールパスは絶対パス`/lib64/security/pam_limits.so`として設定することも、相対パス`pam_limits.so`として設定することもできます。


