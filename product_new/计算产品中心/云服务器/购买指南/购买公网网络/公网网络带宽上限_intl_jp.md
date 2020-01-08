## アウトバウンド帯域幅上限（ダウンストリーム帯域幅）

設定したパブリックネットワーク帯域幅の上限は、デフォルトでアウトバウンド帯域幅の上限です。つまり、CVMから送信した帯域幅です。パブリックネットワークの帯域幅上限は、さまざまなネットワーク課金モードに応じて異なります。具体的な情報は以下のようになります：
- 2019年5月31日までに以下の規則に従って実行してください：
<table>
<tr><th rowspan="2">ネットワーク課金モード</th><th colspan="2">インスタンス</th><th rowspan="2">設定可能な帯域幅の上限範囲（Mbps）</th></tr>
<tr><th>インスタンス課金モード</th><th>インスタンス構成</th></tr>
<tr><td>トラフィックによって課金する</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅によって課金する</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅</td><td colspan="2">ALL</td><td>0 - 200或は無制限の速度</td></tr>
</table>

- 2019年5月31日以降、以下の規則に従って実行してください：
<table>
<tr><th rowspan="2">ネットワーク課金モード</th><th colspan="2">インスタンス</th><th rowspan="2">設定可能な帯域幅の上限範囲（Mbps）</th></tr>
<tr><th style="width: 18.5607%;">インスタンス課金モード</th><th style="width: 24.5814%;">インスタンス構成</th></tr>
<tr><td>トラフィックによって課金する</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅によって課金する</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅</td><td colspan="2">ALL</td><td>0 - 200或は無制限の速度</td></tr>
</table>


## インバウンド帯域幅上限（アップストリーム帯域幅）

パブリックネットワークのインバウンド帯域幅は、CVMインスタンスに受信する帯域幅を指します。
- ユーザーが購入した固定帯域幅が10Mbpsを超える場合、Tencent Cloudは購入した帯域幅と同じの外部ネットワーク着信帯域幅をアサインします。
- ユーザーが購入した固定帯域幅が10 Mbps未満の場合、Tencent Cloudは10Mbpsの外部ネットワークの受信帯域幅をアサインします。

## 帯域幅制限を増やす

実際のニーズに応じて、異なる調整方法を選択します：
- [インスタンスの課金モードを調整する](#AdjustInstanceMode)
- [ネットワーク課金モードを調整する（帯域幅によって課金する）](#AdjustNetworkModeByBandwidth)
- [ネットワーク課金モードを調整する（帯域幅パケットによって課金する）](#AdjustNetworkModeByBandwidthPackage)

インスタンスとネットワークの課金モードを調整できない場合は、[作業依頼書を提出](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM&step=1)して帯域幅上限を増やすことを申請すると、評価した後すぐにフィードバックします。

<span id="AdjustInstanceMode"></span>
### インスタンス課金モードを調整する

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 帯域幅を調整する必要があるインスタンスを見つけて、右側の【もっと】> 【リソースの調整】> 【ネットワークの調整】をクリックします。
3. ポップアップの「ネットワークの調整」ウィンドウで、ターゲット帯域幅の上限を調整し、【OK】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/853916b57df665bc5e1ee1e322ff0d92.png)

<span id="AdjustNetworkModeByBandwidth"></span>
### ネットワーク課金モードを調整する（帯域幅によって課金する）

1. トラフィックによって課金するインスタンスを帯域幅によって課金するように調整します、操作の詳細については、[ネットワーク構成を調整する](https://intl.cloud.tencent.com/document/product/213/15517)をご参照ください。
2. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
3. 帯域幅を調整する必要があるインスタンスを見つけて、右側の【もっと】> 【リソースの調整】> 【ネットワークの調整】をクリックします。
4. ポップアップの「ネットワークの調整」ウィンドウで、ターゲット帯域幅の上限を調整し、【OK】をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/9371e74fc8a2816390a872fcbb46e4fa.png)

<span id="AdjustNetworkModeByBandwidthPackage"></span>
### ネットワーク課金モードを調整する（帯域幅パケットによって課金する）

1. トラフィックによって課金するインスタンスを帯域幅パケットによって課金するように調整します。
> 帯域幅パッケージ内のインスタンスは、帯域幅を無制限に調整することをサポートします。[帯域幅パッケージを申請するのをここをクリックしてください](https://cloud.tencent.com/act/apply/bwp_apply)。
>
2. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
3. 帯域幅を調整する必要があるインスタンスを見つけて、右側の【もっと】> 【リソースの調整】> 【ネットワークの調整】をクリックします。
4. ポップアップボックスでネットワークを調整し、ターゲット帯域幅を調整して、【OK]をクリックします。下図に示すように：
![](https://main.qcloudimg.com/raw/b05d6c586d2d21b75d83df8d71fe3873.png) 

