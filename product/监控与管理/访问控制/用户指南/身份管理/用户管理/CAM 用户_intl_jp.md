CAMユーザーはTencent Cloudで作成したエンティティです。各CAMユーザーは、1つのTencent Cloudアカウントにのみ関連付けられています。登録したTencent Cloudアカウント身元は**メインアカウント**です。共同作業するために、[ユーザー管理](https://console.cloud.tencent.com/cam)を通して、さまざまな権限を持つ**サブアカウント**を作成することができます。サブアカウントのタイプは[サブユーザー](https://intl.cloud.tencent.com/document/product/598/13674)、[協力者](https://intl.cloud.tencent.com/document/product/598/13666)および[メッセージ受信者](https://intl.cloud.tencent.com/document/product/598/13667)に分けられます。

<table>
	<tr>
		<th rowspan="2">アカウントタイプ</th>
		<th rowspan="2">メインアカウント</th>
		<th colspan="3">サブアカウント</th>
	</tr>
	<tr>
		<th>サブユーザー</th>
		<th>協力者</th>
		<th>メッセージ受信者</th>
	</tr>
	<tr>
		<td>定義</td>
		<td>
					<ul>
						<li>Tencent Cloudのすべてのリソースを所有して、任意のリソースに自由にアクセスできます。</li>
						<li>メインアカウントを使用してリソースを操作することはお勧めできません。サブアカウントを作成して、最小限の重みでポリシーを割り当てる必要があります。限られた権限を持つサブアカウントでクラウドリソースを操作します。</li>
					</ul>
		</td>
		<td>メインアカウントによって作成して、サブユーザーを作成したメインアカウントに完全に帰属します。</td>
		<td>メインアカウントの身元を持ち、現在のメインアカウントの協力者として追加されると、現在のメインアカウントのサブアカウントの1つとなりますが、メインアカウント身元に戻すこともできます。</td>
		<td>メッセージ受信機能だけを持っています。</td>
	</tr>
	<tr>
		<td>コンソールアクセス</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>プログラミングアクセス</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>ポリシー承認</td>
		<td>デフォルトでは、すべてのポリシーが設定されています</td>
		<td>✔</td>
		<td>✔</td>
		<td>	- </td>
	</tr>
	<tr>
		<td>メッセージ通知</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
		<td>✔</td>
	</tr>
</table>


