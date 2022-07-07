遅延設定とは、そのドメイン名に対するCSSストリームをHLS形式で再生することで、異なる分割時間および数量を設定して再生の遅延を調整することを言います。業務上の必要性に応じて適切な遅延を設定してください。低遅延にすると、同時にライブストリーミングのラグが生じる可能性があります。

## 前提条件
- CSSサービスがアクティブになっており、かつ[CSSコンソール](https://console.cloud.tencent.com/live/livestat)にログインしていること。
- [プッシュドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加済みであること。


## 遅延設定
1. [ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)を選択し、HLS遅延設定を行いたい**プッシュドメイン名**または右側の**管理**をクリックして、ドメイン名管理ページに進みます。
2. **高度な設定**でHLSの遅延設定を行うことができます。
3. 適切な遅延パラメータを選択します。GOPはHLSの分割時間に影響します。プッシュGOPを1s～2sに設定することをお勧めします。
4. GOPが2sの場合、各設定の想定遅延時間は次のようになります。
<table>
<thead>
<tr>
<th>遅延設定</th>
<th>高</th>
<th>中</th>
<th>低</th>
</tr>
</thead>
<tbody><tr>
<td>遅延予測</td>
<td>20s - 25s</td>
<td>10s - 15s</td>
<td>6s - 8s</td>
</tr>
</tbody></table>

<img src="https://qcloudimg.tencent-cloud.cn/raw/3032e36b30c1a966f5db814f19635612.png">
