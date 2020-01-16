
<span id = "celueyufa"></span>
### ポリシー文法
CAMポリシー：

```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 

```
- **バージョンversion**は記入必須項目であり、現時点で数値が"2.0"であることのみを認めています。
- **ステートメント statement** は一つか複数の権限の詳細情報を説明することに使われています。当該要素は effect、action、resource，condition 等幾つかのほかの要素の権限又は権限の集合を含んでいます。一つのポリシーには一つのstatement 要素しかありません。
 1. **操作action**は許可する又は拒否する操作を説明することに使われています。操作は API（nameプリフィックスで説明する）又は機能セット（特定APIセットであり、permidプリフィックスで説明する）であってよいです。当該要素は記入必須項目です。
 2. **リソースresource** は授権するの具体的なデータを説明することに使われています。リソースは6段階式で説明されます。各製品のリソース定義の詳細は異なっています。リソースの指定方法については、作成したリソース宣言に対応する製品ドキュメントをご参照ください。当該要素は記入必須項目です。
 3. **発効条件condition** はポリシー発効の制約条件を説明しています。条件はオペレーター、操作キーと操作値から構成されています。条件値は時間、IPアドレス等の情報を含んでいます。一部のサービスは、条件に対しほかの値を指定することを認めています。当該要素は記入必須項目ではありません。
 4. **影響effect** は宣言による結果が「許可」であるか「明示的な拒否」であるかを説明しています。それにallow (許可)とdeny (明示的な拒否)という2種類が含まれています。当該要素は記入必須項目です。

<span id = "caozuo"></span>
### CVMの操作

CAポリシーステートメントでは、顧客はCAM対応のいかなるサービスから任意のAPI操作を指定することができます。CVMに対しては、name/cvm:をプレフィックスとするAPIを利用してください。例えば name/cvm:RunInstances 又は name/cvm:ResetInstancesPasswordです。
一つのステートメントで複数の操作を指定したい場合は、コンマで区切ってください。下記の通りです。
```
"action":["name/cvm:action1","name/cvm:action2"]
```
ワイルドカードで複数の操作を指定することも可能です。例えば、先頭が単語" Describe "であるすべての操作を指定することが可能です、下記の通りです。
```
"action":["name/cvm:Describe*"]
```
CVMにおけるすべての操作を指定したい場合は、 * ワイルドカードを使用してください。下記の通りです。
```
"action"：["name/cvm:*"]
```

<span id = "ziyuanlujing"></span> 
### CVMのリソースパス
各CAMポリシーステートメントは自身に適用されるリソースがあります。
リソースパスの一般的な形式は次のとおりです。
```
qcs:project_id:service_type:region:account:resource
```
**project_id**：プロジェクト情報を説明します。CAMの早期ロジックをコンパチブルするためなものだけです。記入する必要がありません。
**service_type**：製品の略称です、例えば CVMです。
**region**：リージョン情報です、例えば bjです。
**account**：リソース所有者のルートアカウント情報です、例えばuin/164256472です。
**resource**：各製品の具体的なリソース詳細です。例えばinstance/instance_id1 又は instance/*です。

例えば、顧客は特定インスタンス (i-15931881scv4) を使用してステートメントでそれを指定することができます。下記の通りです。
```
"resource":[ "qcs::cvm:bj:uin/164256472:instance/i-15931881scv4"]
```
 * ワイルドカードで特定アカウントのすべてのインスタンスを指定することができます。下記の通りです。
```
"resource":[ "qcs::cvm:bj:uin/164256472:instance/*"]
```

すべてのリソースを指定したい場合、或いは特定のAPI操作がリソースレベルの権限をサポートしていない場合、 Resource 要素の中で* ワイルドカードを使ってください。下記の通りです。
```
"resource": ["*"]
```
一つのコマンドで複数のリソースを同時に指定したい場合は、コンマでそれらを区切ってください。下記は二つのリソースを指定する例です。
```
"resource":["resource1","resource2"]
```
下表にはCVMの利用可能なリソース及び対応するリソースの説明方法が示されています。
<style>
table th:nth-of-type(1){
width:250px;
}
table th:nth-of-type(2){
width:500px;
}
</style>
下表においては、$をプレフィックスとする単語はエイリアスです。
- その中に、projectはプロジェクトIDを指しています。
- その中に、regionはリージョンを指しています。
- その中に、accountはアカウントIDを指しています。

| リソース | 授権ポリシーにおけるリソースの説明方法 |
|-------|-------|
|インスタンス|  qcs::cvm:$region:$account:instance/$instanceId|
|キー|  qcs::cvm:$region:$account:keypair/$keyId|
|VPC|  qcs::vpc:$region:$account:vpc/$vpcId|
|サブネット|   qcs::vpc:$region:$account:vpc/$vpcId|
|システムディスク|  qcs::cvm:$region:$account:systemdisk/*|
|イメージ|   qcs::cvm:$region:$account:image/*|
|サブネット|  qcs::vpc:$region:$account:subnet/$subnetId|
|データディスク|  qcs::cvm:$region:$account:datadisk/*|
|セキュリティグループ|  qcs::cvm:$region:$account:sg/$sgId|
|EIP|  qcs::cvm:$region:$account:eip/*|

 

<span id = "tiaojianmiyue"></span>
### CVMの条件キー
ポリシーステートメントでは、ポリシーの発効時間を制御する条件を選択的に指定することができます。各条件には一つか複数のキー値ペアが含まれています。条件キーは大文字・小文字の区分けをしません。

- 顧客は複数の条件、或いは単一の条件で複数のキーを指定する場合は、ANDロジック操作によりそれを評価します。
- 単一の条件で複数の値を持つキーを指定する場合は、ORロジック操作によりそれを評価します。すべての条件にマッチングした場合にのみ、権限を与えます。
下表にはCVMが指定のサービスに使われる条件キーを説明しています。
<table class="tableblock frame-all grid-all spread">
<colgroup>
<col style="width: 25%;">
<col style="width: 25%;">
<col style="width: 50%;">
</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">条件キー</th>
<th class="tableblock halign-left valign-top">参照タイプ</th>
<th class="tableblock halign-left valign-top">キー/値ペア</th>
</tr>
</thead>
<tbody>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type=<code>instance_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>その中に<code>instance_type</code> はインスタンスタイプを指しています（例えば S1.SMALL1）。</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type=<code>image_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>その中に<code>image_type</code> はイメージタイプを指しています（例えば IMAGE_PUBLIC）</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>その中に<code>region</code> はリージョンを指しています（例えば ap-guangzhou）</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>Integer</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size=<code>disk_size</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>その中に<code>disk_size</code> はディスクサイズを指しています（例えば500）</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm_disk_type=<code>disk_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>その中に<code>disk_type</code> はディスクタイプを指しています（例えばCLOUD_BASIC）</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p>その中に<code>region</code> はリージョンを指しています（例えば ap-guangzhou）</p>
</li>
</ul>
</div></div></td>
</tr>
</tbody>
</table>
