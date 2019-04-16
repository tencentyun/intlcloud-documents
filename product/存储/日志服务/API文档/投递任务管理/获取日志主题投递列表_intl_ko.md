## 기능 설명

해당 API는 지정된 로그 토픽의 배달 전략의 세부 목록을 획득하는 데 사용됩니다.

## 요청

### 요청 예시

```shell
 GET /shippers?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
 Host: <Region>.cls.myqcloud.com
 Authorization: <Authorization String>
```

### 요청행 

```shell
GET /shippers
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름   | 유형   | 위치  | 필수 여부 | 의미                          |
| -------- | ------ | ----- | -------- | ----------------------------- |
| topic_id | string | query | 예       | 조회하는 Shipper가 속하는 topic id |
| offset   | int    | query | 아니요       | 조회하는 시작 위치, 기본값은 0입니다.         |
| count    | int    | query | 아니요       | 조회 수, 기본값: 50, 최대: 1000  |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "shippers": [
  {
    "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
    "topic_id": "yyyy-yy-yy-yy-yyyyyyyy",
    "bucket": "test-1250000001",
    "prefix": "test",
    "shipper_name": "myname",
    "interval": 300,
    "max_size": 256,
    "effective": true,
    "filter_rules": [{
      "key": "",
      "regex": "",
      "value": ""
    }],
    "partition": "%Y%m%d",
    "compress": {
        "format": "none"
    },
    "content": {
        "format": "json"
    },
    "create_time": "2017-12-12 12:12:12"
  }
  ]
}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다.

### 응답 매개변수

| 필드 이름   | 유형      | 필수 여부 | 의미         |
| -------- | --------- | -------- | ------------ |
| shippers | JsonArray | 예       | 배달 정보 배열 |

ShipperInfo는 다음과 같이 구성됩니다. 

| 필드 이름       | 유형   | 필수 여부 | 의미                                               |
| ------------ | ------ | -------- | -------------------------------------------------- |
| shipper_id   | string | 예       | 배달 태스크 인스턴스                                          |
| topic_id     | string | 예       | 배달 규칙이 속하는 topic id                            |
| bucket       | string | 예       | 배달 bucket 주소                                 |
| prefix       | string | 예       | 배달 대상 디렉터리                                     |
| shipper_name | string | 예       | 배달 규칙 이름                                     |
| interval     | int    | 예       | 배달하는 시간 간격, 단위: 초                            |
| max_size     | int    | 예       | 배달하는 파일의 최대값, 단위: MB                        |
| effective    | bool   | 예       | 배달 태스크 구성 적용 여부                                           |
| filter_rules | array  | 예       | 배달 로그의 필터링 규칙                                 |
| create_time  | string | 예       | 배달 로그의 생성 시간                                 |
| partition    | string | 예       | 배달 로그의 파티션 규칙, `strftime` 타임 형식으로 표시 |
| compress     | object | 예       | 배달 로그의 압축 구성                                 |
| content      | object | 예       | 배달 로그의 내용 형식 구성                             |

filter_rules는 다음과 같이 구성됩니다.

| 필드 이름 | 유형   | 필수 여부 | 의미                                                  |
| ------ | ------ | -------- | ----------------------------------------------------- |
| key    | string | 예       | 비교되는 key, `__CONTENT__`는 전체 텍스트를 표시합니다.                |
| regex  | string | 예   | 비교 내용의 추출 정규식                              |
| value  | string | 예       | 위의 regex가 추출한 내용과 비교하는 value, 일치하면 적중됩니다. |

compress 형식은 다음과 같습니다.

| 필드 이름 | 유형   | 필수 여부 | 의미                                       |
| ------ | ------ | -------- | ------------------------------------------ |
| format | string | 예       | 압축 형식, gzip, lzop 및 none은 압축하지 않음. |

content 형식은 다음과 같습니다.

| 필드 이름   | 유형   | 필수 여부 | 의미                        |
| -------- | ------ | -------- | --------------------------- |
| format   | string | 예       | 내용 형식, json, csv 지원 |
| csv_info | object | 아니요       | 내용 형식이 csv일 때 리턴합니다       |

csv_info 형식은 다음과 같습니다.

| 필드 이름             | 유형          | 필수 여부 | 의미                                             |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key          | bool          | 예       | key 첫 행을 csv에 쓰기 여부                              |
| keys               | array(string) | 예       | 각 열의 key 이름                                  |
| delimiter          | string        | 예       | 각 필드간의 구분 기호                                 |
| escape_char        | string        | 예       | 필드 내용에 구분 기호가 포함될 경우, 해당 이스케이프 문자로 해당 필드를 포장합니다 |
| non_existing_field | string        | 예       | 위에 지정된 존재하지 않는 필드에 해당 내용으로 채웁니다           |

### 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402) 문서를 참조하십시오.

