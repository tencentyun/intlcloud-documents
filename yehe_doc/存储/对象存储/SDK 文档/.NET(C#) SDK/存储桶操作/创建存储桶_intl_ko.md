## 소개

본문은 버킷 생성 관련 API 개요 및 SDK 샘플 코드를 제공합니다.


| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | 버킷 생성         | 지정 계정에서 버킷 생성         |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버킷 생성

#### 기능 설명

지정된 계정에 버킷을 생성합니다. 동일한 사용자 계정으로 여러 개의 버킷을 생성할 수 있으며, 최대 200개(리전 구분 없음) 생성 가능하며 버킷의 객체 수에는 제한이 없습니다. 버킷 생성은 빈도가 낮은 작업으로 일반적으로 콘솔에서 Bucket을 생성하고 SDK에서 객체 작업을 수행하는 것을 추천합니다.

#### 예시 코드

[//]: # (.cssg-snippet-put-bucket)
```cs
using COSXML.Common;
using COSXML.Model.Bucket;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class PutBucketModel {

      private CosXml cosXml;

      PutBucketModel() {
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

      /// 버킷 생성
      public void PutBucket()
      {
        //.cssg-snippet-body-start:[put-bucket]
        try
        {
          // 버킷 이름. 형식: BucketName-APPID. APPID를 얻으려면 다음을 참고하십시오. https://console.cloud.tencent.com/developer
          string bucket = "examplebucket-1250000000";
          PutBucketRequest request = new PutBucketRequest(bucket);
          //실행 요청
          PutBucketResult result = cosXml.PutBucket(request);
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
        PutBucketModel m = new PutBucketModel();

        /// 버킷 생성
        m.PutBucket();
        // .cssg-methods-pragma
      }
    }
}

```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PutBucket.cs)을 참고하십시오.
>


