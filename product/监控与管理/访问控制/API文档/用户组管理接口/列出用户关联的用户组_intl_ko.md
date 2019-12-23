## API 설명

이 API(ListGroupsForUser)는 사용자와 연결된 사용자 그룹을 나열하는 데 사용됩니다.

요청 도메인 이름:

```
cam.api.qcloud.com
```

## 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

| 매개변수 이름 | 유형 | 필수 여부 | 설명                                  |
| -------- | ---- | -------- | ------------------------------------- |
| page     | int  | 아니요       | 페이지 번호. 기본값은 1이며 유효 범위: 1 ~ 200         |
| rp       | int  | 아니요       | 페이지 당 수량. 기본값은 20이며 유효 범위: 0 ~ 200 |
| uid      | int  | 예       | 사용자 ID                               |

## 출력 매개변수

| 매개변수 이름  | 유형  | 설명                                                         |
| --------- | ----- | ------------------------------------------------------------ |
| totalNum  | int   | 사용자가 가입한 총 사용자 그룹 수                                                   |
| groupInfo | array | 사용자 그룹 배열, 배열의 각 멤버는 groupId(사용자 그룹 ID), groupName(사용자 그룹 이름), remark(사용자 그룹 설명) 필드가 있습니다 |

## 예제

### 입력

```
https://cam.api.qcloud.com/v2/index.php
?rp=10
&page=1
&uid=1133398
&SignatureMethod=HmacSHA256
&Action=ListGroupsForUser
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=23509
&Timestamp=1512716160
&RequestClient=SDK_PHP_1.1
&Signature=PsukZTcNW5Ev2%2FY%2F6QBBpu1DntyI4VMFu6PywZQQ5Ww%3D
```

### 출력

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupInfo": [
            {
                "groupId": 28791,
                "groupName": "testgrname",
                "remark": "tee123"
            }
        ],
        "totalNum": "1"
    }
}
```

## 오류 코드

[오류 코드](https://intl.cloud.tencent.com/document/product/598/13884)를 참조하십시오.
