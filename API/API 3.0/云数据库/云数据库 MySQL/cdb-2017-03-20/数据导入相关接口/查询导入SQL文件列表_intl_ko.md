## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(DescribeUploadedFiles)는 사용자 가져오기한 SQL 파일 리스트 조회에 사용됩니다.

## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeUploadedFiles |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 이 API에는 이 매개변수를 전달할 필요가 없습니다. |
| Path | 예 | String | 파일 경로. 이 필드에는 사용자 기본 계정의 OwnerUin 정보를 입력해야 합니다. |
| Offset | 아니요 | Integer | 오프셋 기록, 기본값은 0입니다. |
| Limit | 아니요 | Integer | 1회 요청의 반환 수량. 기본값은 20입니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| TotalCount | Integer | 조회 조건에 부합하는 SQL 파일 총수.|
| Items | Array of [SqlFileInfo](/document/api/236/15878#SqlFileInfo) | 반환된 SQL 파일 리스트. |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 가져오기 SQL 파일 리스트 조회

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=DescribeUploadedFiles
&Path=100000983328
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":1,
        "Items":[
            {
                "UploadTime":"2016-11-28 15:16:13",
                "UploadInfo":{
                    "AllSliceNum":5,
                    "CompleteNum":3
                },
                "FileName":"joellwang.sql",
                "FileSize":8581633,
                "IsUploadFinished":0,
                "FileId":"5596d7433fe211da4b487228db4e7c57",
                "Access_url": "http://xxxxxx-xxxxxxx.file.myqcloud.com:8080/100000983328/task.sql"
            }
        ]        
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeUploadedFiles)

### SDK

클라우드 API 3.0은 매칭되는 소프트웨어 개발 키트(SDK)를 제공하고 여러 가지 프로그래밍 언어를 지원하여 더욱 편리한 API 호출이 가능합니다.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| InternalError.CosError | 파일 정보 획득 실패. |
| InvalidParameter | 매개변수 오류. |

