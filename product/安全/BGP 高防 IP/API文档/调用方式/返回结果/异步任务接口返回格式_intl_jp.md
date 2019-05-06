

新しいバージョンのAPI（現在のところCVMなどの一部のサービスのみ利用可能）には非同期タスクAPIの概念的な定義がありません。具体的な使用方法は各Actionドキュメントで紹介します。

## 通常非同期APIの戻り形式
一回のリクエストに1つのリソースしか操作できない非同期タスクAPI。例えば、CLBの作成、CVMオペレーティングシステムのリセットなど。

<table>
   <tr>
      <th>名称</th>
      <th>タイプ</th>
      <th>説明</th>
      <th>必須</th>
   </tr>
   <tr>
      <td>code</td>
      <td>Int</td>
      <td>返された結果のエラーコード、0が成功、他の値が失敗を示します。</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>返された結果のエラーメッセージ</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>requestId</td>
      <td>String</td>
      <td>タスク番号</td>
      <td>はい</td>
   </tr>
</table>

## 一括非同期タスクAPIの戻り形式
一回のリクエストに複数のリソースを操作できる非同期タスクAPI。例えば、パスワード変更、マシンの起動、マシンの停止など。

<table>
   <tr>
      <th>名称</th>
      <th>タイプ</th>
      <th>説明</th>
      <th>必須</th>
   </tr>
   <tr>
      <td>code</td>
      <td>Int</td>
      <td>返された結果のエラーコード、0が成功、他の値が失敗を示します。</td>
      <td>はい</td>
   </tr>
   <tr>
      <td>message</td>
      <td>String</td>
      <td>返された結果のエラーメッセージ</td>
      <td>いいえ</td>
   </tr>
   <tr>
      <td>detail</td>
      <td>Array</td>
      <td>リソースIDをkeyとして、リソース操作のcode、message、requestIdを返します</td>
      <td>はい</td>
   </tr>
</table>

例えば：

```
{
	"code": 0,
	"message": "success",
	"detail": {
		"qcvm6a456b0d8f01d4b2b1f5073d3fb8ccc0": {
			"code": 0,
			"message": "",
			"requestId": "1231231231231"
		}
	}
}
```
>!
>- すべてのリソースが正常に操作した場合、最も外側のcodeは0です。
>- すべてのリソースの操作が失敗した場合、最も外側のcodeは5100を返します。
>- 一部のリソースの操作が失敗した場合、最も外側のcodeは5400を返します。この場合、端末は故障箇所の操作情報をdetailによって取得することができます。

