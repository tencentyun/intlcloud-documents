## 기능 설명

해당 API는 서버 그룹을 수정하는데 사용됩니다.

## 요청

### 요청 예시

```
PUT /machinegroup HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"group_id": "xxxx-xx-xx-xx-xxxxxxx", "group_name": "testname", "ips": ["10.10.10.10", "10.10.10.11"]}
```

### 요청행

```
PUT /machinegroup
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  | 필수 여부 |      의미                       |
|--------------|--------|------|---------|--------------------------------|
| group_id     | string | body | 예      |수정할 서버 그룹 ID                |
| group_name   | string | body | 아니요      |서버 그룹 이름이고 중복될 수 없습니다.             |
| ips          | JsonArray| body | 아니요      |서버 그룹의 IP 목록                  |


>!group_name과 ips 중 적어도 하나는 제공되어야 합니다.

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Length: 0

```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

없음

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402) 문서를 참조하십시오.


