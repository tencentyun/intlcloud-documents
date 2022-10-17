## 모든 CLB 인스턴스에 대한 전체 액세스 정책
- CLB 서비스(생성, 관리 등)에 대한 전체 액세스 권한을 서브 계정에 부여합니다.
- 정책 이름: CLBResourceFullAccess
```
{
	"version": "2.0",
	"statement": [{
		"action":[
			"name/clb:*"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

## 모든 CLB 인스턴스에 대한 읽기 전용 정책
- 서브 계정에 CLB에 대한 읽기 전용 액세스 권한을 부여합니다(즉, 모든 CLB 리소스를 생성, 업데이트 또는 삭제할 수는 없지만 볼 수 있는 권한). 콘솔에서 리소스를 조작하기 위한 전제 조건은 리소스를 볼 수 있는 기능입니다. 따라서 서브 계정에 CLB에 대한 전체 읽기 액세스 권한을 부여하는 것이 좋습니다.
- 정책 이름: CLBResourceReadOnlyAccess
```
{
	"version": "2.0",
	"statement": [{
		"action":[
			"name/clb:Describe*"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

## 지정된 태그의 CLB 서비스에 대한 전체 액세스 정책
- 서브 계정에 지정된 태그(태그 키: tagkey, 태그 값: tagvalue)에서 CLB 서비스(인스턴스 생성, 리스너 관리 등)에 대한 전체 액세스 권한을 부여합니다.
- CLB 인스턴스는 태그 구성 및 인증을 위한 태그 사용을 지원합니다.

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
   
