## ユースケース

NTPD（Network Time Protocol daemon）は Linux OSのデーモンプロセスであり、NTP プロトコルを完全に実装され、ローカルシステムとクロックソースサーバー間の時間差を修正するために使用されます。時間を定期的に更新するNTPDateとは異なり、ntpdは時間ギャップなしで継続的に時間を修正します。本ドキュメントでは NTPD のインストールと使い方を紹介します。

## 注意事項

* 一部のOSが chrony をデフォルトの NTP サービスとして利用しています。 「systemctl is-active ntpd.service」コマンドを利用して、NTPDが実行されているかどうかを確認します。「systemctl is-enabled ntpd.service」コマンドを利用して、ブート時にNTPDが自動的に開始するように構成されているかどうかを確認します。
* NTP サービスの通信ポートは UDP 123であり、 NTP サービスを設定する前に UDP 123 ポートが開放していることを確保してください。 netstat -nuplを介してインスタンスが UDP 123 ポートを開通しているかどうかを確認できます。また、[セキュリティグループの操作ガイド](https://intl.cloud.tencent.com/document/product/213/18197) を参照してUDP 123 ポートを開放してください。

> **注意事項：**
> 本文の下記操作は、 CentOS 7.5 64ビットインスタンスで実行されます。

## 操作手順
### インストール

- 以下のコマンドを実行して、NTPD がインストールされているかどうかを確認します：
```
rpm -qa | grep ntp
```
![ntpdがインストールされているかどうかを判断する](https://main.qcloudimg.com/raw/34073904c49e80ab61da25559c7239e5.png)
- ntpdがインストールされていない場合、 yum install ntpを実行してインストールしてください。何も設定しなかった場合、 NTPD はデフォルトでクライアントモードに設定されます。
```
yum -y install ntp
```

### 設定
-  vimでNTP サービスの設定ファイルを開いて編集します。
```
vi /etc/ntp.conf
```
- サーバーの関連設定を検索し、サーバーを設定対象のNTPクロックソースサーバーに修正して、必要がないNTPクロックソースサーバーを削除します。
![serverの設定](https://main.qcloudimg.com/raw/b21b559ce745ef5c765251a8ee514dca.png)

### 起動
- 「service ntpd start」コマンドでNTP サービスを起動します。 NTP が既に起動済みの場合、「service ntpd restart」コマンドで再起動してください。
```
service ntpd start
```
![ntpを起動する](https://main.qcloudimg.com/raw/470afd5f311b5ba3ad321ed12d974c88.png)

### ステータスの確認
-  netstatを利用してNTPサービスポートudp 123が正常にリッスンされているかどうかを確認します。
```
netstat -nupl
```
![netstat -nupl](https://main.qcloudimg.com/raw/e7eb5ed8529fdc1366210ef76cf09bd3.png)
- 以下のコマンドを実行して、NTPDのステータスが正常であるかどうかを確認します：
```
service ntpd status
```
![ntpd status](https://main.qcloudimg.com/raw/8af337c167f295938f5edbc005032809.png)
- 「ntpstat」を利用して NTPD が正常に起動され、正しいNTPクロックソースサーバーに構成されているかどうかを確認します。このコマンドは現在のNTPクロックソースサーバーのIP アドレスが返されます。このIPアドレスは、上記で設定したNTPクロックソースサーバーのIPアドレスである必要があります。（ 「nslookup ドメイン名」を利用してドメイン名に対応するIP アドレスを取得できる）
![ntpstat](https://main.qcloudimg.com/raw/83d49c87c485989123acbb9a30d92d0c.png)

- 更に詳細なNTPサービス情報は ntpq -p を利用して取得できます。
![ntpq](https://main.qcloudimg.com/raw/87df34053b422b0c03e038e4e5a9fde0.png)
> remote：このリクエストに応答するNTPサーバーの名前。
> refid：NTP サーバーが使用する上位のNTP サーバーです。
> st：リモートサーバーのレベルです。NTP は階層構造であり、トップサーバーから、複数のRelay Server 、クライアントまでの構造になっています。サーバーは高レベルから低レベルまで1-16に設定されます。負荷とネットワークの輻輳を緩和するため、原則的にレベル1のサーバーに直接接続することは避けてください。
> when：最後に成功したリクエストから何秒経過したか。
> poll：同期間隔（秒単位）。最初は、NTP を実行する時に、poll の値は小さく、サーバーと同期の頻度が高くなるため、正しい時刻範囲に調整できます。その後は poll の値は徐々に増加し、それに応じて同期頻度が低くなります。
> reach：これは8進値であり、サーバーに接続できるかどうかをテストするために使用されます。その値は、接続が成功するたびに増加します。
> delay：ローカルマシンからNTPサーバーに同期要求を送信する往復時間。
> offset：NTPを介して同期されたホスト時間とタイムソースの時間の差、単位はミリ秒（ms）です。オフセットが0に近いほど、ホストとNTPサーバーの時間が近くなります。
> jitter：これは統計に使用される値です。特定の連続した接続数でオフセットの分布状況を統計します。簡単に言えば、この値の絶対値が小さいほど、ホストの時間はより精確になります。

###  NTPD を自動起動に設定する

- 次のコマンドを実行して、起動時に NTPDの自動起動を設定します。
```
systemctl enable ntpd.service
```

- 次のコマンドを実行して、起動時にchronyが起動するように設定されているかどうかを確認します
```
systemctl is-enabled chronyd.service
```

- chronyはntpdと互換性がなく、NTPDの起動に失敗する可能性があります。次のコマンドを実行して、起動時に実行されるソフトウェアのリストからchronyを削除します。
```
systemctl disable chronyd.service
```


