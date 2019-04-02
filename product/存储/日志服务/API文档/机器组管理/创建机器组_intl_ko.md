## 기능 설명

해당 API는 서버 그룹을 생성하고 새 서버 그룹의 ID를 리턴하는 데 사용됩니다.

## 요청

### 요청 예시

```
POST /machinegroup HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"group_name": "testname", "ips": ["10.10.10.10", "10.10.10.11"]}
```

### 요청행

```
POST /machinegroup
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  | 필수 여부 |      의미                       |
|--------------|--------|------|---------|--------------------------------|
| group_name   | ㅍ | body | 예      | 서버 그룹 이름이고 중복될 수 없음.             |
| ips          | JsonArray| body| 예     | 서버 그룹의 IP 목록                  |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{"group_id": "xxxx-xx-xx-xx-xxxxxxxx"}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

|  필드 이름      |  유형     | 필수 여부 |        의미                    |
|-------------|-----------|---------|-------------------------------|
| group_id    | string    | 예      | 서버 그룹 ID                  |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

