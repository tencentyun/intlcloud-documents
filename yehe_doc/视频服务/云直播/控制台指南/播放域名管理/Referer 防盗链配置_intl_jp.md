Refererホットリンク防止の設定により、Refererブラック/ホワイトリストとルール内容をカスタマイズし、再生リクエストを許可または拒否し、ライブストリーミングコンテンツを保護します。同時に、Cloud Streaming Servicesは、空のRefererアクセスを許可するかどうか、ユーザーが選択できるようにします。

## 設定の原理

HTTPプロトコルでサポートされるRefererメカニズムに基づき、Refererホットリンク防止は、HTTPリクエストにともなうRefererフィールドを介してリクエストのソースを識別し、アクセスの合法性を検証し、ライブストリーミングコンテンツのリクエストを許可または拒否します。

## 注意事項
- Referer情報はHTTP中に含まれており、RTMP、WebRTCおよびQUICなどの非HTTPプロトコルはReferer設定による制限を受けません。RTMPを制限したい場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してオフラインでの修正についてお問い合わせください。
- Refererホットリンク防止の設定をオン、オフ、または修正後は、約15分～20分経過すると有効となり、再度プッシュする必要はありません。
- Refererホットリンク防止は、HTTPリクエストのheaderの中のReferer情報を検証することで、リクエストの合法性を確認し、ライブストリーミングの可否を制御しますが、Refererの偽造によって検証を回避し、サービスが盗用される可能性があります。従って、業務においてRefererに強く依存しコンテンツを保護することはお勧めしません。

## 前提条件

- CSSサービスがアクティブになっており、かつ[CSSコンソール](https://console.cloud.tencent.com/live/livestat)にログインしていること。
- [再生ドメイン名を追加](https://intl.cloud.tencent.com/document/product/267/35970)済みであること。

[](id:open)

## Refererホットリンク防止の起動

1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**を選択し、Refererホットリンク防止を設定したい**再生ドメイン名** または右側の**管理**をクリックして、ドメイン名管理ページに入ります。
2.  **アクセス制御**>**Refererホットリンク防止の設定**にある**編集**をクリックして、Refererホットリンク防止設定ページに進みます。
 ![](https://main.qcloudimg.com/raw/32461edf0353c2c95925b74d80dc25b3.png)
3. ![](https://main.qcloudimg.com/raw/c032c517e25867ff592f128424154688.png)ボタンをクリックして、Refererホットリンク防止の有効化を選択し、次の設定を行います。
 ![](https://main.qcloudimg.com/raw/551044de4acd79683ae69cf106a87c0b.png)

<table id="setmess">
<tr><th width="14%">設定項目</th><th>説明</th>
</tr><tr>
<td>ホットリンク防止タイプ</td>
<td>Referer <b>ブラックリスト</b>または<b>ホワイトリスト</b>の設定をクリックして選択：
<ul style="margin:0">
<li>ブラックリストとホワイトリストは相互に排他的であり、同一時間では一方のみが有効になります。</li>
<li>Refererホワイトリストが設定されている場合、ホワイトリスト内のユーザーのアクセスが許可され、ライブストリーミングコンテンツをリクエストすることができます。ホワイトリスト外のユーザーのアクセスは拒否され、ライブストリーミングコンテンツをリクエストすることはできません。<li>
<li>Refererブラックリストが設定されている場合、ブラックリスト内のリクエストソースのアクセスが拒否され、ライブストリーミングコンテンツをリクエストすることはできません。ブラックリスト外のユーザーのアクセスは許可され、ライブストリーミングコンテンツをリクエストすることができます。</li>
</ul></td>
</tr><tr>
<td>空のRefererを許可</td>
<td><ul style="margin:0">
<li>許可を選択した場合、HTTPリクエストのRefererフィールドがブランクまたはフィールドなしのアクセスが許可され、ブラウザを介してライブストリーミングURLに直接アクセスできるようになります。</li>
<li>許可を選択しない場合、空のRefererアクセスは拒否されます。</li>
</ul></td>
</tr><tr>
<td>ホットリンク防止のルール</td>
<td><ul style="margin:0">
<li>最大<b>100</b>個のルールに対応します。改行コードで区切ってください。 </li>
<li><b>IP</b>と<b>ドメイン名</b>の2種類の入力フォーマットをサポートします。実際のマッチングの際は、パスプレフィックスマッチング（ドメイン名とIP）、ワイルドカードマッチング（汎ドメイン名）に対応します。例：<ul>
<li/><code>101.1.0.1</code>と<code>www.test.com</code>を設定すると、<code>101.1.0.1/157</code>と<code>www.test.com/tencent</code> がいずれも有効になります。
<li/><code>*.test.com</code>を設定すると、<code>www.test.com</code>と<code>a.test.com</code> がいずれも有効になります。</ul></li>
<li>ルール内容がブランクの場合は、ブラックリスト/ホワイトリストがいずれも設定されていないことを表します。</li>
</ul></td>
</tr></table>

4. **保存**をクリックすると、設定が保存されます。


[](id:change)
## Refererホットリンク防止の修正
1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**を選択し、Refererホットリンク防止設定を修正したい**再生ドメイン名** または右側の**管理**をクリックして、ドメイン名管理ページに入ります。
2.   **アクセス制御**>**Refererホットリンク防止の設定**にある**編集**をクリックして、Refererホットリンク防止設定ページに進みます。
3. 実際のニーズに応じて、[設定項目](#setmess)情報を修正し、**保存**をクリックすれば修正が完了します。

![](https://main.qcloudimg.com/raw/a8c79376ed22b4e47f35e69411c6df10.png)

[](id:close)
## Refererホットリンク防止の停止
[Refererホットリンク防止の起動](#open)後、この機能を停止する必要がある場合、具体的な操作は以下のとおりです。

1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**を選択し、Refererホットリンク防止設定を無効化したい**再生ドメイン名** または右側の**管理**をクリックして、ドメイン名管理ページに入ります。
2.   **アクセス制御**>**Refererホットリンク防止の設定**にある**編集**をクリックして、Refererホットリンク防止設定ページに進みます。
3.   ![](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png)ボタンをクリックし、Refererホットリンク防止の停止を選択します。
4. **保存**をクリックして完了です。

![](https://main.qcloudimg.com/raw/eb36bc40cca9f19e198fc742256fed21.png)






