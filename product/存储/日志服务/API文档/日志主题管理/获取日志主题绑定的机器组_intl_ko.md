## 기능 설명

해당 API는 로그 토픽 바인딩 서버 그룹 정보를 획득하는데 사용됩니다.

## 요청

### 요청 예시

```
GET /topic/machinegroup?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <Authorization String>
```

### 요청행

```
GET /topic/machinegroup
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다. 

### 요청 매개변수

| 필드 이름   | 유형   | 위치  | 필수 여부 | 의미             |
| -------- | ------ | ----- | -------- | ---------------- |
| topic_id | string | query | 예       | 조회하는 로그 토픽 ID |

## 응답

### 응답 예시

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123
{
	"machine_groups": [
	{
		"group_id": "xxxx-xx-xx-xx-yyyyyyyy",
		"group_name": "testname"},    
		{"group_id": "xxxx-xx-xx-xx-zzzzzzzz", 
		"group_name": "testname1"}
	]
}
```

### 응답 헤더

공통 응답 헤더를 제외하고는 특별한 응답 헤더가 사용되지 않습니다. 

### 응답 매개변수

| 필드 이름         | 유형      | 필수 여부 | 의미                     |
| -------------- | --------- | -------- | ------------------------ |
| machine_groups | JsonArray | 예       | 로그 토픽 바인딩 서버 그룹 배열 |

machine_group은 다음과 같이 구성됩니다.

| 필드 이름     | 유형   | 필수 여부 | 의미         |
| ---------- | ------ | -------- | ------------ |
| group_id   | string | 예       | 서버 그룹 ID   |
| group_name | string | 예       | 서버 그룹 이름 |

### 오류 코드

자세한 내용은 [오류 코드](https://cloud.tencent.com/document/product/614/12402) 문서를 참조하십시오.

