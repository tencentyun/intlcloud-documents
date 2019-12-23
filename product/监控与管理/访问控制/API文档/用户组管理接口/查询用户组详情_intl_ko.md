## API 설명

이 API(GetGroup )는 사용자 그룹 세부 정보를 나열하는 데 사용됩니다.

요청 도메인 이름:

```
cam.api.qcloud.com
```

## 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

| 매개변수 이름 | 유형 | 필수 여부 | 설명      |
| -------- | ---- | -------- | --------- |
| groupId  | int  | 예       | 사용자 그룹 ID |

## 출력 매개변수

| 매개변수 이름   | 유형   | 설명                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| groupId    | int    | 사용자 그룹 ID                                                    |
| groupName  | String | 사용자 그룹 이름                                                   |
| groupNum   | int    | 사용자 그룹 멤버 수                                               |
| remark     | String | 사용자 그룹 설명                                                   |
| createTime | String | 사용자 그룹 생성 시간                                               |
| userInfo   | array  | 인덱스 배열. 멤버는 연결 배열이며 멤버는 사용자 그룹에 가입한 사용자를 나타냅니다. 멤버 필드에는 uid(사용자 그룹), uin(하위 계정 uin), name(하위 계정 별명)이 있습니다 |

## 예제

### 입력

```
https://cam.api.qcloud.com/v2/index.php
?groupId=28791
&SignatureMethod=HmacSHA256
&Action=GetGroup
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=64065
&Timestamp=1512715507
&RequestClient=SDK_PHP_1.1
&Signature=cmXkOx7XeFtmhmaCJTUTUmKYPZ5vT4S6LjIGBnRiTL4%3D
```

### 출력

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupId": 28791,
        "groupName": "testgrname",
        "groupNum": 1,
        "channel": 3,
        "remark": "tee123",
        "createTime": "2017-12-08 11:15:56",
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
