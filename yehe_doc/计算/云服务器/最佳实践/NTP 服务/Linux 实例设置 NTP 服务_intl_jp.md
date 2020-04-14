## ユースケース

NTPD（Network Time Protocol daemon）は Linux OSのデーモンプロセスであり、NTP プロトコルを完全に実装され、ローカルシステムと時刻源サーバー前の時間の調整に使われてます。NTPD と NTPDate の区別とは、NTPDが一気に時刻調整ではなくステップ式で徐々に時刻を調整することと比べ、 NTPDate がブレークポイントで時刻を調整します。本ドキュメントでは NTPD のインストールと使い方を紹介します。

## 注意事項

* 一部のOSが chrony をデフォルトの NTP サービスとして利用します。 「systemctl is-active ntpd.service」を利用して NTPD が実行しているかを確認します。「systemctl is-enabled ntpd.service」を利用して  NTPD がスタートアップに設定しているかを確認します。詳細については、下記のスタートアップ時NTPD の設定をご参照ください。
* NTP サービスの通信ポートは UDP 123であり、 NTP サービスを設定する前に UDP 123 ポートが開放していることを確保してください。 netstat -nupl に通してインスタンスが UDP 123 ポートを開通しているかどうかを確認できます。[セキュリティグループの操作ガイド](https://intl.cloud.tencent.com/document/product/213/18197) を参照して UDP 123 ポートを開放してください。

> **注意事項：**
> 本文の下記操作はすべて CentOS 7.5 64bit インスタンスで行います。

## 操作手順
### インストール

- 下記のコマンドを利用して NTPD がインストールされているかどうかを確認します：
```
rpm -qa | grep ntp
```
![ntpdがインストールされてるかどうかを判断する](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
- インストールされていない場合、 yum install ntp を利用してインストールを行います。何も設定しなかった場合、 NTPD はデフォルトでクライアントモードに設定されます。
```
yum -y install ntp
```

### 設定
-  vim で NTP サービス設定ファイルを開いて編集します。
```
vi /etc/ntp.conf
```
-  server の関連設定を検索し、 server を設定対象の NTP 時刻源サーバーに修正して、なお当分の間必要がない NTP 時刻源サーバーを削除します。
![serverの設定](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)

### 起動する
- 「service ntpd start」を利用して  NTP サービスを起動します。 NTP が既に起動済みの場合、 「service ntpd restart」を利用してリスタートを行います。
```
service ntpd start
```
![ntpを起動する](https://main.qcloudimg.com/raw/470afd5f311b5ba3ad321ed12d974c88.png)

### 状態を確認する
-  netstat を利用して NTP のサービスポート udp 123 が正常に監視されているかどうかを確認します。
```
netstat -nupl
```
![netstat -nupl](https://main.qcloudimg.com/raw/e7eb5ed8529fdc1366210ef76cf09bd3.png)
- 下記のコマンドを利用して NTPD 状態が正常であるかどうかを確認します：
```
service ntpd status
```
![ntpd status](https://main.qcloudimg.com/raw/8af337c167f295938f5edbc005032809.png)
- 「ntpstat」を利用して NTPD が正常に起動されているかどうかまたは正しい NTP 時刻源サーバーに設定されているかどうかを確認します。このコマンドは現在の NTP 時刻源サーバーの IP アドレスを出力します。この IP アドレスは上記設定された NTP 時刻源サーバーの IP アドレス（ 「nslookup ドメイン名」 を利用してドメイン名に対応する IP アドレスを取得できる）です。
![ntpstat](https://main.qcloudimg.com/raw/83d49c87c485989123acbb9a30d92d0c.png)

- 更に詳細な NTP サービス情報は ntpq -p を利用して取得できます。
![ntpq](https://main.qcloudimg.com/raw/87df34053b422b0c03e038e4e5a9fde0.png)
> remote：このリクエストに応答したNTPサーバーの名称。
> refid：NTP サーバーが利用する上位 のNTP サーバー。
> st：remote リモートサーバーのレベルです。NTP は階層構造であり、トップサーバーから、複数階層の Relay Server 、クライアントまでの構造になっています。サーバーは高レベルから低レベルまで 1-16に設定されます。負荷とネットワークの混雑を緩和するため、原則的にレベル1のサーバーに接続するのを避けましょう。
> when：前回リクエスト成功してから今までの秒数。
> poll：ローカルPCとリモートサーバーはどのぐらいの間隔で同期を行います（単位は秒）。 始めてNTP を実行する時に、 poll の値は小さく、サーバーと同期の頻度が徐々に増え、正しい時刻範囲に調整できます、その後は poll の値は徐々に増え、それに応じて同期の頻度は減って行きます。
> reach：これは8進数の値であり、サーバーに接続できるかどうかをテストするために使用されます。その値は、接続が成功するたびに増加します。
> delay：ローカルPCから NTP サーバーへの同期要求までの round trip time。
> offset：ホストが NTP に通して、同期の時刻と同期の時刻源の時間のオフセット、単位はミリ秒（ms）。offset が0に近いほど、ホストと NTP サーバーの時間が近い。
> jitter：これは統計に使用される値です。特定の連続した接続数で offset の分布状況を統計します。簡単に言えば、この値の絶対値が小さいほど、ホストの時間はより精確になります。

###  NTPD をスタートアップに設定する

- 下記コマンドを利用して NTPD をスタートアップに設定します。
```
systemctl enable ntpd.service
```

- 下記のコマンドを利用して chrony をスタートアップに設定されているかどうかを確認します。
```
systemctl is-enabled chronyd.service
```

- chrony と NTPD が衝突した場合、 NTPD が起動失敗を引き起こす可能性があります。下記のコマンドを利用して、chrony をスタートアップから削除する必要があります。
```
systemctl disable chronyd.service
```


