## API 설명

이 API(CreateGroup)는 사용자 그룹을 생성하는 데 사용됩니다.

요청 도메인 이름:

```
cam.api.qcloud.com
```

## 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수만 나열되고 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/6976)는 나열되지 않았습니다.

| 매개변수 이름  | 유형   | 필수 여부 | 설명       |
| --------- | ------ | ---- | ---------- |
| groupName | String | 아니요   | 사용자 그룹 이름   |
| remark    | String | 아니요   | 사용자 그룹 설명 |

## 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
| -------- | ---- | ---- |
| groupId   | int | 사용자 그룹 ID  |

## 예제

### 입력

```
https://cam.api.qcloud.com/v2/index.php
?groupName=testgroupname
&remark=testre123
&SignatureMethod=HmacSHA256
&Action=CreateGroup
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=38803
&Timestamp=1512702940
&RequestClient=SDK_PHP_1.1
&Signature=p4APCiYw5pHhjVk9Fwjk6U9n2%2FuTTaVGzSehd2G4YZc%3D
```

### 출력

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupId": 28791
    }
}
```

## 오류 코드

[오류 코드](https://intl.cloud.tencent.com/document/product/598/13884)를 참조하십시오.
