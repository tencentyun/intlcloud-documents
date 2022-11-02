## Output管理
コンソールの[Flow Management](https://console.tencentcloud.com/mdc/flow)ページで、リスト内のいずれかのFlowをクリックすると、そのFlowの詳細情報を確認できます。
![](https://qcloudimg.tencent-cloud.cn/raw/6e157c3ffc610bcf01c247a441a538cd.png)
Flow情報ページに進んだ後、ページ上部の**Output**をクリックすると、Output管理ページに進めます。そのページでOutputの追加、削除、編集の操作を行うことができます。
![](https://qcloudimg.tencent-cloud.cn/raw/ddfed18e28122e9198549541d3ebfd70.png)


## Outputの作成
**Create Output**ボタンをクリックすると、Outputを追加できます。クリックするとポップアップウィンドウが表示されますので、関連情報を入力してから**Confirm**をクリックすれば、Outputの追加が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/e9b1da7a805b27d5dcfa452775e7461d.png)

- **Output Name**：Output名です。簡単な名前を入力すれば、複数のOutput情報を管理しやすくなります。
- **Output Region**：Outputのあるリージョンで、ここではストリームの伝送先リージョンを選択します。
- **Output Protocol**：Outputのトランスポートプロトコルを選択し、プロトコルによって異なる設定をする必要があります。

  | Inputプロトコル | Outputオプションプロトコル |
  | -----------| ---------------|
  | RTMP,RTMP_PULL       | RTMP ,RTMP_PUSH,RTMP_PULL|
  | SRT         | SRT,RTMP_PUSH|
  | RTP         | RTP        |
  | RTSP        | RTSP       |
  

### RTMP_PUSH
このプロトコルを選択した場合、Outputは指定されたアドレスにストリームをリレーします。
![](https://qcloudimg.tencent-cloud.cn/raw/1a379f8a32e9ca1bd5341ade3a24912b.png)

- **Destination URL**：RTMP Urlです。例：rtmp://example.com/live。
- **Flow Key**：RTMPストリームキーです。例： e18c3c4dd05aef020946e6afbf9e04ef。


### RTMP_PULL
Outputからプルする必要がある場合、Outputでこのプロトコルを選択できます。Outputを作成すると、Outputリストでプルアドレスを取得できます。
![](https://qcloudimg.tencent-cloud.cn/raw/678b8da18059dec35579f1515c91e1ff.png)

- **CIDR IP AllowList**：IPホワイトリストです。プッシュに使用するIPを制限し、セキュリティを強化します。例： 203.3.3.3/28. 複数入力する必要がある場合は、セミコロンで区切ってください。例：203.3.3.3/28;202.3.3.3/28。

### SRT Listener
![](https://qcloudimg.tencent-cloud.cn/raw/13071f72fe033f1a82b1bba87c7b7a56.png)
- **Mode**：Listenerモードを選択します。受信側でSRT Callモードを使用してOutputをリクエストする必要があります。プルアドレスがOutputリストページに表示されます。
- **Latency Setting**：サービス側のLatencyパラメータを設定します。プッシュ側とStreamLinkのリージョンが同じ国の場合は120ms、異なる国の場合は200ms、異なる大陸の場合は1000msに設定することを推奨しています。実際には、割り当てられたIPに応じて調整できます。
- **Enable Encryption**：暗号化が有効になっている場合、受信側でも暗号化を有効にし、Encryption KeyとKey Lengthという2つのフィールドを入力する必要があります。入力しないとプルに失敗します。
  - **Encryption Key**：暗号化のため、このフィールドに関連するkeyを入力する必要があります。
  - **Key Length**：このフィールドでKeyの長さを選択する必要があります。
- **Failover**：このプロトコルは現在、フェイルオーバーの切り替えをサポートしていないため、このオプションは現時点では利用できません。
- **CIDR IP Allowlist**：IPホワイトリストです。プッシュに使用するIPを制限し、セキュリティを強化します。例： 203.3.3.3/28. 複数入力する必要がある場合は、セミコロンで区切ってください。例：203.3.3.3/28;202.3.3.3/28。

### SRT Caller
![](https://qcloudimg.tencent-cloud.cn/raw/254cb4af2ca2e3d27be2f0ff724b02f4.png)
- **Mode**：Callerモードを選択します。このモードでは、StreamLinkはSRTプロトコルを使用して、指定されたアドレスにストリームを伝送します。
- **Destination**：SRTプッシュを受信するIPアドレスです。ここにドメイン名を入力することもできます。
- **Port**：SRTプッシュを受信するポートです。
- **Latency Setting**：サービス側のLatencyパラメータを設定します。ソースストリームアドレスとStreamLinkのリージョンが同じ国の場合は120ms、異なる国の場合は200ms、異なる大陸の場合は1000msに設定することを推奨しています。実際には、割り当てられたIPに応じて調整できます。
- **Enable Encryption**：受信側の暗号化が有効になっている場合、このスイッチをオンにし、Encryption KeyとKey Lengthという2つのフィールドを入力する必要があります。入力しないと、Outpostのプッシュに失敗します。
  - **Encryption Key**：暗号化のため、このフィールドに関連するkeyを入力する必要があります。
  - **Key Length**：このフィールドでKeyの長さを選択する必要があります。長さは、受信側で設定された長さと一致させる必要があります。
- **Failover**：このプロトコルは現在、フェイルオーバーの切り替えをサポートしていないため、このオプションは現時点では利用できません。


### RTP
このプロトコルを選択した場合、Outputは指定されたアドレスにストリームをプッシュします。
![](https://qcloudimg.tencent-cloud.cn/raw/4cca576a3a1da76f0e2a2a4ab7d80b48.png)

- **Destination**：Outputは、指定されたアドレスにストリームをプッシュします。
- **Port**：現在、Outputのトランスポートプロトコルの選択は、Inputのプロトコルに強く依存しています。