##故障について
SSHを使用してLinuxインスタンスにログインすると、「ssh_exchange_identification: Connection closed by remote host」または「no hostkey alg」が出現する。


## 考えられる原因
`/var/empty/sshd`および`/etc/ssh/ssh_host_rsa_key`設定ファイルの権限が変更されるなど、sshd設定ファイルの権限が変更されたため、SSHを使用したログインができなくなっている可能性があります。


## ソリューション
実際のエラー情報に応じて対応する手順を選択し、設定ファイルの権限を修正します。
 - エラー情報が「ssh_exchange_identification: Connection closed by remote host」である場合は、[/var/empty/sshd ファイル権限の修正](#sshd) 手順をご参照ください。
 - エラー情報が「no hostkey alg」である場合は、[/etc/ssh/ssh_host_rsa_key ファイル権限の修正](#rsa_key) 手順をご参照ください。



## 処理手順

### /var/empty/sshd ファイル権限の修正[](id:sshd)
- [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)。
2. 次のコマンドを実行し、エラーの原因を確認します。
```
sshd -t
```
次のような情報が返されます：
```plaintext
"/var/empty/sshd must be owned by root and not group or world-writable."
```
3. 次のコマンドを実行し、`/var/empty/sshd/` ファイル権限を修正します。
```
chmod 711 /var/empty/sshd/
```



### /etc/ssh/ssh_host_rsa_key ファイル権限の修正[](id:rsa_key)
- [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)。
2. 次のコマンドを実行し、エラーの原因を確認します。
```
sshd -t
```
返される情報には次のようなフィールドが含まれます。
```plaintext
"/etc/ssh/ssh_host_rsa_key are too open"
```
3. 次のコマンドを実行し、`/etc/ssh/ssh_host_rsa_key` ファイル権限を修正します。
```
chmod 600 /etc/ssh/ssh_host_rsa_key
```
