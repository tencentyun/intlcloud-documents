## 소개

본문은 버킷 리스트 쿼리 관련 API 개요 및 SDK 샘플 코드를 제공합니다.

| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service(List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | 버킷 리스트 조회     | 특정 계정의 모든 버킷 리스트 조회     |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버킷 리스트 조회

#### 기능 설명

특정 계정의 모든 버킷 리스트 쿼리에 사용됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-get-service)
```cs
using COSXML.Model.Tag;
using COSXML.Model.Service;
using COSXML.Auth;
using System;
using COSXML;
using System.Collections.Generic;

namespace COSSnippet
{
    public class GetServiceModel {

      private CosXml cosXml;

      GetServiceModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 기본 리전을 설정합니다. COS 리전의 약칭은 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/6224  
          .Build();
        
        string secretId = "SECRET_ID";   // Tencent Cloud API 키 SecretId. API 키를 얻으려면 다음을 참고하십시오. https://console.cloud.tencent.com/cam/capi
        string secretKey = "SECRET_KEY"; // Tencent Cloud API 키 SecretKey. API 키를 얻으려면 다음을 참고하십시오. https://console.cloud.tencent.com/cam/capi
        long durationSecond = 600;           //각 서명 요청의 유효 시간. 단위: 초.
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 버킷 리스트 가져오기
      public void GetService()
      {
        //.cssg-snippet-body-start:[get-service]
        try
        {
          GetServiceRequest request = new GetServiceRequest();
          //실행 요청.
          GetServiceResult result = cosXml.GetService(request);
          //모든 buckets 획득
          List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
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

      /// 리전의 버킷리스트 가져오기
      public void GetRegionalService()
      {
        //.cssg-snippet-body-start:[get-regional-service]
        try
        {
          GetServiceRequest request = new GetServiceRequest();
          string region = "ap-guangzhou";
          request.host = $"cos.{region}.myqcloud.com";
          //실행 요청
          GetServiceResult result = cosXml.GetService(request);
          //모든 buckets 획득
          List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
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
        GetServiceModel m = new GetServiceModel();

        /// 버킷 리스트 가져오기
        m.GetService();
        /// 리전의 버킷 리스트 가져오기
        m.GetRegionalService();
        // .cssg-methods-pragma
      }
    }
}

```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetService.cs)을 참고하십시오.
>

