## 기능 설명

해당 API는 기존 배달 태스크를 수정하는 데 사용됩니다. 해당 API를 사용할 때 CLS에 지정된 버킷의 쓰기 권한을 수동으로 부여해야 합니다.



### 요청 예시

```
 PUT /shipper HTTP/1.1
 Host: <Region>.cls.myqcloud.com
 Authorization: <AuthorizationString>
 Content-Type: application/json
 
 {
   "shipper_id": "xxxx-xx-xx-xx-xxxxxxxx",
   "bucket": "test-1250000001",
   "prefix": "test",
   "shipper_name": "myname",
   "interval": 300,
   "max_size": 256,
   "effective": true,
   "partition": "%Y%m%d",
     "compress": {
         "format": "none"
     },
     "content": {
         "format": "json",
     },
   "filter_rules": [{
     "key": "",
     "regex": "",
     "value": ""
   }]
 }
```



## 요청행

```
PUT /shipper
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름       | 유형   | 위치 | 필수 여부 | 의미                                                         |
| ------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| shipper_id   | string | body | 예   | 수정할 Shipper ID                                         |
| bucket       | string | body | 아니요   | Shipper가 배달하는 새로운 bucket, 형식: {bucketName}-{appid}        |
| prefix       | string | body | 아니요   | Shipper가 배달하는 새로운 디렉터리 접두사                                   |
| shipper_name | string | body | 아니요   | 배달 규칙의 이름                                               |
| interval     | int    | body | 아니요   | 배달하는 시간 간격, 단위: 초, 기본값: 300, 범위: 60 ~ 3600           |
| max_size     | int    | body | 아니요   | 배달하는 파일의 최대값, 단위: MB, 기본값: 256, 범위: 100 ~ 10240      |
| effective    | bool   | body | 아니요   | 배달 스위치 상태                                           |
| filter_rules | array  | body | 아니요   | 배달하는 로그의 필터링 규칙, 일치한 로그를 배달합니다. 각 rule은 `and` 관계를 유지하고, 상한은 5입니다. 배열이 비어 있을 경우 필터링하지 않고 모두 배달합니다 |
| partition    | string | body | 아니요   | 배달하는 로그의 파티션 규칙, `strftime` 타임 형식으로 표시             |
| compress     | object | body | 예   | 배달 로그의 압축 구성                                           |
| content      | object | body | 예   | 배달 로그의 내용 형식 구성                                       |

Rule 형식은 다음과 같습니다.

| 필드 이름 | 유형   | 필수 여부 | 의미                                                  |
| ------ | ------ | ---- | ----------------------------------------------------- |
| key    | string | 예   | 비교되는 key, `__CONTENT__`는 전체 텍스트를 표시합니다.                 |
| regex  | string | 예   | 비교 내용의 추출 정규식                              |
| value  | string | 예   | 위의 regex가 추출한 내용과 비교하는 value, 일치하면 적중됩니다. |

compress 형식은 다음과 같습니다.

| 필드 이름 | 유형   | 필수 여부 | 의미                                       |
| ------ | ------ | ---- | ------------------------------------------ |
| format | string | 예   | 압축 형식, `gzip`, `lzop` 및 `none`은 압축하지 않음. |

content 형식은 다음과 같습니다.

| 필드 이름   | 유형   | 필수 여부 | 의미                        |
| -------- | ------ | -------- | --------------------------- |
| format   | string | 예       | 내용 형식, `json`, `csv` 지원 |
| csv_info | object | 아니요       | 내용 형식이 `csv`일 때 성정        |

csv_info 형식은 다음과 같습니다.

| 필드 이름             | 유형          | 필수 여부 | 의미                                             |
| ------------------ | ------------- | -------- | ------------------------------------------------ |
| print_key          | bool          | 예       | key 첫 행을 csv에 쓰기 여부                                 |
| keys               | array(string) | 예       | 각 열의 key 이름                                    |
| delimiter          | string        | 예       | 각 필드간의 구분 기호                                 |
| escape_char        | string        | 예       | 필드 내용에 구분 기호가 포함될 경우, 해당 이스케이프 문자로 해당 필드를 포장합니다 |
| non_existing_field | string        | 예       | 위에 지정된 존재하지 않는 필드에 해당 내용으로 채웁니다           |

>!bucket, prefix, shipper_name, interval, max_size, effective, filter_rules 및 compress 필드 중 적어도 하나는 있어야 합니다.

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

