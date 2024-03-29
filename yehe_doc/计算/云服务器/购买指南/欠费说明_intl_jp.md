## 従量課金CVMインスタンス

![](https://main.qcloudimg.com/raw/463d6b815dcf2677ebe28f9683d14430.jpg)

### 注意事項
- 従量課金リソースが使わなくなった場合は、引き続き課金されないように、**タイムリーにリソースを終了してください**。
- CVMインスタンスが終了または回収されると、そのデータは消去され、復元できなくなります。
- 実際のリソース消費量が刻一刻と移り変わっているため、残高不足アラートには若干差異が生じる場合がございます。

### アラート

<table>
	<tr><th>アラートタイプ</th><th>説明</th></tr>
	<tr><td><b> 支払い遅延のリマインダー</b></td><td>従量課金制のリソースは、時間単位で課金されます。アカウント残高がマイナスになっている場合は、メールやSMSでTencent Cloudアカウントの作成者、グロバールリソース協力者および財務協力者に通知します。</td></tr>
	<tr><td><b>支払い遅延のアラート</b></td><td>この機能はデフォルトで無効になっています。</td></tr>
</table>

### 支払遅延時のリスクと対処法
アカウントの残高が引き落とされてマイナスの値になった時点から、**2時間以内**にCVMインスタンスを引き続き使用し、通常どおり課金されます。2時間後、アカウントの残高がマイナスのままである場合、CVMインスタンスは自動的にシャットダウンされ、課金が停止されます。
自動シャットダウン後、CVMインスタンスは次の段階を経ます。
<table>
	<tr><th>自動シャットダウン後の経過時間</th><th>説明</th></tr>
	<tr><td rowspan=2><b>≤ 15日</b></td><td>アカウントの残高がプラスになると、課金が再開され、CVMインスタンスを引き続き使用できます。</td></tr>
	<tr><td>アカウントの残高がマイナスのままである場合は、CVMインスタンスを起動できません。</td></tr>
	<tr><td><b>＞ 15日</b></td><td>アカウントのマイナス残高の状態が15日を超えて継続する場合には、従量課金CVMインスタンスが回収されます。インスタンス中のすべてのデータが消去され、復元できなくなります。CVMインスタンスが回収されると、Tencent Cloudアカウントの作成者とすべての協力者にメールとSMSで通知されます。</td></tr>
</table>

## 利用したトラフィック量に応じて課金されるネットワーク
<table>
	<tr><th>アラートタイプ</th><th>説明</th></tr>
	<tr><td><b>残高アラート</b></td><td>トラフィックの変動が大きくて予測しにくいため、システムは残高アラート機能を提供していません。</td></tr>
	<tr><td><b>支払い遅延のアラート</b></td><td>アカウントの残高が引き落とされてマイナスの値になった時点から、トラフィックによって課金するネットワークが<b>2時間以内に<b>利用可能であり、アカウントが引き続き課金されます。2時間後、アカウントの残高がマイナスのままである場合、サービスは自動的に停止します。</br>アカウントの残高がプラスになると、サービスを再開します。</td></tr>
</table>

>! トラフィック料金の詳細については 、[パブリックネットワークの課金方法](https://intl.cloud.tencent.com/document/product/213/10578)をご参照ください。
>
