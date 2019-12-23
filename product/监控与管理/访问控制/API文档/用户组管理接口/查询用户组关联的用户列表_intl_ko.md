## API 설명

이 API(ListUsersForGroup)는 사용자 그룹과 연결된 사용자 리스트를 조회하는 데 사용됩니다.

요청 도메인 이름:

```
cam.api.qcloud.com
```

## 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

| 매개변수 이름 | 유형 | 필수 여부 | 설명                                  |
| -------- | ---- | ---- | ------------------------------------- |
| page     | int  | 아니요   | 페이지 번호. 기본값은 1이며 유효 범위: 1 ~ 200         |
| rp       | int  | 아니요   | 페이지 당 수량. 기본값은 20이며 유효 범위: 0 ~ 200 |
| groupId  | int  | 예   | 사용자 그룹 ID                             |

## 출력 매개변수

| 매개변수 이름 | 유형  | 설명                                                         |
| -------- | ----- | ------------------------------------------------------------ |
| totalNum | int   | 사용자 그룹과 연결된 총 사용자 수                                         |
| userInfo | array | 사용자 배열, 배열의 각 멤버는 uid(사용자 ID), uin(사용자 UIN), name(사용자 이름), createTime(생성 시간), isReceiverOwner(기본 계정 여부) 등의 필드가 있습니다 |

## 예제

### 입력

```
https://cam.api.qcloud.com/v2/index.php
?rp=10
&page=1
&groupId=23742
&SignatureMethod=HmacSHA256
&Action=ListUsersForGroup
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=53463
&Timestamp=1510737439
&RequestClient=SDK_PHP_1.1
&Signature=43rnmIrGF64te4WuPdWgBDdHPRAU1CsuF19WUR8dxVc%3D
```

### 출력

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupInfo": [],
        "totalNum": "1",
        "userInfo": [
            {
                "uid": 1133398,
                "uin": 3449203261,
                "name": "test1",
                "phoneNum": "13631422209",
                "countryCode": "86",
                "phoneFlag": 0,
                "email": "2385420691@qq.com",
                "emailFlag": 0,
                "userType": 3,
                "createTime": "2017-09-04 16:40:15",
                "isReceiverOwner": 0
            }
        ]
    }
}
```

## 오류 코드

[오류 코드](https://intl.cloud.tencent.com/document/product/598/13884)를 참조하십시오.
