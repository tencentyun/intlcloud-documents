## 기능 설명

해당 API는 배달 태스크 정보 목록을 획득하는 데 사용됩니다.

## 요청

### 요청 예시

```
GET /tasks?shipper_id=xx-xx-xx-xxxx&start_time=2017-10-10+00%3A00%3A00&end_time=2017-10-10+23%3A59%3A59 HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### 요청행

```
GET /tasks
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  |필수 여부 |      의미                  |
|--------------|--------|------|---------|---------------------------------|
| shipper_id   | string | query| 예      |조회하는 배달 규칙 id                  |
| start_time   | string | query| 예      |조회 시작 시간, 최근 3일의 조회를 지원합니다.  |
| end_time     | string | query| 예      |조회 종료 시간                     |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "tasks": [
    {
      "task_id": "xxxxx-xx-xx-xx",
      "shipper_id": "xxxxx-xx-xx-xx",
      "topic_id": "xxxxx-xx-xx-xx",
      "range_start": "2017-10-17 10:10:10",
      "range_end": "2017-10-17 10:10:10",
      "start_time": "2017-10-17 10:10:10",
      "end_time": "2017-10-17 10:10:10",
      "status": "success",
      "message": "success",
    }
  ]
}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

|  필드 이름      |  유형     | 필수 여부 |        의미                    |
|-------------|-----------|---------|-------------------------------|
| tasks       | JsonArray | 예      | 배달 태스크 정보 배열                |

TaskInfo는 다음과 같이 구성됩니다.

|  필드 이름     |  유형  | 필수 여부 |        의미                    |
|------------|--------|---------|-------------------------------|
| task_id    | string | 예      | 배달 태스크 ID                |
| shipper_id | string | 예      | 배달 규칙 ID                |
| topic_id   | string | 예      | 로그 토픽 ID                |
| range_start| string | 예      | 이번 배달 로그의 시작 시간         |
| range_end  | string | 예      | 이번 배달 로그의 종료 시간         |
| start_time | string | 예      | 이번 배달 태스크의 시작 시간           |
| end_time   | string | 예      | 이번 배달 태스크의 종료 시간           |
| status     | string | 예      | 이번 배달 태스크의 결과, "success", "running", "failed", 또는 "wait". |
| message    | string | 예      | 결과의 세부 정보                  |

## 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402)를 참조하십시오.

