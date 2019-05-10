## 기능 설명

해당 API는 지정된 기준에 따라 로그 내용을 검색하는 데 사용됩니다.

### 요청 예시

```
GET /searchlog?logset_id=xxxx-xx-xx-xx-xxxxxxxx&topic_ids=xxxx,xxxx&start_time=2017-08-22%2010%3A10%3A10&end_time=2017-08-23%2010%3A10%3A10&query=&limit=10&context= HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### 요청행

```
GET /searchlog
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름         |  유형  | 위치  |필수 여부 |      의미                                          |
|---------------|--------|------|--------|---------------------------------------------------|
| logset_id     | string | query| 예      |조회할 로그 집합 ID                                   |
| topic_ids     | string | query| 예      |조회할 topic id 조합, `,`로 구분                         |
| start_time    | string | query| 예      |조회할 로그 시작 시간, 형식: YYYY-mm-dd HH:MM:SS       |
| end_time      | string | query| 예      |조회할 로그 종료 시간, 형식: YYYY-mm-dd HH:MM:SS       |
| query         | string | query| 예      |조회할 내용                                         |
| limit         | int    | query| 예      |한 번에 리턴할 로그 수, 최대: `100` 개          |
| context       | string | query| 아니요      |더 많은 내용을 사용하려면, 마지막으로 리턴한 context 값을 패스스루하고, 후속 로그 내용을 획득합니다 |
| sort          | string | query| 아니요      |시간에 따라 정렬. asc(오름차순) 또는 desc(내림차순), 기본적으로 desc입니다.        |

## 응답

### 응답 예시

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 53

{
    "context": "abcdefg",
    "listover": false,
    "results": [
    {
        "timestamp": "2017-07-14 20:43:00",
        "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
        "topic_name": "xxxxxxx",
        "content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    },
    {
        "timestamp": "2017-07-14 20:42:00",
        "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
        "topic_name": "xxxxxxx",
        "content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    }
    ]
}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

| 필드 이름      | 유형                | 필수 여부 |        의미                    |
|-------------|----------------------|---------|-------------------------------|
| context     | string               | 예      | 후속 내용을 탑재하는 데 사용되는 내용        |
| listover    | bool                 | 예      | 찾은 결과를 모두 리턴하였는지 여부          |
| results     | JsonArray(LogObject) | 예      | 로그 내용 정보                    |

LogObject는 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| topic_id   | string | 예      | 로그가 속한 topic id             |
| topic_name | string | 예      | 로그 토픽 이름                  |
| timestamp  | string | 예      | 로그 시간                       |
| content    | string | 예      | 로그 내용                       |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

