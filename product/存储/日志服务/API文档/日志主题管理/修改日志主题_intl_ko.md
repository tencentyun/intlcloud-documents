## 기능 설명

해당 API는 로그 토픽을 수정하는 데 사용됩니다.

## 요청

### 요청 예시

```
PUT /topic HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxxxx-xx-xx-xx-xxxxxxxx",
  "topic_name": "testname",
  "path": "/data/nginx/log/access.log",
  "wild_path":"/data/nginx/log/**/access.log",
  "collection": false,
  "log_type": "delimiter_log",
  "extract_rule": {
      "time_key": "date",
      "time_format": "%Y-%m-%d %H:%M:%S",
      "delimiter": "|",
      "log_regex": ".*",
      "beginning_regex": "^",
      "keys": ["date","","content"],
      "filter_keys": [],
      "filter_regex": []
  }
}
```

### 요청행

```
PUT /topic
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름       | 유형       | 위치 | 필수 여부 | 의미                                                         |
| ------------ | ---------- | ---- | ---- | ------------------------------------------------------------ |
| topic_id     | string     | body | 예   | 로그 토픽 ID                                                |
| topic_name   | string     | body | 아니요   | 로그 토픽 이름                                               |
| path         | string     | body | 아니요   | 이전 로그 토픽이 캡처해야 할 로그 경로                                   |
| wild_path    | string     | body | 아니요   | 새로운 와일드카드 로그 캡처 경로이고 /\*\*/로 파일 디렉터리와 파일 이름을 분리하며 이전 경로와 둘 중 하나만 존재합니다.       |
| collection   | bool       | body | 아니요   | 캡처 시작 여부                                                 |
| log_type     | string     | body | 아니요   | 캡처한 로그 유형, `json_log`는 json 형식 로그, `delimiter_log`는 구분 기호 형식 로그, `minimalist_log`는 매우 간편한 로그, `multiline_log`는 여러 행 로그, `fullregex_log`는 완전 정규식 |
| extract_rule | JsonObject | body | 아니요   | 추출 규칙                                                     |

>!topic_name, path, group_id, collection, (log_type+extract_rule) 중 적어도 하나는 제공되어야 합니다.



extract_rule은 다음과 같이 구성됩니다.

| 필드 이름          | 유형              | 필수 여부 | 의미                                                         |
| --------------- | ----------------- | -------- | ------------------------------------------------------------ |
| time_key        | string            | 아니요       | 타임 필드의 key 이름, time_key 및 time_format는 반드시 짝으로 나타나야 합니다.         |
| time_format     | string             | 아니요       | 타임 필드의 형식, C 언어의 타임 필드 형식에 대한 `strftime`함수의 설명을 참조하십시오.  |
| delimiter       | string            | 아니요       | 구분 기호 유형 로그의 구분 기호, `log_type`이 `delimiter_log`일 때만 유효합니다 |
| log_regex       | string            | 아니요       | 모든 로그 일치 규칙, `log_type`이 `fullregex_log`일 때만 유효합니다      |
| beginning_regex | string            | 아니요       | 첫 행 일치 규칙, `log_type`이 `multiline_log` 또는 `regex_log`일 때만 유효합니다 |
| keys            | JsonArray(string) | 아니요       | 추출한 필드의 key 이름, 빈 key 는 필드를 버리는 것을 의미합니다. `log_type`이 `delimiter_log`일 때만 유효합니다. `json_log` 로그는 json의 key를 사용합니다. |
| filter_keys     | JsonArray(string) | 아니요       | 로그를 필터해야 할 key, 최대 5개                                   |
| filter_regex    | JsonArray(string) | 아니요       | 위의 필드 filter_keys에 해당하는 값, filter_keys의 개수와 일치하고 일일이 대응되며 일치한 로그를 캡처합니다 |

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

