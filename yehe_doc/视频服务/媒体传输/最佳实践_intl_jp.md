# リージョン間転送に関するプラクティス

## ユースケースの説明
ライブストリーミングを例に取った場合、中国成都で開催すると仮定すると、現場の信号は中国上海に送信され、制作されることになります。制作された信号は、各ライブストリーミングプラットフォームに送信され、同時配信されます。ライブストリーミングプラットフォームは、中国、欧州、北米に設置されています。

## 対処方法
![](https://qcloudimg.tencent-cloud.cn/raw/62fd6a79371347984aa53930a465bcd0.jpeg)
- 現場から信号がSRTプロトコルでスタジオに送信されます。
- スタジオでは、オリジナル信号から最終的な配信信号が作成され、SRTプロトコルによって各ライブストリーミングプラットフォームに送信されます。
- ライブストリーミングプラットフォームでは、StreamLinkから自発的にプルするか、StreamLinkが直接ライブストリーミングプラットフォームにプッシュすることができます。


## 設定についての説明
上海のプロダクションセンターに送信する必要のある信号があると仮定します。プロダクションセンターには制作されたプログラムストリームがあり、それを各配信プラットフォームに送信する必要があります。


### 1. 現場からスタジオへのFlow設定
現場とプロダクションセンター間のレイテンシー要件は比較的低いため、このセクションではSRTトランスポートプロトコルを選択しています。オリジナル信号は非常に重要であり、プロダクションセンターはソースストリームに依存しなければ最終的なプログラムを制作できないため、ここでは転送用に2つの個別Flowが作成されています。

#### SRT Main Flowの作成
現場は成都にあるので、ページの左上隅でRegionを成都に切り替え、Input側とプッシュ側を同じリージョンにする必要があります。
![](https://qcloudimg.tencent-cloud.cn/raw/c8e72acfc3666277ca4686e74feba235.png)
![](https://qcloudimg.tencent-cloud.cn/raw/51e1c324d0da25db355060a4ad7b89e5.png)

- **Name**：chengdu_main_ori_streamを入力しておくと、後で管理しやすくなります。
- **Max Bandwidth**：制作に使用するオリジナル信号はビットレートが高いので、20Mbpsを選択しています。
- **Protocol**：SRTプロトコルを選択します。
- **Mode**：モードはListenerを選択し、現場からStreamLinkに信号を直接プッシュします。
- **Latency**プッシュ側とStreamLinkが同じ都市にあり、中国の同じ都市では転送時のRTTは通常10ms以下であるため、Latencyを60msに設定しています。プッシュする際にRTTが高いことが判明した場合、プッシュ側のLatencyの設定を調整してLatencyを大きくすることができます。
- **Decryption Settings**：プッシュ側には固定IPが存在するため、このプッシュでは暗号化を設定せず、代わりにIPホワイトリストを使用してセキュリティを確保します。
- **CIDR IP Allowlist**：プッシュ側で使用するIPを入力し、Flowへのプッシュをこのイベントのデバイスのみができるように制限します。

入力完了後、**Create**をクリックして、Flowの設定を保存します。

#### Outputの追加
プロダクションセンターが上海にあるため、上海にあるOutputを追加する必要がありますが、遅延を考慮し、OutputにはSRTプロトコルを選択しています。
![](https://qcloudimg.tencent-cloud.cn/raw/57276bf97bce0d5032fd4d2691df7beb.png)

- **Output Name**：shanghai_main_outputを入力しておくと、後で管理しやすくなります。
- **Output Region**：遅延を考慮し、上海を選択します。
- **Output Protocol**：SRTプロトコルを選択します。
- **Mode**：Listenerモードを選択すると、スタジオがStreamLinkからプルし、操作しやすくなります。
- **Latency Setting**プル側とStreamLinkが同じ都市にあり、中国の同じ都市では転送時のRTTは通常10ms以下であるため、Latencyを60msに設定しています。プッシュする際にRTTが高いことが判明した場合、プッシュ側のLatencyの設定を調整してLatencyを大きくすることができます。
- **Enable Encryption**：プル側には固定IPが存在するため、このプッシュでは暗号化を設定せず、代わりにIPホワイトリストを使用してセキュリティを確保します。
- **CIDR IP AllowList**：プル側で使用するIPを入力し、プルできるデバイスを制限します。

上記の情報を入力後、**Confirm**をクリックしてoutputの設定を保存します。

#### SRT Backup Flowの作成
作成プロセスと設定はMain Flowと同じなので、ここでは繰り返して説明しません。


### 2. スタジオから各配信プラットフォームへのFlow設定
スタジオで制作されたプログラムは、最終的に各プラットフォームへ配信される必要があります。各プラットフォームでの配信は遅延の影響をあまり受けないため、この転送にはRTMPプロトコルを使用しています。

#### RTMP Failover Flowの作成
スタジオは上海にあるので、ページの左上隅でRegionを上海に切り替え、Input側とプッシュ側を同じリージョンにする必要があります。
![](https://qcloudimg.tencent-cloud.cn/raw/3f2cc6be8882b2ef9f7ea3c2efa8a285.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0ece7d6ebe0c1062f3210c8354d2b3cf.png)

- **Name**：pgm_mainを入力しておくと、後で管理しやすくなります。
- **Max Bandwidth**：最終的な配信に使用するストリームのビットレートが低いため、10Mbpsを選択しています。
- **Protocol**：RTMPプロトコルを選択します。
- **Failover**：Failoverを開きます。
- **CIDR IP Allowlist**：プッシュ側で使用するIPを入力し、Flowへのプッシュをスタジオのデバイスのみができるように制限します。

入力完了後、**Create**をクリックして、Flowの設定を保存します。

#### Outputの追加
米国、欧州、中国という3つのリージョンで配信する必要があるため、リージョンごとに少なくとも1つのOutputの作成が必要です。OutputはRTMP_PULLプロトコルを選択して、ライブストリーミングプラットフォームが自発的にプルできるようにし、ライブストリーミングプラットフォームの処理を容易にします。1つのOutputで同時にプルできるストリームは最大4つなので、同じリージョンで複数のプラットフォームがプルする場合、複数のOutputを作成することをお勧めします。欧州を例に取ると、2つのライブストリーミングプラットフォームが同時に配信する必要がある場合、2つのOutputを作成することで、それぞれのプラットフォームが個別アドレスを使用し、互いに影響を及ぼさないようにすることができます。ここでは、1つのOutputの作成のみを示します。他のOutputの作成プロセスは同じであるため、繰り返して説明しません。
![](https://qcloudimg.tencent-cloud.cn/raw/edf53f502063c2f3c93ef8170256a1dc.png)

- **Output Name**：eu_pgm_platform_aを入力しておくと、後で管理しやすくなります。
- **Output Region**：Frankfurt、Germanyを選択します。
- **Output Protocol**：RTMP_PULLを選択し、ライブストリーミングプラットフォームが自発的にプルするようにし、ライブストリーミングプラットフォームの処理を容易にします。
- **CIDR IP Allowlist**：プル側で使用するIPを入力し、プルできるデバイスを制限します。

上記の情報を入力後、**Confirm**をクリックしてOutputの設定を保存します。

### 3. プッシュ・プルアドレスの取得
#### プッシュアドレス
プッシュアドレスは、Flow ManagementとInput Source Informationのページで取得できます。
Flow Managementからプッシュアドレスを取得します。
![](https://qcloudimg.tencent-cloud.cn/raw/685dd9818b72280ffc9d84cec9ab8c0a.png)
Input Source Informationからプッシュアドレスを取得します。
![](https://qcloudimg.tencent-cloud.cn/raw/2098e9e325b6673ded79ab6843b7ad75.png)

#### プルアドレス
プルアドレスは、以下のOutputリストページで取得できます。
![](https://qcloudimg.tencent-cloud.cn/raw/5f760430afe012ee26531294510de0bf.png)

### 4. Flowの開始
![](https://qcloudimg.tencent-cloud.cn/raw/d4e543da4000175587ec2d4d74e4775e.png)
ライブストリーミングイベントの開始時には、StreamLinkでFlowを開始する必要があります。

### 5. Flow設定の動的な変更
ライブストリーミング中に予期せぬ事態が発生し、Flowの設定を一時的に調整する必要がある場合、Flowを停止せずに直接操作することができます。
Input CIDR Allowiplistを変更します。
![](https://qcloudimg.tencent-cloud.cn/raw/c4c642e542beed25a7cd134600a3ba62.png)
Output CIDR Allowiplistを変更します。
![](https://qcloudimg.tencent-cloud.cn/raw/de4ce1df26d2bff4b0ca9ca7312a70ba.png)
いずれかのOutputを停止します。
![](https://qcloudimg.tencent-cloud.cn/raw/13b2a0fe21b9d528bdee155135da9b5d.png)
Outputを追加します。
![](https://qcloudimg.tencent-cloud.cn/raw/026591b6497dc6aa8411f3e19a2e42db.png)