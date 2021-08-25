## 준비 작업

1. 파일 패키징 압축 기능은 Serverless Cloud Function(SCF)을 통해 구현되며, 사용 전에 COS 콘솔 [애플리케이션 통합-ZIP 파일 일괄 패키징](https://console.cloud.tencent.com/cos5/application/cosZip)에 **ZIP 파일 일괄 패키징** 함수를 생성해야 합니다.
2. 함수 생성 후 함수 리스트 작업 열의 **사용 안내**에 따라 함수 매개변수 설정을 완료합니다. 구체적인 함수 매개변수 설정은 다음을 참고하십시오. 형식은 **JSON 문자열**입니다.
 - SCF 인증을 선택한 함수의 경우 SCF에서 제공하는 실행 함수(Invoke) 인터페이스를 호출하여 SCF를 실행해야 하며, 그 중 ClientContext 매개변수는 json 형식으로 전달됩니다. [함수 매개변수 설정 예시](#1)를 참고하십시오.
 -인증 면제를 선택한 함수의 경우 해당 API 게이트웨이에 HTTP 요청을 통해 함수를 호출할 수 있습니다.


<span id=1></span>

## 함수 매개변수 예시

>? 실제 사용 시에는 코드에서 주석을 제거해야 합니다.
>

```plaintext
{
    "bucket": "examplebucket-1250000000", // ZIP 파일이 최종적으로 전송되는 버킷
    "region": "ap-guangzhou", // ZIP 파일이 최종적으로 전송되는 버킷 소재 리전
    "key": "mypack.zip", // 최종적으로 전송되는 ZIP 파일의 이름
    "flatten": false,                 // 소스 파일 경로의 플랫 처리 여부

    /**
     * sourceList는 패키징할 소스 파일 목록을 지정하는 데 사용되며 형식은 JSON 배열입니다.
     * 각 항목에는 소스 파일 url, 이름 변경 경로 renamePath 등이 포함됩니다.
     * 
     * 소스 파일 리스트가 너무 길면 sourceList 매개변수를 JSON 문자열화할 수 있습니다.
     * .json 파일을 작성하고 COS에 업로드한 후, sourceConfigList 매개변수를 통해 지정합니다.
     * 
     * sourceList 및 sourceConfigList 매개변수 중 하나만 지정하면 됩니다.
     */
    "sourceList": [
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg",
            "renamePath": "dir1_rename/file1.jpg"
        },
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4",
            "renamePath": "file2.mp4"
        },
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md"
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
| bucket                  | ZIP 파일이 최종적으로 전송되는 버킷입니다. 이름 형식은 BucketName-APPID입니다. 여기에 입력되는 버킷 이름은 examplebucket-1250000000과 같은 형식이어야 합니다. | String  | 예 |
| region                                                       | ZIP 파일이 최종적으로 전송되는 버킷이 위치한 리전입니다. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String    | 예   |
| key                                                          | 최종 전송된 ZIP 파일 이름(Object의 이름)으로, 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String    | 예   |
| flatten                 | 경로 플랫 처리 여부(소스 디렉터리 구조 제거)로, 예: 소스 파일 URL이 https://domain/source/test.mp4이고 소스 파일 경로가 source/test.mp4, true이면, true일 때 ZIP 파일 중 해당 파일 경로는 test.mp4이고, 그렇지 않으면 ZIP 파일 중 해당 파일 경로는 source/test.mp4입니다. 기본값은 false입니다. | Boolean | 아니요      |
| sourceList | 소스 파일 리스트. **sourceList와 sourceConfigList는 동시에 비워 둘 수 없습니다** | Array | 예       |
| sourceList[].url        | 소스 파일 URL                                                 | String  | 예       |
| sourceList[].renamePath | 경로를 수반한 이름 변경. 즉 소스 파일의 ZIP 파일에서의 파일 경로. 예: dir1/file1.jpg의 이름을 dir1_rename/file1.jpg로 바꿉니다. <br>참고: renamePath의 우선순위는 flatten보다 높으며, 이름 변경 후의 경로는 플랫 처리 영향을 받지 않습니다. | String  | 아니요       |
| sourceConfigList        | sourceList 구성 파일 리스트. 요청 시 전체 sourceList를 수반하지 않으려면 sourceList 매개변수 JSON 문자열을 처리하여 json 구성 파일을 생성하고, COS에 업로드한 후sourceConfigList에서 해당 파일 URL을 지정할 수 있습니다. 다중 구성 파일 지정을 지원하며, **sourceList와 sourceConfigList는 동시에 비워 둘 수 없습니다** | Array   | 아니요       |
| sourceConfigList[].url  | sourceList 구성 파일 중의 URL                                    | String  | 아니요       |

## 함수 응답 결과 예시
```plaintext
{
  code: 0,
  data: {
    Bucket: "examplebucket-1250000000",
    ETag: "\"35bb5e5f050e22bed8f443d8da5dbfb8-1\"",
    Key: "mypack.zip",
    Location: "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/mypack.zip"
  },
  error: null,
  message: "cos zip file success"
}
```

응답 매개변수 설정 설명:

| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ------- | ------------------------------------------------------ | ---------------- |
| code    | 비즈니스 오류 코드, 0이면 실행 성공, 그렇지 않으면 실행 실패    | Number           |
| message | 실행 결과의 텍스트 설명, null일 수 있음                        | String           |
| data    | 실행 완료 메시지, 실행 성공 시 ZIP 파일의 url 정보 포함 | Object           |
| error   | 실행 오류 메시지, 실행 성공 시 null                    | Object or String |

## 실제 사례

### 사례 1: 단순 사례

#### 매개변수 설정
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "mypack.zip",
  "flatten": false,
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md"
      }
  ]
}
```

#### 최종 ZIP 압축파일 구조

```plaintext
mypack.zip
    ├── dir1/file1.jpg
    ├── dir2/file2.mp4
    └── file3.md
```

### 사례 2: 소스 파일 경로 플랫 처리

#### 매개변수 설정
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "mypack.zip",
  "flatten": true,                  // flatten이 true이면 소스 파일 경로를 플랫 처리합니다.
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md"
      }
  ]
}
```

#### 최종 ZIP 압축파일 구조

```plaintext
mypack.zip
    ├── file1.jpg
    ├── file2.mp4
    └── file3.md
```


### 사례 3: 소스 파일 경로 이름 변경

#### 매개변수 설정
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "mypack.zip",
  "flatten": false,
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg",
          // dir1/file1.jpg의 경로 이름을 dir1_rename/file1.jpg로 변경
          "renamePath": "dir1_rename/file1.jpg"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4",
          // dir2/file2.mp4의 이름을 file2.mp4로 변경
          "renamePath": "file2.mp4"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md"
      }
  ]
}
```

#### 최종 ZIP 압축파일 구조

```plaintext
mypack.zip
    ├── dir1_rename/file1.jpg
    ├── file2.mp4
    └── file3.md
```

### 사례 4: 소스 파일 경로 이름 변경 + 플랫 처리

#### 매개변수 설정
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "mypack.zip",
  "flatten": true,         // flatten가 true일 경우, 소스 파일 경로 플랫 처리 진행
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md",
          // file3.md의 이름을 dir3/file3.md로 변경, renamePath 우선 순위가 flatten보다 높기 때문에, 이름 변경 후의 경로는 플랫 처리되지 않음
          "renamePath": "dir3/file3.md"
      }
  ]
}
```

#### 최종 ZIP 압축파일 구조

```plaintext
mypack.zip
    ├── file1.jpg
    ├── file2.mp4
    └── dir3/file3.md
```
