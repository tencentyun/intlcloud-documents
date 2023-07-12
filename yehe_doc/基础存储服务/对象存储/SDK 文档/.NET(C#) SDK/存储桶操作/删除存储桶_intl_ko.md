## 소개

본문은 버킷 삭제 관련 API 개요 및 SDK 샘플 코드를 제공합니다.


| API                                                          | 작업명             | 작업 설명                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 버킷 삭제         | 지정 계정의 빈 버킷 삭제           |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 버킷 삭제

#### 기능 설명

지정된 버킷을 삭제합니다(DELETE Bucket).

>! 버킷 삭제 전, 버킷에 저장되어 있는 데이터와 업로드가 완료되지 않은 블록 데이터를 모두 삭제하였는지 확인하십시오. 모두 삭제되지 않은 경우 버킷이 삭제되지 않습니다.
>

#### 예시 코드

[//]: # (.cssg-snippet-delete-bucket)
```cs
using COSXML.Model.Bucket;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class DeleteBucketModel {

      private CosXml cosXml;

      DeleteBucketModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 기본 리전을 설정합니다. COS 리전 약칭을 참고하십시오. https://cloud.tencent.com/document/product/436/6224 
          .Build();
        
        string secretId = "SECRET_ID";   // Tencent Cloud API 키 SecretId. API 키 가져오기를 참고하십시오. https://console.cloud.tencent.com/cam/capi
        string secretKey = "SECRET_KEY"; // Tencent Cloud API 키 SecretKey. API 키 가져오기를 참고하십시오. https://console.cloud.tencent.com/cam/capi
        long durationSecond = 600;           //각 서명 요청의 유효 시간. 단위: 초.
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 버킷 삭제
      public void DeleteBucket()
      {
        //.cssg-snippet-body-start:[delete-bucket]
        try
        {
          // 버킷 이름. 형식: BucketName-APPID. APPID 가져오기를 참고하십시오. https://console.cloud.tencent.com/developer
          string bucket = "examplebucket-1250000000";
          DeleteBucketRequest request = new DeleteBucketRequest(bucket);
          //실행 요청.
          DeleteBucketResult result = cosXml.DeleteBucket(request);
          //요청 완료.
          Console.WriteLine(result.GetResultInfo());
        }
        catch (COSXML.CosException.CosClientException clientEx)
        {
          //요청 실패.
          Console.WriteLine("CosClientException: " + clientEx);
        }
        catch (COSXML.CosException.CosServerException serverEx)
        {
          //요청 실패.
          Console.WriteLine("CosServerException: " + serverEx.GetInfo());
        }
        
        //.cssg-snippet-body-end
      }
      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        DeleteBucketModel m = new DeleteBucketModel();

        /// 버킷 삭제
        m.DeleteBucket();
        // .cssg-methods-pragma
      }
    }
}

```

>? 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteBucket.cs)을 참고하십시오.
>

