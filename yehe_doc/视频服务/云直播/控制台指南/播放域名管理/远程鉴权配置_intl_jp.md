リモート認証とは、Tencent Cloudストリーミングプッシュ/再生リンク不正アクセス防止の認証を通った後、顧客の業務サーバーのインターフェースを呼び出し、リクエストを顧客の業務サービスに転送し、顧客がリクエストの正当性を判断し判断結果をTencent Cloudに返し、Tencent Cloudで返された判断結果によって、再生を許可または拒否する処理を実行することです。お客様自身でリモート認証サーバーを開発して指定する必要があり、この認証サーバーはユーザーのリクエストを検証することに使用され、より正確な認証を実装し、ライブブロードキャストの安全性を確保します。

## フロー説明
リモート認証の処理フローは以下のとおりです：
![](https://qcloudimg.tencent-cloud.cn/raw/e0b53fa1bccc5cf193df5312a3b1fa3a.png)

| 番号 | 説明                                                         |
| ---- | ------------------------------------------------------------ |
| 1    | エンドユーザーはリクエストをCSSサービスに発行します。                               |
| 2    | CSSはリクエストに対応するドメイン名に対してリモート認証が設定されているかを判断します。リモート認証が設定されているた場合、リモート認証の設定に基づいてリクエストを処理し、顧客のリモート認証サーバーに転送します。|
| 3    | 顧客のリモート認証サーバーは認証結果を返します。HTTPステータスコードは、パスの場合は200、ブロックの場合は403です。|
| 4    | CSSは認証結果によってユーザーのリクエストに応答するかを判断します。           |

##  前提条件
- CSSサービスがアクティブになっており、かつ[CSSコンソール](https://console.cloud.tencent.com/live/livestat)にログインしていること。
- [再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加済み。

## リモート認証の設定
1.CSSコンソールにログインし、[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)を選択し、リモート認証を設定する**再生ドメイン名**または右側の**管理**をクリックし、ドメイン名管理ページに進みます。
2.**アクセス制御** > **リモート認証**で、リモート認証を有効/無効にすることができます。
<img src="https://qcloudimg.tencent-cloud.cn/raw/73648ec779caa4cc2be1be8a7c88931b.png" width=800>
3.![](https://qcloudimg.tencent-cloud.cn/raw/b64d8a4343b3a1e340db3adb9002db60.png)ボタンをクリックし、リモート認証を有効にし、以下のように設定します：<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/86867489b1dc604cdd7c4bd5bc4ed3e1.png" width=800>

<table>
<thead><tr><th width="20%">設定項目</th><th>説明</th></tr></thead>
<tbody><tr>
<td>リモート認証アドレス</td>
<td>リモート認証アドレスは顧客側のリモート認証サーバーのアドレスであり、必須です。ルールは<code>http(s)://+ドメイン名またはIP+ポート+パス</code>です。</td>
</tr><tr>
<td>リクエスト方法</td>
<td>デフォルトではPOSTが選択されます。HEADまたはGETを選択できます。</td>
</tr><tr>
<td>URL認証パラメータ：パラメータ設定を残します</td>
<td>デフォルトではすべてのパラメータを残します。指定したパラメータを残すこと、または、すべてのパラメータを削除することを選択できます。<ul style="margin:0">
<li>指定したパラメータを残すことを選択した場合、入力ボックスに残すパラメータを入力する必要があります。現在、中国語はサポートされていません。パラメータが複数ある場合、 | で区切る必要があります。例：<code>value1|value2</code>。</li>
<li>認証パラメータは大文字と小文字を区別します。keyとKEYは2つの異なるパラメータとして認識されます。</li>
</ul></td>
</tr><tr>
<td>URL認証パラメータ：カスタムパラメータを追加します</td>
<td>クリックして追加します。パラメータを選択するか、パラメータをカスタマイズすることができます。（最大で50個のパラメータを追加できます）<ul style="margin:0">
<li>パラメータの選択は、host、uri、client_ip、およびcdn_ipパラメータの選択をサポートします。これらのパラメータは、再生ドメイン名、元のURLのリクエスト、クライアントIPのリクエスト、およびCDN側IPのリクエストを表します。</li>
<li>カスタムを選択する場合、パラメータと値の入力ボックスは必須です。現在、中国語はサポートされていません。URL認証パラメータは大文字と小文字を区別します。keyとKEYは2つの異なるパラメータとして認識されます。</li>
</ul></td>
</tr><tr>
<td>リクエストヘッダー認証パラメータ：パラメータ設定を残します</td>
<td>デフォルトではすべてのパラメータを残します。指定したパラメータを残すこと、または、すべてのパラメータを削除することを選択できます。<ul style="margin:0">
<li>指定したパラメータを残すことを選択した場合、入力ボックスに残すパラメータを入力する必要があります。現在、中国語がサポートされていません。パラメータが複数ある場合、 | で区切る必要があります。例：<code>value1|value2</code>。</li>
<li>リクエストヘッダーパラメータに「すべてのパラメータを残す」を指定した場合、CDNノードはデフォルトでHOSTヘッダーを削除します。HOSTヘッダーを残す必要がある場合、「指定したパラメータを残す」または「カスタムパラメータを追加する」を使用して残すことができます。</li>
<li>認証パラメータは大文字と小文字を区別しません。</li>
</ul></td>
</tr><tr>
<td>リクエストヘッダー認証パラメータ：カスタムパラメータを追加します</td>
<td>クリックして追加します。パラメータを選択するか、パラメータをカスタマイズすることができます。（最大で50個のパラメータを追加できます）<ul style="margin:0">
<li>パラメータの選択は、User-Agent、Referer、およびX-Forwarded-Forパラメータの選択をサポートします。これらのパラメータは、ユーザーが使用するシステムとブラウザの情報、指定されたWebページのリダイレクトパス、偽装アクセスリンクを表します。</li>
<li>カスタムを選択する場合、パラメータと値の入力ボックスは必須です。現在、中国語はサポートされていません。リクエストヘッダー認証パラメータは大文字と小文字を区別しません。</li>
</ul></td>
</tr><tr>
<td>1回の認証リクエストのタイムアウト時間（ms）</td>
<td>必須。デフォルトでは3000msとします。500～3000を指定できます。</td>
</tr><tr>
<td>タイムアウト再試行回数</td>
<td>デフォルトでは1回とします。0～3回を指定できます。</td>
</tr><tr>
<td>タイムアウトの場合の処理</td>
<td>デフォルトではパスです。ブロックがサポートされています。1回の認証リクエストのタイムアウト時間×（リトライ回数+1）経過しても明確なレスポンス結果（HTTPステータスコードが<code>200</code>または<code>403</code>）を受信しない場合、システムは設定されたタイムアウト実行アクションを実行します。</td>
</tr></tbody></table>

4. **保存**をクリックすると設定が保存されます。

## リモート認証の変更
1.CSSコンソールにログインし、[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)を選択し、リモート認証を設定する**再生ドメイン名**または右側の**管理**をクリックし、ドメイン名管理ページに進みます。
2.**アクセス制御** > **リモート認証**で、編集をクリックしてリモート認証の設定ページに進みます。
3. 実際の必要に応じて、設定項目情報を変更し、保存をクリックして変更を完了できます。

<img src="https://qcloudimg.tencent-cloud.cn/raw/30044c0f1f3cb90cd5f8024e01a5efc8.png" width=800>

## リモート認証の無効化
1.CSSコンソールにログインし、[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)を選択し、リモート認証を無効にする**再生ドメイン名**または右側の**管理**をクリックし、ドメイン名管理ページに進みます。
2.**アクセス制御** > **リモート認証**で、![img](https://main.qcloudimg.com/raw/e72f89a0deb6858428dc3e93ce7e7088.png)ボタンをクリックして、リモート認証を無効にします。