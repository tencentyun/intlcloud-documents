## 준비 작업

1. 파일 통합 기능은 Serverless Cloud Function(SCF)을 통해 구현되며, 사용 전에 COS 콘솔 [애플리케이션 통합-파일 통합](https://console.cloud.tencent.com/cos5/application/cosConcatFile)에 **파일 통합** 함수를 생성해야 합니다.
2. 함수 생성 후, 함수 리스트 작업 열의 **사용 안내**에 따라 함수 매개변수 설정을 완료합니다. 구체적인 함수 매개변수 설정은 다음을 참고하십시오. 형식은 **JSON 문자열**입니다.
 - SCF 인증을 선택하는 함수의 경우, 클라우드 기능을 실행하기 위해 SCF에서 제공하는 [인보크(Invoke) 인터페이스](https://intl.cloud.tencent.com/document/api/583/17243)를 호출해야 합니다. 이 중 ClientContext 매개변수는 json 형식으로 전달합니다. [함수 매개변수 구성 예시](#1)를 참고하십시오.
 - 인증 면제를 선택한 함수의 경우 해당 API 게이트웨이에 HTTP 요청을 통해 함수를 호출할 수 있습니다.


<span id=1></span>

## 함수 매개변수 예시

>? 실제 사용 시에는 코드에서 주석을 제거해야 합니다.
>

```plaintext
{
    "bucket": "examplebucket-1250000000", // 통합 산출 파일이 최종적으로 전송되는 버킷
    "region": "ap-guangzhou",         // 통합 산출 파일이 최종적으로 전송되는 버킷 소재 리전
    "key": "concat.txt",              // 최종 전송된 통합 산출 파일 이름

    /**
     * sourceList는 패키징할 소스 파일 목록을 지정하는 데 사용되며 형식은 JSON 배열입니다.
     * 각 항목에는 소스 파일의 url과 같은 정보가 포함되어 있으며, 향후 더 많은 매개변수가 확장될 수 있습니다.
     * 
     * 소스 파일 리스트가 너무 길면 sourceList 매개변수를 JSON 문자열화할 수 있습니다.
     * .json 파일을 작성하고 COS에 업로드한 후, sourceConfigList 매개변수를 통해 지정합니다.
     * 
     * sourceList 및 sourceConfigList 매개변수 중 하나만 지정하면 됩니다.
     */
    "sourceList": [
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file1.txt"
        },
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file2.txt"
        },
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.txt"
        }
    ],
    "sourceConfigList": [
        {
             "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceList.json"
        }
    ]
}
```

매개변수 설명은 다음과 같습니다.

| 매개변수 이름                 | 매개변수 설명                                                     | 유형             | 필수 입력 여부 |
| ----------------------- | ------------------------------------------------------------ | ------- | -------- |
| bucket                  | 통합 산출 파일이 최종적으로 전송되는 버킷. 이름 형식: BucketName-APPID. 여기에 입력되는 버킷 이름은 examplebucket-1250000000과 같은 형식이어야 합니다. | String  | 필수 |
| region                                                       | 통합 산출 파일이 최종적으로 전송되는 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String    | 필수   |
| key                                                          | 최종 전송된 통합 산출 파일 이름(Object의 이름). 버킷에서의 객체 고유 식별자. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String    | 필수   |
| sourceList | 소스 파일 리스트. **sourceList와 sourceConfigList는 동시에 비워 둘 수 없습니다** | Array | 필수       |
| sourceList[].url        | 소스 파일 URL                                                 | String  | 필수       |
| sourceConfigList        | sourceList 구성 파일 리스트. 요청 시 전체 sourceList를 수반하지 않으려면 sourceList 매개변수 JSON 문자열을 처리하여 json 구성 파일을 생성하고, COS에 업로드한 후 sourceConfigList에서 해당 파일 URL을 지정할 수 있습니다. 다중 구성 파일 지정을 지원하며, **sourceList와 sourceConfigList는 동시에 비워 둘 수 없습니다** | Array   | 옵션       |
| sourceConfigList[].url  | sourceList 구성 파일 중의 URL                                    | String  | 옵션       |

## 함수 응답 결과 예시
```plaintext
{
    "code": 0,
    "message": "cos concat file success",
    "data": {
        "Location": "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/concat.txt",
        "Bucket": "examplebucket-1250000000",
        "Key": "concat.txt",
        "ETag": "\"152958e4f4bfded94c0b30f03343d6b8-1\""
    }
}
```

응답 매개변수 설정 설명:

| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ------- | ------------------------------------------------------ | ---------------- |
| code    | 비즈니스 오류 코드. 0이면 실행 성공, 그렇지 않으면 실행 실패    | Number           |
| message | 실행 결과의 텍스트 설명. null일 수 있음                        | String           |
| data    | 실행 완료 메시지. 실행 성공 시 통합 산출 파일의 URL 정보 포함 | Object           |
| error   | 실행 오류 메시지. 실행 성공 시 null                    | Object or String |

## 실제 사례



### 매개변수 설정
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "concat.txt",
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file1.txt"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file2.txt"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.txt"
      }
  ]
}
```

### 최종 다중 파일 통합 산출 구조

```plaintext
concat.txt
    ├── content of file1.txt
    ├── content of file2.txt
    └── content of file3.txt
```
