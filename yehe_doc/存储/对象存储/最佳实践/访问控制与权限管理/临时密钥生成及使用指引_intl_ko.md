>임시 키를 사용해 액세스 권한을 부여하는 경우, 반드시 업무 수요에 따라 최소 권한 부여를 원칙으로 권한을 부여해야 합니다. 직접 모든 리소스(`(resource:*)` 또는 모든 작업`(action:*)`에 대한 권한을 부여하는 경우 권한 범위가 너무 커 데이터 보안에 대한 리스크가 발생할 수 있습니다.

## 임시 키

[임시 키(임시 액세스 자격 증명)](https://intl.cloud.tencent.com/document/product/598/35838)는 CAM 클라우드 API에서 제공하는 인터페이스를 통해 획득하는 권한이 부여된 키입니다.
 COS API는 임시 키를 사용해 서명을 컴퓨팅해 COS API 요청을 전송하는 데 사용합니다.
 COS API 요청은 임시 키를 사용해 서명 컴퓨팅 시, 다음 3개의 임시 키 인터페이스 반환 정보 획득에 사용하는 필드가 필요합니다.
- TmpSecretId
- TmpSecretKey
- Token 

## 임시 키 사용의 장점

Web, iOS, Android에서 COS를 사용할 때, 고정 키를 사용해 서명을 컴퓨팅하는 경우 권한을 효과적으로 제어할 수 없을 뿐 아니라, 영구 키를 클라이언트 코드에 삽입하는 경우 커다란 유출 위험이 존재하게 됩니다. 임시 키 방식을 사용하면 권한 제어 문제를 편리하고 효과적으로 해결할 수 있습니다.
예를 들어, 임시 키 신청 과정에서 권한 정책 [policy](https://intl.cloud.tencent.com/document/product/436/30580) 필드 설정을 통해 작업 및 리소스를 제한하고, 권한을 지정된 범위로 제한할 수 있습니다.

COS API 권한 부여 정책과 관련해서는 다음을 참조하십시오.
- [COS API 임시 키를 사용한 권한 부여 정책 가이드](https://intl.cloud.tencent.com/document/product/436/30580)
- [자주 볼 수 있는 시나리오에서의 임시 키를 사용한 권한 부여 정책 예시](https://intl.cloud.tencent.com/document/product/436/30580#.E5.B8.B8.E8.A7.81.E5.9C.BA.E6.99.AF.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5)

## 임시 키 획득

임시 키는 제공되는 [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk) 방식을 통해 획득할 수 있으며, 직접 [STS 클라우드 API](https://intl.cloud.tencent.com/document/product/598/35838) 요청 방식으로도 획득할 수 있습니다.


>예시에서는 Java SDK를 사용하였으며, GitHub에서 SDK 코드(버전)을 획득해야 합니다. 해당 SDK 버전을 찾을 수 없다는 안내가 표시되는 경우, GitHub에서 상응하는 버전의 SDK를 획득하였는지 확인하십시오.

### COS STS SDK 

COS는 STS에 대한 SDK와 샘플을 제공합니다. 현재 Java, Nodejs, PHP, Python, Go 등 여러 가지 언어 샘플을 제공하고 있으며, 자세한 내용은 [COS STS SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk)를 참조하고, 각 SDK별 사용 설명은 Github의 README와 샘플을 참조하십시오.

>STS SDK는 STS 인터페이스 자체의 버전별 차이점을 차단하기 위해 반환 매개변수 구조가 STS 인터페이스와 완벽하게 일치하지 않습니다. 자세한 내용은 [Java SDK 문서](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java) 설명을 참조하십시오.

Java SDK를 사용한다고 가정하고, 먼저 [Java SDK](https://github.com/tencentyun/qcloud-cos-sts-sdk/tree/master/java)를 다운로드한 후 실행하여 다음 예시와 같이 임시 키를 획득합니다.

```java
// github에서 제공하는 maven 통합 방법에 따라 java sts sdk 가져오기 
import java.util.*;
import org.json.JSONObject; 
import com.tencent.cloud.CosStsClient;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

		try {
		    // 사용자의 SecretId로 변경 
		    config.put("SecretId", "AKIDHTVVaV34t5G45YOb6y65R6e3****"));
		    // 사용자의 SecretKey로 변경
		    config.put("SecretKey", "PdkhT9e2t43t45B42FE79rZCfy6****");
		
		    // 임시 키의 유효 시간은 초 단위입니다. 기본값은 1800초이며, 현재 루트 계정에서 최대 2시간(7200초), 서브 계정에서 최대 36시간(129600초)까지 설정 가능합니다.
		    config.put("durationSeconds", 1800);
		
		    // 사용자의 bucket으로 변경
		    config.put("bucket", "examplebucket-1250000000");
		    // bucket 소재 리전으로 변경
		    config.put("region", "ap-guangzhou");
		
		    // 여기서 허용된 경로의 접두사로 바꾸면 자신의 웹 사이트의 사용자 로그인 상태에 따라 업로드가 허용된 구체적 경로를 판단할 수 있습니다. 예: a.jpg 또는 a/* 또는 *
			// '*'를 입력하면 사용자가 모든 리소스에 액세스하는 것을 허용하게 됩니다. 업무에 필요한 경우가 아니면 최소 권한 원칙에 따라 사용자에게 적합한 액세스 권한 범위를 부여하십시오.
		    config.put("allowPrefix", "a.jpg");
		
		    // 키 권한 리스트. 간편 업로드, 폼 업로드 및 멀티파트 업로드 시에는 다음과 같은 권한이 필요합니다. 기타 권한 리스트는 https://intl.cloud.tencent.com/document/product/436/30580을 참조하십시오.
		    String[] allowActions = new String[] {
		            // 간편 업로드
		            "name/cos:PutObject",
				    // 폼 업로드, 미니프로그램 업로드
					"name/cos:PostObject",
		            // 멀티파트 업로드
		            "name/cos:InitiateMultipartUpload",
		            "name/cos:ListMultipartUploads",
		            "name/cos:ListParts",
		            "name/cos:UploadPart",
		            "name/cos:CompleteMultipartUpload"
		    };
		    config.put("allowActions", allowActions);
		
		    JSONObject credential = CosStsClient.getCredential(config);
			//임시 키 정보를 성공적으로 반환하면, 다음과 같은 키 정보가 출력됩니다.
		    System.out.println(credential);
		} catch (Exception e) {
			//실패 시 이상 경고가 발생합니다.
		    throw new IllegalArgumentException("no valid secret !");
		}
    }
}
```

### 임시 키를 사용한 COS 액세스

 COS API에서 임시 키를 사용해 COS 서비스에 액세스하는 경우, x-cos-security-token 필드를 통해 임시 sessionToken를 전달하고 임시 SecretId와 SecretKey로 서명을 컴퓨팅합니다.

임시 키를 사용하여 COS에 액세스하는 COS Java SDK 예시는 다음과 같습니다.
>다음 예시 실행 전 [Github 프로젝트](https://github.com/tencentyun/cos-java-sdk-v5)에서 Java SDK 설치 패키지를 다운로드하십시오.

```java
// github에서 제공하는 maven 통합 방법에 따라 cos xml java sdk 가져오기
import com.qcloud.cos.*;
import com.qcloud.cos.auth.*;
import com.qcloud.cos.exception.*;
import com.qcloud.cos.model.*;
import com.qcloud.cos.region.*;
public class Demo {
    public static void main(String[] args) throws Exception {

        // 사용자 기본 정보
        String tmpSecretId = "COS_SECRETID";   // STS 인터페이스에서 반환하는 임시 SecretId로 변경 
        String tmpSecretKey = "COS_SECRETKEY";  // STS 인터페이스에서 반환하는 임시 SecretKey로 변경
        String sessionToken = "Token";  // STS 인터페이스에서 반환하는 임시 Token으로 변경

        // 1. 사용자 자격 정보 초기화(secretId, secretKey)
        COSCredentials cred = new BasicCOSCredentials(tmpSecretId, tmpSecretKey);
        // 2. bucket 리전 설정, 자세한 정보는 COS 리전 https://intl.cloud.tencent.com/document/product/436/6224 참조
        ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
        // 3 cos 클라이언트 생성
        COSClient cosclient = new COSClient(cred, clientConfig);
        // bucket 이름에는 반드시 appid가 포함됨
        String bucketName = "examplebucket-1250000000";

        String key = "doc/picture.jpg";
        // object 업로드, 20M 이상의 파일은 해당 인터페이스를 사용해 업로드하는 것을 권장
        File localFile = new File("src/test/resources/text.txt");
        PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

        // x-cos-security-token header 필드 설정
        ObjectMetadata objectMetadata = new ObjectMetadata();
        objectMetadata.setSecurityToken(sessionToken);
        putObjectRequest.setMetadata(objectMetadata);

        try {
            PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
            // 성공: putobjectResult에서 파일의 etag 반환
            String etag = putObjectResult.getETag();
        } catch (CosServiceException e) {
			//실패 시 CosServiceException 팝업
            e.printStackTrace();
        } catch (CosClientException e) {
			//실패 시 CosClientException 팝업
            e.printStackTrace();
        }

        // 클라이언트 종료
        cosclient.shutdown();

    }
}
```
