## 기능 설명

해당 API는 배달 구성을 삭제하는 데 사용됩니다.

## 요청

### 요청 예시

```
DELETE /shipper?shipper_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```
### 요청행

```
DELETE /shipper
```
### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  | 필수 여부 |      의미                       |
|--------------|--------|------|---------|--------------------------------|
| shipper_id   | string | query| 예      |삭제할 배달 구성의 ID                |

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

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

