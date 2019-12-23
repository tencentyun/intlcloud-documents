## API 설명

이 API(ListGroups)는 사용자 그룹 리스트를 조회하는 데 사용됩니다.

요청 도메인 이름:

```
cam.api.qcloud.com
```

## 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

| 매개변수 이름 | 유형   | 필수 여부 | 설명                                  |
| -------- | ------ | ---- | ------------------------------------- |
| page     | int    | 아니요   | 페이지 번호. 기본값은 1이며 유효 범위: 1 ~ 200         |
| rp       | int    | 아니요   | 페이지 당 수량. 기본값은 20이며 유효 범위: 0 ~ 200 |
| keyword  | String | 아니요   | 사용자 그룹 이름으로 매칭                      |

## 출력 매개변수

| 매개변수 이름  | 유형  | 설명                                                         |
| --------- | ----- | ------------------------------------------------------------ |
| totalNum  | int   | 총 사용자 그룹 수                                                   |
| groupInfo | array | 사용자 그룹 배열, 배열의 각 멤버는 groupId(사용자 그룹 ID), groupName(사용자 그룹 이름), createTime(사용자 그룹 생성 시간), remark(사용자 그룹 설명) 필드가 있습니다 |

## 예제

### 입력

```
https://cam.api.qcloud.com/v2/index.php
?rp=10
&page=1
&SignatureMethod=HmacSHA256
&Action=ListGroups
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=21810
&Timestamp=1510736488
&RequestClient=SDK_PHP_1.1
&Signature=d8ZMD4byKJB0vBVqLqj0NJoyMa3c5DtFsZcbw1oLCEk%3D
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
                "groupId": 26705,
                "groupName": "ckwmwsllx",
                "channel": 3,
                "remark": "这很西游5",
                "createTime": "2017-10-23 20:49:49"
            },
            {
                "groupId": 23742,
                "groupName": "gtdx",
                "channel": 3,
                "remark": null,
                "createTime": "2017-07-24 19:42:39"
            }
        ],
        "totalNum": "2"
    }
}
```

## 오류 코드

[오류 코드](https://intl.cloud.tencent.com/document/product/598/13884)를 참조하십시오.
