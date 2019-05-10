## 기능 설명

해당 API는 서버 그룹 정보 목록을 획득하는 데 사용됩니다.

## 요청

### 요청 예시

```
GET /machinegroups HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### 요청행

```
GET /machinegroups
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

없음

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "machine_groups": [
    {
    "group_id": "xxxx-xx-xx-xx-xxxxxxxx",
    "group_name": "testname",
    "create_time": "2017-08-08 12:12:12"
    }
  ]
]
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 해당 매개변수

|  필드 이름      |  유형     | 필수 여부 |        의미                    |
|-------------|-----------|---------|-------------------------------|
| machine_groups|JsonArray| 예     | 서버 그룹 정보 배열                  |

MachineGroupInfo는 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| group_id   | string | 예      | 서버 그룹 ID                  |
| group_name | string | 예      | 서버 그룹 이름                    |
| create_time| string | 아니요      | 생성 시간                       |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

