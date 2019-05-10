## 기능 설명

해당 API는 지정된 로그 토픽에 로그를 업로드하는 데 사용됩니다.

## 요청

### 요청 예시

```
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf

<LogGroupList 내용을 pd 파일로 패키지화>
```
#### PB 설명 파일

```
package cls;
message Log
{
    message Content
    {
        required string key   = 1;
        required string value = 2;
    }
    required int64   time     = 1; // UNIX Time Format
    repeated Content contents = 2;
}
message LogGroup
{
    repeated Log    logs        = 1;
    optional string contextFlow = 2; // 컨텍스트의 일관성을 유지하기 위해서 사용되는 UID
    optional string filename    = 3; // 파일 이름
    optional string source      = 4; // 로그 소스, 일반적으로 서버 IP를 사용함
}
message LogGroupList
{
    repeated LogGroup logGroupList = 1;
}
```

### 요청행

```
POST /structuredlog
```

### 요청 헤더

공통 헤더를 제외하고 특별한 요청 헤더는 사용되지 않습니다.

### 요청 매개변수

| 필드 이름        |  유형  | 위치  |필수 여부 |      의미                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | query| 예     |로그가 보고되는 로그 토픽 ID                            |
| logGroupList | message|  pb | 예     |로그 내용 관련 설명                                     |

LogGroup 설명:

| 필드 이름        |      의미                                      |
|--------------|-----------------------------------------------|
| logs         |로그 내용                                        |
| contextFlow  |컨텍스트의 일관성을 유지하기 위해서 사용되는 UID                                |
| filename     |파일 이름                                          |
| source       |로그 소스, 일반적으로 서버 IP를 사용함                          |

Log 설명:

| 필드 이름        |      의미                                      |
|--------------|-----------------------------------------------|
| time         |로그 시간, UNIX 타임스탬프, 단위: 초 일부 언어의 경우 밀리초 단위의 시간이 반환되므로 전환이 필요합니다. |
| contents     |로그 내용                                        |

Content 설명:

| 필드 이름        |      의미                                      |
|--------------|-----------------------------------------------|
| key          |필드 key, ```_```으로 시작할 수 없습니다.                    |
| value        |필드 값                                        |

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

