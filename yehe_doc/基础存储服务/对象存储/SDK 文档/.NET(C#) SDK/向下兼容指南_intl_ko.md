## 설명

NET SDK 5.4.23 버전부터, .NET Framework 4.0 및 이전 버전과의 호환성을 제공합니다. COSXML-Compatible.dll 라이브러리를 추가함으로써 .NET Framework 4.0 이후 버전 애플리케이션에서 실행할 수 있습니다.

>! 
> - 호환 환경은 NuGet 통합을 지원하지 않을 수 있습니다. 구체적인 통합 방법은 ‘참조 추가’를 참고하십시오.
> - 모든 고급 인터페이스(고급 업로드, 다운로드 재개 등)는 COSXML-Compatible.dll에서 사용할 수 없습니다.
> 

## 참조 추가

현재 .dll 파일을 수동으로 추가하는 통합 방법만 제공되며 통합 방법은 다음과 같습니다.
1. [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases)에서 COSXML-Compatible.dll 파일을 다운로드 합니다.
2. Visual Studio 프로젝트에서 **프로젝트**> **참조 추가**> **브라우징**> **COSXML-Compatible.dll**을 선택하여 .NET SDK를 추가합니다.

## 사용 방법

사용법은 기본적으로 .NET SDK의 일반 버전과 동일하며 다음 두 가지 사항에 주의가 필요합니다.

1. .NET Framework 4.0 및 이전 버전 환경에서는 HTTPS를 통한 COS 액세스에 문제가 있을 수 있으며, HTTPS 활성화 설정으로 인해 요청이 실패할 경우 HTTPS를 껐다가 다시 시도할 수 있습니다.
2. .NET 호환 버전은 고급 인터페이스에 대한 지원을 포함하지 않습니다. COS에 액세스하려면 다른 인터페이스를 사용하십시오. 호환되지 않는 인터페이스는 다음 표에 나와 있습니다.

| 네임스페이스           | 클래스                          | 설명                            |
| ----------------- | ---------------------------- | ------------------------------- |
| COSXML.Transfer   | COSXMLCopyTask               | 고급 Copy 인터페이스               |
| COSXML.Transfer   | COSXMLDownloadTask           | 고급 다운로드 인터페이스                |
| COSXML.Transfer   | COSXMLTask                   | 고급 인터페이스 추상 클래스             |
| COSXML.Transfer   | COSXMLUploadTask             | 고급 업로드 인터페이스               |
| COSXML.Transfer   | TransferManager              | 전송 작업 제어 클래스             |

## 기타 문제

호환 패키지는 현재 베타 단계이며, 사용 관련 다른 문제가 있는 경우 GitHub 프로젝트에 [issue](https://github.com/tencentyun/qcloud-sdk-dotnet/issues)를 제출하시기 바랍니다.
