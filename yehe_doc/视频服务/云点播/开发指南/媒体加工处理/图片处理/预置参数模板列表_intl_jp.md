VODでは、画像処理を開始するための複雑なパラメータセットの代わりにパラメータテンプレートを使用できます。さまざまな処理シナリオに応じて、一連のプリセットパラメータテンプレートを提供します。

## 画像のリアルタイム処理
1つの画像リアルタイム処理テンプレートは1組の順序立った操作の集合を表します。

### プリセット画像リアルタイム処理テンプレート

<table>
    <tr>
        <th>
            テンプレートID                
        </th>
				<th>
           操作説明
        </th>
        <th>
            操作パラメータ
        </th>
    </tr>
 <tr>
        <td>
            10
        </td>
				<td>
            トリミング
        </td>
        <td>
            <li>タイプ：矩形トリミング</li>
						<li>幅：360px</li>
						<li>高さ：200px</li>
				</td>
 </tr>
 <tr>
        <td>
            20
        </td>
				<td>
            トリミング
        </td>
        <td>
            <li>タイプ：矩形トリミング</li>
						<li>幅：200px</li>
						<li>高さ：400px</li>
				</td>
 </tr>
 <tr>
        <td>
            30
        </td>
				<td>
            サムネイル
        </td>
        <td>
            <li>タイプ：短辺を指定し、長辺は同じ比率でズーム</li>
						<li>短辺：320px</li>
				</td>
 </tr>
 <tr>
        <td>
            40
        </td>
				<td>
            サムネイル
        </td>
        <td>
            <li>タイプ：幅、高さを強制指定</li>
						<li>幅：200px</li>
						<li>高さ：200px</li>
				</td>
 </tr>
 <tr>
        <td rowspan="2">
            50
        </td>
				<td rowspan="2">
            先にサムネイル作成、後からトリミング
        </td>
        <td>
				サムネイル：
            <li>タイプ：短辺を指定し、長辺は同じ比率でズーム</li>
						<li>短辺：320px</li>
				</td>
 </tr>
 <tr>
        <td>
				トリミング：
            <li>タイプ：矩形トリミング</li>
						<li>幅：200px</li>
						<li>高さ：200px</li>
				</td>
 </tr>
</table>

## 画像審査

### プリセット画像審査テンプレート

|  テンプレートID | ポルノ（Porn）  | 暴力・テロ（Terror） |
|---|---|---|
| 10 |  はい | はい |
