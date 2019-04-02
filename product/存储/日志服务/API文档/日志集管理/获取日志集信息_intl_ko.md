## 기능 설명

해당 API는 로그 집합 정보를 획득하는 데 사용됩니다.

## 요청

### 요청 예시

```
GET /logset?logset_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### 요청행

```
GET /logset
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  | 필수 여부 |      의미                       |
|--------------|--------|------|---------|--------------------------------|
| logset_id    | string | query| 예      |조회하는 로그 집합 ID |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "logset_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "logset_name": "testname",
  "period": 15,
  "create_time": "2017-08-08 12:12:12"
}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| logset_id  | string | 예      | 로그 집합 ID                  |
| logset_name| string | 예      | 로그 집합 이름                    |
| period     | int    | 예      | 저장 기간(일)                  |
| create_time| string | 아니요      | 생성 시간                       |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

