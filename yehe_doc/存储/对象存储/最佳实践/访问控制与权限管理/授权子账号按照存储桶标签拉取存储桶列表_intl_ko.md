## 소개

Cloud Object Storage(COS)를 사용하면 콘솔에서 또는 API를 통해 태그별로 버킷을 필터링할 수 있습니다. 이는 태그별 권한 부여를 기반으로 구현됩니다.

## 인증 단계


1. 루트 계정 Owner로 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 로그인하고 정책 구성 페이지로 이동합니다.
2. 다음과 같이 **정책 생성기** 또는 **정책 구문**을 통해 지정된 태그가 있는 버킷에 대한 서브 계정 SubUser 액세스 권한을 부여합니다.
<dx-tabs>
::: 정책 생성기 사용
1. [CAM 콘솔 구성](https://console.cloud.tencent.com/cam/policy) 페이지로 이동합니다.
2. **사용자 지정 정책 생성 > 정책 생성기에서 생성**을 클릭합니다.
3. 권한 구성 페이지로 이동하여 다음과 같이 정보를 구성합니다.
	- **효과**: 허용이 선택되어 있으며, 기본값에서 변경하지 않습니다.
	- **서비스**: COS를 선택합니다.
	- **작업**: **읽기 > GetService(버킷 목록 가져오기)**를 선택합니다.
	- **리소스**: **모든 리소스**를 선택합니다.
	- **조건**: **기타 조건 추가**를 클릭합니다. 패널에서 다음을 구성합니다.
		- **조건 키**: `qcs:resource_tag`를 선택합니다.
		- **오퍼레이터**: `string_equal`을 선택합니다.
		- **조건 값**: `key&val` 형식으로 태그를 입력합니다. 여기에서 key와 value을 각각 태그 키와 값으로 바꿉니다.
4. **다음**을 클릭하고 정책 이름을 입력합니다.
5. **완료**를 클릭하면 생성이 완료됩니다.
:::
::: 정책 구문
1. [CAM 콘솔 구성](https://console.cloud.tencent.com/cam/policy) 페이지로 이동합니다.
2. **사용자 지정 정책 생성 > 정책 구문으로 생성**을 클릭합니다.
3. 빈 템플릿을 선택하고 **다음**을 클릭합니다.
4. 다음 형식으로 정책을 입력합니다. 여기에서 key와 value을 각각 지정된 태그 키와 값으로 바꿉니다.
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action":[
                "name/cos:GetService"
            ],
            "resource": "*",
            "condition":{
                "for_any_value:string_equal":{
                    "qcs:resource_tag": [
                        "key&value"
                    ]
                }
            }
        }
    ]
}
```
5. **완료**를 클릭하면 생성이 완료됩니다.
:::
</dx-tabs>
3. 정책 페이지의 2단계에서 생성한 정책을 찾고 오른쪽에서 **사용자/사용자 그룹/역할** 연결을 클릭하여 정책을 서브 계정 SubUser와 연결합니다.
4. 팝업 창에서 서브 계정 SubUser를 선택하고 **확인**을 클릭합니다.


## 콘솔에서 보기


1. 서브 계정 SubUser로 [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 버킷 목록 페이지에는 **서브 계정이 액세스할 수 있는 버킷 목록이 자동으로 표시됩니다**.

이제 지정된 태그(key 및 value)가 있는 버킷에 대한 서브 계정 액세스 권한 부여가 완료되었습니다.


## API 호출


>!
> - 콘솔과 달리 GetService API는 서브 계정이 액세스할 수 있는 버킷 목록을 자동으로 표시할 수 없으며 태그 매개변수를 전달해야 합니다.
> - 현재 GetService API를 사용하면 하나의 태그만 전달할 수 있습니다.


1. 서브 계정 SubUser의 키로 요청을 시작합니다.
2. GetService API를 호출하여 (key, value)와 같은 태그 필터링 매개변수를 전달합니다. 아래는 샘플 요청입니다. 자세한 내용은 [GET Service(List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291)를 참고하십시오.

```
GET /?tagkey=key1&tagvalue=value1 HTTP/1.1
Date: Fri, 24 May 2019 11:59:51 GMT
Authorization: Auth String
```


