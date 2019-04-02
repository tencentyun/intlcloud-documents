## 기능 설명

해당 API는 기존 인덱스 태스크를 수정하는 데 사용됩니다.

## 요청

### 요청 예시

```
PUT /index HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "effective": true,
  "rule": {
    "full_text": {
      "case_sensitive": false,
      "tokenizer": "{^&%"
    },
    "key_value": {
      "case_sensitive": false,
      "keys": ["age","name"],
      "types": ["long","text"],
      "tokenizers": ["","-"]
    }
  }
}

```

### 요청행

```
PUT /index
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  |필수 여부 |      의미                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | body | 예      |수정한 index 가 속하는 topic id                      |
| effective    | bool   | body | 예      |인덱스 스위치 상태                                |
| rule         | object | body | 아니요      |인덱스 규칙, effective가 true일 경우 필수함               |


rule은 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| full_text  | object | 아니요      | 전체 텍스트 인덱스 관련 구성              |
| key_value  | object | 아니요      | kv 인덱스 관련 구성               |
> **주의:**
>
> rule을 설정할 때 full_text 및 key_value 중 적어도 하나를 설정해야 합니다.

full_text는 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | 예      | 대소문자를 구분 여부              |
| tokenizer | string | 아니요      | 전체 텍스트 인덱스의 단어 구분 기호              |

Key_value는 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | 예      | 대소문자를 구분 여부              |
| keys | array(string) | 예      | 인덱스를 생성해야 할 key 이름            |
| types| array(string) | 예      | 인덱스를 생성해야 할 key가 해당하는 유형, 일일이 대응됩니다. 지원하는 사항: ```long double text``` |
| tokenizers| array(string) | 아니요      | 위의 key가 해당하는 단어 구분 기호, 일일이 대응됩니다. ```text``` 유형에만 한해 설정하고, 다른 유형은 빈 문자열입니다.  |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0

```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

없음

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

