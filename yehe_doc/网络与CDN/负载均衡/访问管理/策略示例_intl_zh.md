## 所有 CLB 的全读写策略
- 授权一个子账户以 CLB 服务的完全管理权限（创建、管理等全部操作）。
- 策略名称：CLBResourceFullAccess
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

## 所有 CLB 的只读策略
- 授权一个子账户只读访问 CLB 的权限（即可以查看所有 CLB 下面所有资源的权限），但子账户无法创建、更新或删除它们。在控制台，操作一个资源的前提是可以查看该资源，所以建议您为子账户开通 CLB 全读权限。
- 策略名称： CLBResourceReadOnlyAccess
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

## 某个标签下 CLB 的全读写策略
- 授权一个子账户对某个标签（标签键为 tagkey，标签值为 tagvalue）下的 CLB 的完全管理权限（管理实例、管理监听器等全部操作）。
- CLB 实例支持配置标签和使用标签鉴权。

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
   
