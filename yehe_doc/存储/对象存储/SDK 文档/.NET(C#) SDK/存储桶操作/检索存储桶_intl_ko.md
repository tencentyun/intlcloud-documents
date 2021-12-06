## 소개

본문은 버킷 인덱스 관련 API 개요 및 SDK 샘플 코드를 제공합니다.


| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 버킷 및 해당 권한 인덱스 | 버킷 존재 여부 및 액세스 권한 보유 여부 인덱스 |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버킷 및 해당 권한 인덱스

#### 기능 설명

HEAD Bucket은 해당 버킷이 존재하는지 여부와 액세스 권한 여부 확인을 요청하며, 다음과 같은 상황이 있을 수 있습니다.

- 버킷이 존재하며 읽기 권한이 있는 경우 HTTP 상태 코드 200가 반환됩니다.
- 버킷에 대한 읽기 권한이 없는 경우 HTTP 상태 코드 403가 반환됩니다.
- 버킷이 존재하지 않는 경우 HTTP 상태 코드 404가 반환됩니다.

#### 예시 코드

[//]: # (.cssg-snippet-head-bucket)
```cs
using COSXML.Model.Bucket;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class HeadBucketModel {

      private CosXml cosXml;

      HeadBucketModel() {
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

      /// 버킷 정보 가져오기
      public void HeadBucket()
      {
        //.cssg-snippet-body-start:[head-bucket]
        try
        {
          // 버킷 이름. 형식: BucketName-APPID. APPID를 얻으려면 다음을 참고하십시오. https://console.cloud.tencent.com/developer
          string bucket = "examplebucket-1250000000";
          HeadBucketRequest request = new HeadBucketRequest(bucket);
          //실행 요청
          HeadBucketResult result = cosXml.HeadBucket(request);
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
      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        HeadBucketModel m = new HeadBucketModel();

        /// 버킷 정보 가져오기
        m.HeadBucket();
        // .cssg-methods-pragma
      }
    }
}
```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/HeadBucket.cs)를 참고하십시오.
>
