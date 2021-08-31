### NTPサービスを構成した後、NTPサーバーの同期間隔を調整するにはどうすればよいですか。
 [NTPサービスを構成](https://intl.cloud.tencent.com/document/product/213/32381)した後、ntpdサービスを再起動してNTPサーバーの同期間隔をリセットできます。ntpd同期間隔を手動で設定するには、次の手順を実行します。
1.次のコマンドを実行して、NTP構成ファイルを変更します。
```
vi /etc/ntp.conf
```
2.  **i** を押して編集モードに入り、次のように構成します。
  1.  `server time1.tencentyun.com iburst`tの先頭にポンド記号`#`を追加して、コメントアウトします。
  2. 次の構成を追加します。ここで、 `minpoll 4` は最小間隔が2<sup>4</sup>であることを意味し、`maxpoll 5` は最大間隔が2<sup>5</sup>であることを意味します。
```
server time1.tencentyun.com minpoll 4 maxpoll 5
```
構成が完了した後、次の図に示すように、**:wq** と入力して変更を保存し、ファイルを閉じます。
![](https://main.qcloudimg.com/raw/02d6457d29b4c573605e3c79c5ccfc9f.png)
3. ntpdサービスを再起動した後、 `ntpd -p`コマンドを実行して、ポーリング値が16（つまり、2<sup>4</sup> ）であることを確認します。次の図に示すように：
![](https://main.qcloudimg.com/raw/9fa0c72751de74d3b6e72cc1ca831952.png)

### Tencent Cloudが提供するntpdタイムソース(NTPサーバー)の時間は、どのソースから取得されますか。
NTPサーバーは通常、BeiDou衛星時計を使用します。
 
### NTP構成でlocalhost.localdomain timeoutエラーが報告された場合はどうすればよいですか。
次の図のようなエラーが表示されます。
![](https://main.qcloudimg.com/raw/1b3158135475e6cfbee28d2373685616.png)
POSTROUTINGを実行したかどうかを確認してください。実行した場合、 `ntp.conf`構成ファイルの送信元IPをeth0のIPアドレスに変更してください。

### off-cloudサーバーはNTPをTencent Cloud CVMと共有できますか。NTP同期アドレスを提供できますか。
プライベートNTPサーバーは、Tencent Cloud上のインスタンスでのみ使用できます。off-cloudサーバーがパブリックネットワークをサポートしている場合、パブリックNTPサーバーを構成することで同期を実現できます。アドレスは次のとおりです。
- プライベートNTPサーバー
```
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```
- パブリックNTPサーバー
```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

### カスタムイメージを介して作成されたCVMインスタンスの時刻が正しくないのはなぜですか。
NTPサービスが有効になっているか確認してください。後でNTP同期機能を使用するには、インスタンスのOSに応じて次のドキュメントを参照してNTPを設定してください。次に、カスタムイメージを再作成します。
 - [ Linuxインスタンス：NTPサービスの設定方法](https://intl.cloud.tencent.com/document/product/213/32381)
 - [ Windowsインスタンス：NTPサービスの設定方法](https://intl.cloud.tencent.com/document/product/213/32380)

### CVMがNTPサーバーにpingを実行できない場合、NTP同期は影響を受けますか。
影響を受けません。NTPサービスにアクセスできる限り、同期は機能します。

### カスタムイメージを介して作成されたCVMのntp.confコンテンツが復元されるのはなぜですか。
Cloud-Initの初期化が原因となっている可能性があります。カスタムイメージを作成する前に `/etc/cloud/cloud.cfg`中のNTP関連の設定を削除してください。詳細については、 [cloud-init / cloudbase-init ](https://intl.cloud.tencent.com/document/product/213/19670)をご参照ください。

### プライベートネットワークDNSが変更された後、具体的にどのような影響を及ぼすでしょうか。
Tencent Cloudプライベートドメイン名の解決に関連するすべてのサービスが影響を受けます。例えば、
- yumのダウンロードに影響します。yumリポジトリはTencent Cloudプライベートドメイン名を使用します。 DNSを変更した後、YUMリポジトリを変更する必要があります。
- 監視データの報告に影響します。この機能はプライベートドメイン名に依存します。
- NTP機能は、サーバー時間を同期するためにプライベートドメイン名に依存し、影響を受けます。

### Windowsシステムインスタンスの現地時間は米国東部時間に設定されていますが、再起動後に北京時間にリセットされるのはなぜですか。
インスタンスでwindowstimeサービスが有効になっているかどうかを確認してください。サービスを有効にしていない場合は、手動で有効化する必要があります。サービスを有効にした後、インスタンスのシステム時刻は自動的に同期されます。起動後に自動的に開始するようにこのサービスを設定することをお勧めします。　

### ntpq -npコマンドを使用して同期時間を表示できないのはなぜですか。
次の図のようなエラーが表示されます。
![](https://main.qcloudimg.com/raw/88972a2aeda155c10000e8576d16bbe9.png)
 `/etc/ntp.conf` 構成ファイルで、listenネットワークデバイスにIPが構成されていないか間違ったIPが構成されていないかを確認してください。はいの場合、インスタンスのプライマリプライベートIPに変更し、ntpdを再起動します。

### パブリックNTPサーバーを使用して時刻を同期するときにエラーが発生した場合はどうすればよいですか。
パブリックNTPサーバーを使用して時刻を同期するときに、「`no server suitable for synchronization found」というエラーが表示されます。以下に示すように：
![](https://main.qcloudimg.com/raw/1909910bc2a86a5f93e09f4601654327.png)
エラーの理由として考えられるものは次の通りです：インスタンスのパブリックIPがDDoS攻撃を受けると、NTP保護ポリシーがトリガーされ、Tencent Cloudのソースポイント123ですべてのパブリックインバウンドトラフィックをブロックし、同期例外を引き起こします。インスタンスを使用するときは、プライベートNTPサーバーを使用して時刻を同期することをお勧めします。
