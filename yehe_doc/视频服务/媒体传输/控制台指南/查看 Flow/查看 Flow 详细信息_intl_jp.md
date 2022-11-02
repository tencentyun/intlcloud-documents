コンソールの[Flow Management](https://console.tencentcloud.com/mdc/flow)ページに進み、リスト内のいずれかのFlowをクリックすると、そのFlowの詳細情報を確認できます。

![](https://qcloudimg.tencent-cloud.cn/raw/8761f3d6e89cd2ef43c7a1531baceeb0.png)

## 基本情報 Information
![](https://qcloudimg.tencent-cloud.cn/raw/849236bd82f00c864ec0ba5a4a8e03bc.png)
**Information**では、Flow ID、Flow Name、Input Region、現在の状態および最大帯域幅を確認できます。

## 入力ソース情報 Input Source
![](https://qcloudimg.tencent-cloud.cn/raw/08335f06efbb8d4699a50b1acd7f86b5.png)
**Input Source**では、Input Source Name、Inputアドレス、ホワイトリストの設定およびプロトコル関連の設定を確認できます。

#### 出力情報 Output
![](https://qcloudimg.tencent-cloud.cn/raw/900b528fbc1d55552c7c520d74c18a7a.png)
**Output**では、選択したすべてのOutputを確認でき、リストには次の事項が表示されます。

- **Name**：Outputの名前です。
- **Output ID**：OutputのIDです。
- **Output Region**：Outputのあるリージョンで、Flowはこのリージョンにストリームを伝送します。
- **Output IP**：Output出力ノードのIPアドレスです。
- **Protocol**：Outputの出力プロトコルです。
- **URL**：Outputがプルをサポートしている場合、プルアドレスは以下から取得できます。

またこのページでは、Outputsの作成、編集、削除などの操作を行うことができます。

## ログ情報 Log
![](https://qcloudimg.tencent-cloud.cn/raw/2ed506e30a7bf706805ae2d29986454b.png)
**ログ**では、プッシュ、中断、IPホワイトリストで拒否されたプルなど、Flow実行中のさまざまなイベントに関する情報を確認できます。

## ヘルス情報 Health
フレームレートやビットレートなど、現在のストリームの指標を確認できます。
### ソース Input Source
直近の過去1時間のプッシュとプルの品質を確認できます。また、時間選択ウィンドウで他の時間帯を選択すると、他の時間帯の品質情報も確認できます。
![](https://qcloudimg.tencent-cloud.cn/raw/f4f10f4d37873fce43c3d88def9eaef0.png)

VideoとAudioカーブでは、対応するボタンをクリックすることで、ビットレートまたはフレームレートいずれかの表示を選択できます。複数のオーディオがある場合、ドロップダウン選択ボックスで異なるオーディオを選択すると、そのビットレートまたはフレームレートを確認できます。
![](https://qcloudimg.tencent-cloud.cn/raw/ef3502d0afb338f4c64b673379dd25cf.png)

SRTプロトコルの場合、ページの一番下で次のようなSRTのリンク品質を確認することもできます。
- **Paket Loss rate**：SRTリンクのパケットロス率は、リンクの安定性を判断することのできる指標であり、パケットロス率が20%未満であれば、通常、正常でスムーズな伝送が可能です。
- **Retransmission Rate**：SRリンクの再送率は、再送率がパケットロス率よりはるかに低い場合、リンクに異常があることを意味します。このような場合、CSSストリームにはラグが発生し、中断することもあります。
- **RTT**：RTTはリンク遅延を判断するために使用され、RTTが高いほどリンク遅延が大きく、SRTのLatencyも高く設定する必要があります。Latencyは通常、RTTの4倍が推奨されます。RTTカーブの振れが非常に激しい場合、リンクの品質が不安定であることを意味し、極端な場合には、深刻なパケットロスにつながる可能性もあります。
- **Number Of Dropped Packtes**：SRTプロトコルスタックは、現在のパケットの遅延が設定されたLatencyを超えたため、再度伝送しても意味がないと判断し、自発的にパケットをドロップします。このようなパケットロスが発生した場合、通常、画面表示の障害が発生します。これはプッシュ側の帯域幅が不足しているか、リンクのRTTが高すぎるため、Latencyを大きくする必要があることを意味します。

![](https://qcloudimg.tencent-cloud.cn/raw/720784ac0a25685da1c75d8a1aeeaea1.png)

### 出力 Output
Outputの情報はInputとほぼ同じですが、Outputが大量に存在する可能性があるため、検索ボックスで確認したいOutputを選択できます。
![](https://qcloudimg.tencent-cloud.cn/raw/2563d297d6ee371f8f31b3010578a8b9.png)