## 操作シナリオ
CVMを購入する際に、0Mbpsの帯域幅上限を選択した場合は、当該CVMはパブリックネットワークにアクセスことができません。本文書は CentOS7.5 を例とし、パブリックIP無しのCVMでは、PPTP VPN経由でパブリックIP有りのCVMに接続しパブリックネットワークにアクセスする方法について説明します。


## 前提条件
- 同じVirtual Private Cloudで2台のCVMを作成しました。（1台の**パブリックIP無しのCVM**及び1台の**パブリックネットワークIP有りのCVM**）。
- パブリックIPを備えたCVMのプライベートIPを取得しました。。

## 操作手順
### パブリックIP有りのCVMにおけるPPTPをコンフィギュレーションする

1. パブリックIP有りのCVMにログインします。
2. 下記のコマンドを実行し、 PPTPをインストールします。
```
yum install -y pptpd
```
2. 下記のコマンドを実行し、 `pptpd.conf`  コンフィギュレーションファイルを開きます。
```
vim /etc/pptpd.conf
```
3. 「**i**」 又は 「**Insert**」 を押して、編集モードに切り替え、ファイルの最後に下記の内容を追加します。
```
localip 192.168.0.1
remoteip 192.168.0.234-238,192.168.0.245
```
4.  「**Esc**」を押して、 「**:wq**」を入力し、ファイルを保存してから戻ります。
5. 下記のコマンドを実行し、`/etc/ppp/chap-secrets` コンフィギュレーションファイルを開きます。
```
vim /etc/ppp/chap-secrets
```
6. <span id="step7"> 「**i**」 又は 「**Insert**」 を押して、編集モードに切り替え、下記のフォーマットに基づき、ファイルの最後にPPTPに接続するユーザー名とパスワードを追加します。</span>
```
ユーザー名    pptpd    パスワード    *
```
例えば、PPTPに接続するユーザー名がrootであり、パスワードが123456である場合は、次の情報を追加する必要があります。
```
root    pptpd    123456    *
```
7.  「**Esc**」を押し、 「**:wq**」を入力し、ファイルを保存してから戻ります。
8. 下記のコマンドを実行し、 PPTPサービスをスタートアップします。
```
systemctl start pptpd
```
9. 順次に下記のコマンドを実行し、転送機能を実行します。
```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o eth0 -s 192.168.0.0/24 -j MASQUERADE
```

### パブリックネットワークIP 無しのCVMにおけるPPTPのコンフィギュレーション

1. パブリックネットワークIP無しのCVMにログインします。
2. 下記のコマンドを実行し、 PPTPクライアントをインストールします。
```
yum install -y pptp pptp-setup
``` 
3. 下記のコマンドを実行し、コンフィギュレーションファイルを作成します。
```
pptpsetup --create コンフィギュレーションファイルの名称 --server パブリックIP有りのCVMのプライベートIP --username  PPTPに接続するユーザー名 --password  PPTPに接続するパスワード --encrypt
```
例えば、 testコンフィギュレーションファイルを新規に作成し、パブリックIP を取得したCVMのプライベートIP が10.100.100.1である場合は、下記のコマンドを実行します。
```
pptpsetup --create test --server 10.100.100.1 --username root --password 123456 --encrypt
```
4. 下記のコマンドを実行し、 PPTPに接続します。
```
pppd call test（ステップ3で作成されたコンフィギュレーションファイルのファイル名である）
```
5. 順次に下記のコマンドを実行し、ルーティングを設定します。
```
route add -net 10.0.0.0/8 dev eth0
route add -net 172.16.0.0/12 dev eth0
route add -net 192.168.0.0/16 dev eth0
route add -net 169.254.0.0/16 dev eth0
route add -net 9.0.0.0/8 dev eth0
route add -net 100.64.0.0/10 dev eth0
route add -net 0.0.0.0 dev ppp0
```

### コンフィギュレーションが成功しているかどうかをチェックする
パブリックIP無しのCVMで、下記のコマンドを実行し、任意のパブリックアドレスをPINGし、 正常にPINGできるかどうかを確認します。 。
```
ping -c 4 パブリックアドレス
```
下記のような結果が戻った場合は、コンフィギュレーションが成功したことを示しています。
![](https://main.qcloudimg.com/raw/c841782ce0976982d1f289d3437ec0ed.png)



