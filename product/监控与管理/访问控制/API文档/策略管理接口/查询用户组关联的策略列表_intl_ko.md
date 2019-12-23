## API 설명

이 API(ListAttachedGroupPolicies)는 사용자 그룹과 연결된 전략 리스트를 조회하는 데 사용됩니다.

요청 도메인 이름:

```
cam.api.qcloud.com 
```

## 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

| 매개변수 이름 | 유형 | 필수 여부 | 설명                        |
| -------- | ---- | ---- | --------------------------- |
| groupId  | int  | 예   | 사용자 그룹 ID                   |
| page     | int  | 아니요   | 페이지 번호, 기본값: 1, 초시값: 1 |
| rp       | int  | 아니요   | 페이지 당 크기, 기본값: 20       |

## 출력 매개변수

[ListPolicies](https://intl.cloud.tencent.com/document/product/598/15426) API 설명을 참조하십시오.

## 예제

### 입력

```
https://cam.api.qcloud.com/v2/index.php
?groupId=34444
&page=1
&rp=20
&SignatureMethod=HmacSHA256
&Action=ListAttachedGroupPolicies
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=44835
&Timestamp=1523262775
&RequestClient=SDK_PHP_1.1&
Signature=vBfc7JZiDSZZysKesDoywMN3ca80pgZmWVdiQ4QXJJg%3D
```

### 출력

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 1,
        "list": [
            {
                "policyId": 1,
                "policyName": "AdministratorAccess",
                "addTime": "2018-04-09 16:31:19",
                "createMode": 2
            }
        ]
    }
}
```

## 오류 코드

[오류 코드](https://intl.cloud.tencent.com/document/product/598/13884)를 참조하십시오.

