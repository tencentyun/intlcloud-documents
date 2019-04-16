## 기능 설명

해당 API는 지정된 로그 토픽의 로그 커서를 획득하고 다운로드하는 데 사용됩니다.

## 요청

### 요청 예시

```
GET /cursor?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&start=2017-12-28%2014%3A13%3A00 HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### 요청행

```
GET /cursor
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  |필수 여부 |      의미                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | query| 예     |로그 토픽 ID                                     |
| start        | string | query| 예     |로그 시작 시간, 세분화 단위는 분입니다. 형식: YYYY-mm-dd HH:MM:SS  |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 23

{
    "cursor": "1212ssssxxxxxx"
}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

| 필드 이름      | 유형                | 필수 여부 |        의미                    |
|-------------|----------------------|---------|-------------------------------|
| cursor      | string               | 예      | 커서                           |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

