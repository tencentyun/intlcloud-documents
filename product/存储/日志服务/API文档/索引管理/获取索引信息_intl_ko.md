## 기능 설명

해당 API는 지정된 인덱스 전략에 대한 세부 정보를 획득하는 데 사용됩니다.

## 요청

### 요청 예시

```
GET /index?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### 요청행

```
GET /index
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름         |  유형  | 위치   |필수 여부 |      의미                  |
|---------------|--------|-------|---------|---------------------------|
| topic_id      | string | query | 예      |조회하는 index가 속하는 topic id    |

### 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 153

{
  "topic_id": "yyyy-yy-yy-yy-yyyyyyyy",
  "effective": true,
  "rule": {
    "full_text": {
      "case_sensitive": false
    },
    "key_value": {
      "case_sensitive": false,
      "keys": ["age","name"],
      "types": ["long","text"]
    }
  }
}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| topic_id   | string | 예      | 인덱스 규칙이 속하는 topic id          |
| effective  | bool   | 예      | 배달 태스크 구성 적용 여부                       |
| rule       | object | 아니요      | 인덱스 규칙, effective가 true일 경우 리턴합니다|

rule은 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| full_text  | object | 아니요      | 전체 텍스트 인덱스 관련 구성              |
| key_value  | object | 아니요      | kv 인덱스 관련 구성               |

full_text는 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | 예      | 대소문자를 구분 여부              |

Key_value는 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | 예      | 대소문자를 구분 여부              |
| keys | array(string) | 예      | 인덱스를 생성해야 할 key 이름              |
| types| array(string) | 예      | 위의 key가 해당하는 유형, 일일이 대응됩니다. 지원하는 사항: ```long double text```  |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

