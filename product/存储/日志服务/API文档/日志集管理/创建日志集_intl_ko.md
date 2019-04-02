## 기능 설명

해당 API는 로그 집합을 생성하고 새 로그 집합의 ID를 리턴하는 데 사용됩니다.

## 요청

### 요청 예시

```
POST /logset HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"logset_name": "testname","period": 15}
```

### 요청행

```
POST /logset
```

### 요청 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  | 필수 여부 |      의미                       |
|--------------|--------|------|---------|--------------------------------|
| logset_name  | string | body | 예      |로그 집합의 이름이며 중복될 수 없음             |
| period       | int    | body | 예      |로그 집합 저장 기간이고 단위는 일이며 최대 :90      |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{"logset_id": "xxxx-xx-xx-xx-xxxxxxxx"}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

|  필드 이름      |  유형     | 필수 여부 |        의미                    |
|-------------|-----------|---------|-------------------------------|
| logset_id   | string    | 예      | 로그 집합 ID                  |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

