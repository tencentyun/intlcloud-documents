## すべてのCLBの全読み取り書き込みポリシー
- サブアカウントにCLBサービスの完全な管理権限（作成、管理などの全操作）を承認します。
- ポリシー名：CLBResourceFullAccess
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"name/clb:*"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

## すべてのCLBの読み取り専用ポリシー
- サブアカウントに、CLBに読み取り専用でアクセスできる権限（すなわち、すべてのCLB下のすべてのリソースを見ることができる権限）を承認します。ただしサブアカウントはそれらの作成、更新または削除を行うことはできません。コンソールでのリソース操作の前提は、そのリソースを見ることができることであるため、サブアカウントのCLB全読み取り権限をアクティブ化することをお勧めします。
- ポリシー名： CLBResourceReadOnlyAccess
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"name/clb:Describe*"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

## あるタグ下のCLBの全読み取り書き込みポリシー
- サブアカウントに、あるタグ（タグキーはtagkey、タグ値はtagvalue）下のCLBの完全な管理権限（インスタンス管理、リスナー管理などの全操作）を承認します。
- CLBインスタンスはタグ設定およびタグ使用認証をサポートしています。

```
{
    "version":"2.0",
    "statement":[
        {
            "effect":"allow",
            "action":"*",
            "resource":"*",
            "condition":{
                "for_any_value:string_equal":{
                    "qcs:tag":[
                        "tagkey&tagvalue"
                    ]
                }
            }
        }
    ]
}  
```
   
