## 기능 설명

해당 API는 로그 토픽 정보 목록을 획득하는 데 사용됩니다.

## 요청

### 요청 예시

```
GET /topics?logset_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### 요청행

```
GET /topics
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름    | 유형   | 위치  | 필수 여부 | 의미             |
| --------- | ------ | ----- | ---- | ---------------- |
| logset_id | string | query | 예   | 조회하는 로그 집합 ID |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "topics": [
    {
    "logset_id": "xxxx-xx-xx-xx-xxxxxxxx",
    "topic_id": "xxxx-xx-xx-xx-yyyyyyyy",
    "topic_name": "testname",
    "path": "/abc/log/test.log",
    "wild_path":"/data/nginx/log/**/access.log",
    "collection": true,
    "index": true,
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
      },
    "create_time": "2017-08-08 12:12:12"
    }
  ]
}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

| 필드 이름 | 유형      | 필수 여부 | 의미             |
| ------ | --------- | ---- | ---------------- |
| topics | JsonArray | 예   | 로그 토픽 정보 배열 |

TopicInfo는 다음과 같이 구성됩니다.

| 필드 이름        | 유형       | 필수 여부 | 의미                                                         |
| ------------- | ---------- | ---- | ------------------------------------------------------------ |
| logset_id     | string     | 예   | 로그 집합 ID                                                  |
| topic_id      | string     | 예   | 로그 토픽 ID                                                |
| topic_name    | string     | 예   | 로그 토픽 이름                                               |
| path          | string     | 예   | 이전 로그 파일 경로                                             |
| wild_path     |	string     | 아니요   | 새로운 와일드카드 로그 캡처 경로이고 /\*\*/로 파일 디렉터리와 파일 이름을 분리하며 이전 경로와 둘 중 하나만 존재합니다  |
| collection    | bool       | 예   | 캡처 사용 여부                                                 |
| index         | bool       | 예   | 인덱스 사용 여부                                                 |
| log_type      | string     | 예   | 캡처한 로그 유형, `json_log`는 json 형식 로그, `delimiter_log`는 구분 기호 형식 로그, `minimalist_log`는 매우 간편한 로그, `egex_log`, `multiline_log`는 여러 행 로그, `fullregex_log`는 완전 정규식 |
| extract_rule  | JsonObject | 예   | 추출 규칙                                                     |
| machine_group | JsonObject | 아니요   | 서버 그룹 정보 캡처                                               |
| create_time   | string     | 아니요   | 생성 시간                                                     |

extract_rule은 다음과 같이 구성됩니다.

| 필드 이름          | 유형              | 필수 여부 | 의미                                                        |
| --------------- | ----------------- | -------- | ----------------------------------------------------------- |
| time_key        | string            | 아니요       | 타임 필드의 key 이름                                           |
| time_format     | string             | 아니요       | 타임 필드의 형식, C 언어의 타임 필드 형식에 대한 `strftime`함수의 설명을 참조하십시오. |
| delimiter       | string            | 아니요       | 구분 기호 유형 로그의 구분 기호                                      |
| log_regex       | string            | 아니요       | 여러 행 로그 유형에 대한 전체 로그 일치 규칙                             |
| beginning_regex | string            | 아니요       | 여러 행 로그 유형에 대한 첫 행 일치 규칙                                 |
| keys            | JsonArray(string) | 아니요       | 추출된 각 필드의 key 이름                                     |
| filter_keys     | JsonArray(string) | 아니요       | 로그를 필터링해야 하는 key                                           |
| filter_regex    | JsonArray(string) | 아니요       | 위의 필드 filter_keys에 해당하는 값, filter_keys의 개수와 일치하고 일일이 대응됩니다.        |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

