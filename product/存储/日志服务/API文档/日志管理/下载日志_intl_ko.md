## 기능 설명

해당 API는 커서를 사용하여 로그를 다운로드하는 데 사용됩니다.

## 요청

### 요청 예시

```
GET /log?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&cursor=xxxxxx&count=10 HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### 요청행

```
GET /log
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  |필수 여부 |      의미                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | query| 예     |로그 토픽 ID                                     |
| cursor       | string | query| 예     |  로그 커서 획득을 통하여 API가 획득한 커서                 |
| count        | string | query| 예     |다운로드할 로그 수, 최대: 1000개                     |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/x-protobuf
Content-Length: 23
x-cls-cursor: xxxxxx
x-cls-count:10

<LogGroupList 내용을 pd 파일로 패키지화>
```

### 응답 헤더

| Header 이름              |      의미                       |
|------------------------|--------------------------------|
| x-cls-cursor           |현재 로그 커서, 다음 다운로드에 계속 사용  |
| x-cls-count            |현재 요청에서 다운로드된 로그 수           |

### 응답 매개변수

LogGroupList 개체의 패키지된 내용을 반환합니다. pb 파일의 설명에 대한 세부 정보는 [구조화 로그 업로드](https://cloud.tencent.com/document/product/614/16873) API를 참조하십시오.

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402) 문서를 참조하십시오.

