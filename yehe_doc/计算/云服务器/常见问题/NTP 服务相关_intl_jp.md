### NTPサービスを設定した後、NTPの同期間隔を調整するにはどうすればいいですか？
[NTPサービスの設定](https://intl.cloud.tencent.com/document/product/213/32381)を実行した後、ntpdサービスを再起動してNTPの同期間隔をリセットできます。ntpd同期間隔を手動で設定する場合は、次の手順をご参照ください：
1. 次のコマンドを実行して、NTPファイルを変更します。
```
vi /etc/ntp.conf
```
2. **i**を押して編集モードに入り、以下の設定を行います：
  1. `servertime1.tencentyun.com iburst`があれば、行の先頭に`#`を付けてコメントしてください。
  2. 以下のコンフィグレーションを追加します。ここで`minpoll 4`は最小2<sup>4</sup>、`maxpoll 5`は最大2<sup>5</sup>を表します。
```
server time1.tencentyun.com minpoll 4 maxpoll 5
```
設定が完了したら、次の図に示すように**:wq**と入力して変更を保存し、終了します。
![](https://main.qcloudimg.com/raw/02d6457d29b4c573605e3c79c5ccfc9f.png)
3. ntpdサービスを再起動した後、`ntpd-p`コマンドを実行すると、pollの値が16(つまり2<sup>4</sup>)であることがわかります。下図の通りです：
![](https://main.qcloudimg.com/raw/9fa0c72751de74d3b6e72cc1ca831952.png)

### Tencent Cloudが提供するntpd クロックソースサーバーからの時間はどのソースから取得されますか？
NTPクロックの上流は北斗の時間源となります。
 
### NTPサービス設定にlocalhost.localdomain timeoutが報告されることはどんな原因ですか？どのように修復すればいいですか？
エラーメッセージは下図のように表示されます：
![](https://main.qcloudimg.com/raw/1b3158135475e6cfbee28d2373685616.png)
このエラーが発生すると、POSTROUTINGを実行した可能性があります。確認してみてください。そうであれば、コンフィグレーションファイル`ntp.conf`のソースIPをeth0のIPに変更してください。

### クラウド下のマシンはクラウド上のマシンとNTPを共有できますか？NTP同期アドレスを提供できますか？
プライベートネットワークNTPはTencent Cloud上のインスタンスでのみ使用できます。クラウド下のマシンがパブリックネットワークをサポートしている場合、パブリックネットワークNTPソースを設定することで同期を実現できます。アドレスは以下のとおりです：
- プライベートネットワークNTPサーバー
```plaintext
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```
- パブリックネットワークNTPサーバー
```plaintext
ntp.tencent.com
ntp1.tencent.com
ntp2.tencent.com
ntp3.tencent.com
ntp4.tencent.com
ntp5.tencent.com
```
以下は、古いパブリックネットワークNTPサーバーアドレスです。古いアドレスは引き続き使用できますが、新しいパブリックネットワークNTPサーバーアドレスを構成して使用することをお勧めします。
```plaintext
time.cloud.tencent.com
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

### カスタムイメージーを使用して作成されたCVMが通常の時刻と一致しないのはなぜですか？
NTPサービスがオンになっていることを確認してください。この後にNTP同期機能を使用する場合、インスタンスのオペレーティング・システムに応じて以下のドキュメントを参照してNTP設定を行ってください。設定完了後にカスタムイメージを再作成してください。
 - [Linuxインスタンス：NTPサービスの設定](https://intl.cloud.tencent.com/document/product/213/32381)
 - [Windowsインスタンス：NTPサービスの設定](https://intl.cloud.tencent.com/document/product/213/32380)



### カスタムイメージを使用して作成されたCVMntp.confの内容が復元されたのはなぜですか？
システム内のCloud-Initの初期化が原因です。カスタムイメージを作成する前に`/etc/cloud/cloud.cfg`のNTP関連の設定を削除してください。詳細については[Cloud-InitとCloudbase-Init問題](https://intl.cloud.tencent.com/document/product/213/19670)をご参照ください。

### プライベートネットワークDNSを変更すると、どのような影響がありますか？
Tencent Cloud内部のドメイン名解析に関わる業務はいずれも影響を受けます。例：
- yumダウンロードに影響します。yumソースはデフォルトでTencentのプライベートネットワークのドメイン名になります。DNSを変更した場合は、yumソースも変更してください。
- 監視データのエスカレーションに影響します。この機能はプライベートネットワークのドメイン名に依存しています。
- サーバーの時刻同期NTP機能に影響します。この機能はプライベートネットワークのドメイン名に依存しています。

### Windowsシステムインスタンスのローカル時間が米国東部時間に設定されていますが、再起動後に北京時間にリセットされるのはなぜですか？
このインスタンスでWindows timeサービスがオンになっていることを確認してください。このサービスがオンになっていない場合は、手動でオンにしてください。サービスがオンになると、インスタンスのシステム時刻が自動的に同期されます。このサービスは、電源を入れて起動するように設定することをお勧めします。

### ntpq-npコマンドを使用して同期時刻を表示できないのはなぜですか？
エラーメッセージは下図のように表示されます：
![](https://main.qcloudimg.com/raw/88972a2aeda155c10000e8576d16bbe9.png)
このエラーは通常、`/etc/ntp.conf`のlistenネットワークデバイスがIP設定されていないか、インスタンスでないプライベートネットワークのプライマリIPを設定した場合に発生します。そうである場合は、プライマリIPに変更してから、ntpdを再起動してください。

### パブリックネットワークNTPのタイムサーバーを使用して時刻を同期しているときにエラーが発生しました。どのように対処しますか？
パブリックネットワークNTPタイムサーバーを使用して時刻を同期すると、`no server suitable for synchronization found'というエラーが報告されました。下図の通りです：
![](https://main.qcloudimg.com/raw/1909910bc2a86a5f93e09f4601654327.png)
原因としては、インスタンスのパブリックIPがDDOS攻撃を受けたとき、NTPリフレクション攻撃保護ポリシーがトリガーされ、Tencent Cloudにアクセスするソースポート123のパブリックネットワークトラフィックがすべて遮断されることで、時刻同期の異常を引き起こすことが考えられます。インスタンスを使用する際には、可能な限りプライベートNTPタイムサーバーを使用して時刻を同期することをお勧めします。



