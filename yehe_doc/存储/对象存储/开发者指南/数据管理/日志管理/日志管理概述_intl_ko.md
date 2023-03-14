## 소개
로그 관리 기능은 버킷을 더 편리하게 관리할 수 있도록 지정한 원본 버킷의 액세스 상세 정보를 기록하고 해당 정보를 로그 파일 포맷으로 지정할 수 있습니다.

타깃 버킷에서 로그 기록 경로는 다음과 같습니다.

```shell
타깃 버킷/경로 접두사{YYYY}/{MM}/{DD}/{time}_{random}_{index}
```

로그는 5분마다 생성되어 한 줄씩 기록됩니다. 모든 기록은 여러 개의 필드를 포함하고 각 필드는 빈칸으로 분할됩니다. 주의할 점은 단일 로그 파일의 최대 크기가 256MB이며, 5분 이내 발생된 로그량이 256MB을 초과할 경우 로그는 여러 개의 로그 파일로 분할된다는 것입니다. 현재 지원하는 로그 필드는 다음과 같습니다.

| No. | 필드         | 설명                  | 예시                                                                        |
| :--------: | :---------------: | :-----------------------: | ----------------------------------------------------------------------------- |
| 1        | eventVersion    | 로그 버전          | 1.0                                                                          |
| 2        | bucketName      | 버킷 이름          | examplebucket-1250000000                                                      |
| 3        | qcsRegion       | 요청 리전            | ap-beijing                                                                    |
| 4        | eventTime       | 이벤트 시간(요청 종료 시간, UTC 0시 타임스탬프) | 2018-12-01T11:02:33Z                                                          |
| 5        | eventSource     | 액세스 도메인 이름 | examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com                        |
| 6        | eventName       | 이벤트 이름             | UploadPart                                                                    |
| 7        | remoteIp        | 출처 IP                 | 192.168.0.1                                                                   |
| 8        | userSecretKeyId | 사용자 액세스 KeyId        | AKIDNYVCdoJQyGJ5brTf                                                          |
| 9        | reservedFiled | 예약된 필드   | 예약된 필드는 `-`로 나타납니다. |
| 10       | reqBytesSent    | 요청 바이트 수(Bytes) | 83886080                                                                      |
| 11       | deltaDataSize   | 요청에 의한 스토리지 변경(Bytes) | 808                                                                   |
| 12       | reqPath         | 요청한 파일 경로        | /folder/text.txt                                                              |
| 13       | reqMethod       | 요청 방법             | put                                                                           |
| 14       | userAgent       | 사용자 UA                | cos-go-sdk-v5.2.9                                                             |
| 15       | resHttpCode     | HTTP 응답 상태 코드           | 404                                                                      |
| 16       | resErrorCode    | 에러 코드               | NoSuchKey                               |
| 17       | resErrorMsg     | 에러 메시지            | The specified key does not exist.                                      |
| 18       | resBytesSent    | 반환된 바이트 수(Bytes)   | 197                                                                           |
| 19       | resTotalTime    | 요청에 사용된 총 시간(밀리초, 즉 응답의 마지막 바이트와 요청의 첫 번째 바이트 사이의 시간) | 4295        |
| 20       | logSourceType   | 로그 소스 유형          | USER(사용자 액세스 요청), CDN(CDN 원본 요청)                                                     |
| 21       | storageClass    | 스토리지 유형         | STANDARD, STANDARD_IA, ARCHIVE                                              |
| 22       | accountId    | 버킷 소유자 ID             | 100000000001                                              |
| 23       | resTurnAroundTime    | 요청 서버에서 사용한 시간(밀리초 단위, 즉 응답의 첫 번째 바이트와 요청의 마지막 바이트 사이의 시간) | 4295                                                                          |
| 24       | requester    | 요청자 계정. <br>요청자가 루트 계정인 경우 이 매개변수는 `루트 계정 UIN:루트 계정 UIN` 형식입니다. <br>요청자가 서브 계정인 경우 이 매개변수는 `루트 계정 UIN:서브 계정 UIN` 형식입니다. <br>요청자가 [Service Role](https://intl.cloud.tencent.com/document/product/598/19421)인 경우 이 매개변수는 `승인된 루트 계정 UIN:역할 ID` 형식입니다. <br>요청자가 익명인 경우 이 매개변수는 `-`로 표시됩니다             |    100000000001:100000000001          |
| 25       | requestId    | 요청 ID             | NWQ1ZjY4MTBfMjZiMjU4NjRfOWI1N180NDBiYTY=      |
| 26       | objectSize    | 객체 크기(Bytes)             | 808, 멀티파트 업로드를 사용하면 업로드가 완료된 경우에만 objectSize가 표시되고 멀티파트 업로드 프로세스 중에는 `-`로 표시됩니다 |
| 27       | versionId    | 객체 버전 ID             | 랜덤 문자열                                            |
| 28       | targetStorageClass    | 타깃 스토리지 유형. 복사 작업 요청을 시작하면 해당 필드를 기록합니다.            | STANDARD, STANDARD_IA, ARCHIVE                                              |
| 29     | referer    | 요청 HTTP referer             | `*.example.com` 또는 111.111.111.1       |
| 30       | requestUri    | 요청 URI             | "GET /fdgfdgsf%20/%E6%B5%AE%E7%82%B9%E6%95%B0 HTTP/1.1"       |
| 31       | vpcId    | VPC 요청 ID            | "0"(VPC 아님)/"12345"(VPC, "0"이 아닌string)       |

>!
> - 현재 COS의 로그 관리 기능이 지원되는 리전은 베이징, 상하이, 광저우, 난징, 충칭, 청두, 중국홍콩, 서울, 싱가포르, 토론토, 실리콘밸리, 뭄바이입니다.
> - 로그 관리 기능은 소스 버킷과 타깃 버킷이 반드시 같은 리전에 있어야 합니다.
> - 로그를 보관한 타깃 버킷은 소스 버킷 자체가 될 수 있지만, 권장하지는 않습니다.
> - 현재는 버킷이 JSON API 또는 JSON API 기반 SDK 또는 툴이 아닌 XML API 및 XML API 기반 SDK 또는 툴을 통해 액세스하는 경우에만 로그가 생성됩니다.
> - 고객 요구 및 비즈니스 개발에 따라 COS는 액세스 로그에 새 필드를 추가할 수 있습니다. 로그를 파싱할 때 이에 대비해야 합니다.
> 

## 로그 관리 활성화
### 콘솔 사용
사용자는 콘솔을 통해 로그 관리 기능을 빠르게 활성화할 수 있습니다. 작업 가이드는 [로그 관리 설정](https://intl.cloud.tencent.com/document/product/436/17040) 콘솔 가이드를 참고하십시오.

### API 사용 
API를 사용해 지정 버킷에 로그 관리 기능을 활성화할 경우 다음 순서를 참고하십시오.
1. 로그 역할을 생성합니다.
2. 로그 역할로 권한을 바인딩합니다.
3. 로그 관리를 활성화합니다.

#### 1. 로그 역할 생성
로그 역할 생성과 구체적인 인터페이스 정보는 [CreateRole](https://intl.cloud.tencent.com/document/product/598/33561)을 참고하십시오.
roleName은 반드시 CLS_QcsRole이어야 합니다.
policyDocument:
```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal":{
			"service": "cls.cloud.tencent.com"
		}
	}]
}
```
#### 2. 로그 역할 바인딩 권한
로그 역할 권한을 부여합니다. API에 대한 자세한 내용은 [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/33562)를 참고하십시오.
여기에서 policyName은 QcloudCOSAccessForCLSRole로 설정되고 roleName은 1단계의 CLS_QcsRole 또는 roleName 생성 시 반환된 roleID입니다.

#### 3. 로그 관리 활성화
인터페이스 호출 및 로그 관리 기능 활성화와 구체적인 인터페이스 정보는 [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054)을 참고하십시오. 로그를 보관한 대상 버킷과 소스 버킷은 같은 리전에 있어야 합니다.
