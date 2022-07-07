業務上の必要性に応じて適切な遅延を設定してください。低遅延にすると、同時にライブストリーミングのラグが生じる可能性があります。

## 前提条件
- CSSサービスがアクティブになっており、かつ[CSSコンソール](https://console.cloud.tencent.com/live/livestat)にログインしていること。
- [再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加済みであること。


## 遅延設定
1. [ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)を選択し、RTMPおよびFLV遅延設定を行いたい**再生ドメイン名**または右側の**管理**をクリックして、ドメイン名管理ページに進みます。
2. **高度な設定**でRTMPおよびFLVの遅延設定を行うことができます。
3. 適切な遅延パラメータを選択します。プッシュGOPを1s～2sに設定することをお勧めします。GOP値が大きくなるほど、遅延が大きくなります。
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
<td>7s - 9s</td>
<td>5s - 7s</td>
<td>4s -5s</td>
</tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/49744a600f2e1101a9261a0205b5e651.png">

