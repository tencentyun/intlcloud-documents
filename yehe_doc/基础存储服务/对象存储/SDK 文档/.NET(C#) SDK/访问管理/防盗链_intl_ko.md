## 소개

본문은 버킷 Referer 에 대한 얼로우/블록리스트의 API 개요 및 SDK 예시 코드를 제공합니다.


| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 버킷 Referer 설정 | 버킷 Referer 얼로우 또는 블록리스트 설정 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 버킷 Referer 쿼리 | 버킷 Referer 얼로우 또는 블록리스트 쿼리 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버킷 Referer 설정

#### 기능 설명

.NET SDK를 사용하여 버킷에 대한 Referer 얼로우리스트 또는 블록리스트를 설정하고 버킷의 Referer 설정을 읽습니다.

>?
> - 버킷 링크 도용 방지 설정은 5.4.24 버전에서 지원됩니다. 새 버전의 SDK를 다운로드하고 [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases)로 이동하거나 [시작하기](https://intl.cloud.tencent.com/document/product/436/30594)를 참고하십시오.
> - 버전 업데이트 로그 조회는 [GitHub](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md)로 이동하십시오.
> 

#### 예시 코드

[//]: # ".cssg-snippet-get-service"
```cs
using COSXML.Model.Tag;
using COSXML.Model.Bucket;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class BucketRefererModel {

      private CosXml cosXml;

      BucketRefererModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 기본 리전을 설정합니다. COS 리전의 약칭은 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/6224
          .Build();
        
        string secretId = "SECRET_ID";   // Tencent Cloud API 키 SecretId. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        string secretKey = "SECRET_KEY"; // Tencent Cloud API 키 SecretKey. API 키를 얻으려면 https://console.cloud.tencent.com/cam/capi를 참고하십시오.
        long durationSecond = 600;          //매번 서명의 유효 기간을 요청하며, 단위는 초 입니다.
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 버킷 링크 도용 방지 설정
      public void PutBucketReferer()
      {
        //.cssg-snippet-body-start:[put-bucket-cors]
        try
        {
          // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
          string bucket = "examplebucket-1250000000";
          PutBucketRefererRequest request = new PutBucketRefererRequest(bucket);
          // 링크 도용 방지 규칙 설정
          RefererConfiguration configuration = new RefererConfiguration();
          // 링크 도용 방지 활성화 여부. 열거 값: Enabled, Disabled
          configuration.Status = "Enabled"; 
          // 링크 도용 방지 유형. 열거 값: Black-List, White-List
          configuration.RefererType = "White-List"; 
          // 적용 도메인 리스트. 여러 도메인 및 접두사 매칭 지원, 포트가 있는 도메인 및 IP 지원, 와일드카드* 지원, 2단계 수준 도메인 또는 다중 단계 도메인에 대해 와일드카드 수행
          configuration.domainList = new DomainList(); 
          // 유효한 단일 도메인. 예: www.qq.com/example, 192.168.1.2:8080, *.qq.com
          configuration.domainList.AddDomain("*.domain1.com");
          configuration.domainList.AddDomain("*.domain2.com");
          // 빈 Referer 액세스 허용 여부. 열거 값: Allow, Deny, 기본값: Deny
          configuration.EmptyReferConfiguration = "Deny";
          request.SetRefererConfiguration(configuration);
          //실행 요청
          PutBucketRefererResult result = cosXml.PutBucketReferer(request);
          //요청 완료
          Console.WriteLine(result.GetResultInfo());
        }
        catch (COSXML.CosException.CosClientException clientEx)
        {
          //요청 실패
          Console.WriteLine("CosClientException: " + clientEx);
        }
        catch (COSXML.CosException.CosServerException serverEx)
        {
          //요청 실패
          Console.WriteLine("CosServerException: " + serverEx.GetInfo());
        }
        
        //.cssg-snippet-body-end
      }

      /// 버킷 링크 도용 방지 규칙 가져오기
      public void GetBucketReferer()
      {
        //.cssg-snippet-body-start:[get-bucket-cors]
        try
        {
          // 버킷 이름. 형식: bucketname-APPID. APPID는 https://console.cloud.tencent.com/developer를 참고하십시오.
          string bucket = "examplebucket-1250000000";
          GetBucketRefererRequest request = new GetBucketRefererRequest(bucket);
          // 실행 요청
          GetBucketRefererResult result = cosXml.GetBucketReferer(request);
          Console.WriteLine(result.GetResultInfo());
          // Status 매개변수
          Console.WriteLine(result.refererConfiguration.Status);
          // Referer 목록 유형
          Console.WriteLine(result.refererConfiguration.RefererType);
          // 목록 중 도메인 나열
          foreach (string domain in result.refererConfiguration.domainList.domains)
          {
            Console.WriteLine(domain);
          }
        }
        catch (COSXML.CosException.CosClientException clientEx)
        {
          //요청 실패
          Console.WriteLine("CosClientException: " + clientEx);
        }
        catch (COSXML.CosException.CosServerException serverEx)
        {
          //요청 실패
          Console.WriteLine("CosServerException: " + serverEx.GetInfo());
        }
        
        //.cssg-snippet-body-end
      }
    
      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        BucketRefererModel m = new BucketRefererModel();
        /// 버킷 크로스 도메인 규칙 설정
        m.PutBucketReferer();
        /// 버킷 크로스 도메인 규칙 가져오기
        m.GetBucketReferer();
        // .cssg-methods-pragma
      }
    }
}

```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketReferer.cs)를 참고하십시오.
>
