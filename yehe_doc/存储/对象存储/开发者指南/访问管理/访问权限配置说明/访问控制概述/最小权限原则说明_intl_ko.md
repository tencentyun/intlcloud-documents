## 개요

Cloud Object Storage(COS)를 사용 시 임시 키를 사용해 사용자에게 해당 리소스의 작업 권한을 부여하거나 서브 계정 또는 협업 파트너에게 적합한 사용자 정책을 부여해, 그들이 COS의 리소스를 작업할 수 있도록 허용해야 할 수 있습니다. 또한 버킷에 관련 버킷 정책을 추가해 지정된 사용자가 버킷에서 지정된 작업을 하거나 지정된 리소스를 작업하도록 해야 할 수 있습니다. 이와 같은 권한 설정 시, 반드시 **최소 권한 원칙**을 준수해 데이터 자산 보안을 확보하십시오.

**최소 권한 원칙**이란, 권한을 부여할 때 권한 범위를 명확히 하여 **지정 사용자**에게 **어떤 조건**에서 **어떤 작업**을 수행하고 **어떤 리소스**에 액세스할지에 대해 권한을 명확하게 부여하는 것을 의미합니다.

## 주의 사항
사용자가 지정된 작업(예: `action:GetObject`)만 수행하거나 지정된 리소스(예: `resource:examplebucket-1250000000/exampleobject.txt`)에 액세스할 수 있도록 최소 권한 원칙을 엄격히 따르는 것이 좋습니다. 
과도한 권한으로 인한 예기치 않은 무단 작업으로 인한 데이터 보안 위험을 방지하려면 사용자에게 모든 리소스(예: `resource:*`)에 대한 액세스 권한을 부여하거나 모든 작업(예: `action:*`)을 수행하지 않는 것이 좋습니다.

잠재된 데이터 보안 리스크 예시는 다음과 같습니다.
- 데이터 유출: 사용자에게 `examplebucket-1250000000/data/config.json` 및 `examplebucket-1250000000/video/`와 같은 지정된 리소스를 다운로드할 수 있도록 권한을 부여하고 싶지만 권한 정책에 `examplebucket-1250000000/*`을 포함하면 버킷의 모든 객체는 승인 없이 다운로드될 수 있어 예기치 않은 데이터 유출이 발생할 수 있습니다.
- 데이터 덮어쓰기: 사용자에게 `examplebucket-1250000000/data/config.json` 및 `examplebucket-1250000000/video/`를 업로드할 수 있는 권한을 부여하고 싶지만 권한 정책에 `examplebucket-1250000000/*`을 포함하면 승인 없이 버킷의 모든 객체를 업로드할 수 있으므로 의도하지 않은 객체를 덮어쓸 수 있습니다. 이러한 위험을 방지하기 위해 최소 권한 원칙을 따르는 것 외에도 [버전 제어 개요](https://intl.cloud.tencent.com/document/product/436/19883)에 설명된 대로 추적을 위해 모든 버전의 데이터를 유지할 수 있습니다.
- 권한 유출: 사용자가 버킷(`cos:GetBucket`)의 객체를 나열할 수 있는 권한을 부여하고 싶지만 권한 정책에서 `cos:*`를 구성하면 버킷 재승인, 객체 삭제 및 버킷 삭제를 포함하여 버킷에 대한 모든 작업이 허용되므로 데이터가 매우 위험해집니다.


## 사용 가이드

최소 권한 원칙에 따라 정책에서 다음 정보를 명확히 지정해야 합니다.

- 위탁자(principal): 권한을 부여할 서브 계정(사용자 ID 필요), 협업 파트너(사용자 ID 필요), 익명 사용자 또는 사용자 그룹을 지정해야 합니다. 액세스에 임시 키를 사용하는 경우에는 필요하지 않습니다.
- 명령(statement): 해당 매개변수를 입력합니다.
	-  효력(effect): 정책이 allow인지 deny인지 지정해야 합니다.
	-  작업(action): 허용 또는 거부할 동작을 지정해야 합니다. 하나의 API 작업 또는 일련의 API 작업일 수 있습니다.
	-  리소스(resource): 권한이 부여된 리소스를 지정해야 합니다. 리소스는 6개 세그먼트 형식으로 설명됩니다. 리소스를 특정 파일(예: `exampleobject.jpg`) 또는 디렉터리(예: `examplePrefix/*`)로 설정할 수 있습니다. 필요한 경우가 아니면 `*` 와일드카드를 사용하여 모든 리소스에 대한 액세스 권한을 사용자에게 부여하지 마십시오.
	-  조건(condition): 정책의 효력이 발생하는 규제 조건을 기술합니다. 조건에는 오퍼레이터, 작업 키와 작업 값 구성이 포함됩니다. 조건 값은 시간, IP 주소 등의 정보를 포함합니다.

### 임시 키 최소 권한 가이드

임시 키 신청 과정에서 권한 정책 [Policy](https://intl.cloud.tencent.com/document/product/1150/49452) 필드 설정을 통해 작업 및 리소스를 제한하고, 권한을 지정된 범위로 제한할 수 있습니다. 임시 키 생성 관련 자세한 설명은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 문서를 참고하십시오.

#### 권한 부여 예시

#### Java용 SDK를 사용하여 지정된 객체에 액세스할 수 있는 사용자 권한 부여

Java SDK를 사용하여 사용자에게 `examplebucket-1250000000` 버킷의 `exampleObject.txt` 객체를 다운로드할 수 있는 권한을 부여하려면 구성 코드는 다음과 같아야 합니다.

```
// github에서 제공하는 maven 통합 방법에 따라 java sts sdk 가져오기 
import java.util.*;
import org.json.JSONObject; 
import com.tencent.cloud.CosStsClient;

public class Demo {
    public static void main(String[] args) {
        TreeMap<String, Object> config = new TreeMap<String, Object>();

        try {
            String secretId = System.getenv("secretId");//사용자 SecretId. 리스크를 줄이기 위해 서브 계정 키를 사용하고 최소 권한 원칙을 따르는 것이 좋습니다. 서브 계정 키를 가져오는 방법에 대한 자세한 내용은 다음을 참고하십시오. https://cloud.tencent.com/document/product/598/37140
            String secretKey = System.getenv("secretKey");//사용자 SecretKey. 리스크를 줄이기 위해 서브 계정 키를 사용하고 최소 권한 원칙을 따르는 것이 좋습니다. 서브 계정 키를 가져오는 방법에 대한 자세한 내용은 다음을 참고하십시오. https://cloud.tencent.com/document/product/598/37140
            // 자신의 SecretId로 교체 
            config.put("SecretId", secretId);
            // 자신의 SecretKey로 교체
            config.put("SecretKey", secretKey);

            // 임시 키의 유효 기간(초), 기본값: 1800; 최대값: 7200
            config.put("durationSeconds", 1800);

            // 자신의 bucket으로 교체
            config.put("bucket", "examplebucket-1250000000");
            // bucket 소재 리전으로 교체
            config.put("region", "ap-guangzhou");

            // 허용되는 경로 접두사(예: a.jpg, a/* 또는 *)로 변경합니다. 로그인 상태에 따라 업로드 경로를 결정할 수 있습니다.
            // ‘*’를 입력하면 사용자가 모든 리소스에 액세스할 수 있습니다. 업무에 필요한 경우가 아니면 최소 권한 원칙에 따라 필요한 제한된 권한만 사용자에게 부여합니다.
            config.put("allowPrefix", "exampleObject.txt");

            // 키 권한 리스트. 단순 업로드, 양식을 이용한 업로드 및 멀티 파트 업로드에 필요한 권한은 다음과 같습니다. 기타 권한 리스트는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/31923
            String[] allowActions = new String[] {
                    // 데이터 다운로드
                    "name/cos:GetObject"
            };
            config.put("allowActions", allowActions);

            JSONObject credential = CosStsClient.getCredential(config);
            // 성공하면 아래와 같이 임시 키 정보가 반환되어 출력됩니다
            System.out.println(credential);
        } catch (Exception e) {
            //실패 시 예외가 발생합니다
            throw new IllegalArgumentException("no valid secret !");
        }
    }
}
```

#### API를 사용하여 지정된 객체에 대한 액세스 권한 부여

API를 사용하여 `examplebucket-1250000000` 버킷의 `exampleObject.txt` 객체와 `examplePrefix` 디렉터리의 모든 객체를 다운로드할 수 있는 권한을 사용자에게 부여하려면 액세스 정책은 다음과 같아야 합니다.

```shell
{
  "version": "2.0",
  "statement": [
    {
      "action":[
        "name/cos:GetObject"
      ],
      "effect": "allow",
      "resource":[
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ]
}
```

### 사전 서명 최소 권한 가이드

사전 서명된 URL을 통해 임시 업로드 및 다운로드 작업을 구현할 수 있습니다. 또한 사전 서명된 URL을 누구에게나 전달할 수 있으며 유효한 사전 서명된 URL을 받는 사람은 누구나 객체를 업로드하거나 다운로드할 수 있습니다.

>!임시 키와 영구 키를 모두 사용하여 사전 서명된 URL을 생성할 수 있지만, 최소 권한 가이드 [임시 키 생성](https://intl.cloud.tencent.com/document/product/436/14048)을 준수하여, 임시 키를 사용하여 사전 서명을 계산합니다. 보안 리스크를 방지하기 위해 과도한 권한을 가진 영구 키를 사용하지 마십시오.

#### 권한 부여 예시

#### 사전 서명된 URL을 사용하여 사용자에게 객체 다운로드 권한 부여

임시 키를 사용해 서명이 있는 다운로드 링크를 생성하고, 반환할 일부 공용 헤더(예: content-type, content-language)를 덮어쓰도록 설정합니다. 다음은 Java 예시 코드입니다.

```java
// 획득한 임시 키(tmpSecretId, tmpSecretKey, sessionToken) 전송
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// bucket 리전 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오.
// clientConfig에 region, https(기본값: http), 타임아웃, 프록시 등을 설정하는 set 메소드가 포함되어 있습니다. 사용 시 소스 코드 또는 FAQ의 Java SDK 부분을 참고하십시오.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// https 프로토콜을 사용하는 URL을 생성할 경우, 이 행을 설정하길 권장합니다.
// clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성.
COSClient cosClient = new COSClient(cred, clientConfig);
// 버킷의 이름 생성 형식: BucketName-APPID 
String bucketName = "examplebucket-1250000000";
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 다운로드 시 반환하는 http 헤더 설정
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
// 반환 헤더에 포함되는 파일명 정보 설정
String responseContentDispositon = "filename=\"exampleobject\"";
String responseCacheControl = "no-cache";
String cacheExpireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24L * 3600L * 1000L));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(cacheExpireStr);
req.setResponseHeaders(responseHeaders);
// 서명 만료 시간 설정(옵션). 설정하지 않을 경우 기본적으로 ClientConfig의 서명 만료 시간(1시간)을 사용합니다.
// 본 예시에서는 30분 후 만료로 설정합니다.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

### 사용자 정책 최소 권한 가이드

사용자 정책은 [CAM 콘솔](https://console.cloud.tencent.com/cam/policy)에 추가된 사용자 권한 정책으로, 사용자가 COS 리소스에 액세스할 수 있는 권한을 부여하는 데 사용됩니다. 사용자 액세스 정책 개요의 설정에 관한 자세한 설명은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023) 문서를 참고하십시오.

#### 권한 부여 예시

#### 계정에 지정된 객체에 액세스할 수 있는 권한 부여

UIN이 `100000000001`인 계정에 `examplebucket-1250000000` 버킷의 `exampleObject.txt` 객체를 다운로드할 수 있는 권한을 부여하려면 액세스 정책은 다음과 같아야 합니다.
```shell
{
   "version": "2.0",
   "principal":{
      "qcs":[
         "qcs::cam::uin/100000000001:uin/100000000001"
      ]
   },
    "statement": [
        {
            "action":[
                "name/cos:GetObject"
            ],
            "effect": "allow",
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/exampleObject.txt"
            ]
        }
    ]
}
```

#### 서브 계정에 지정된 디렉터리에 대한 액세스 권한 부여

UIN이 `100000000011`인 서브 계정(루트 계정 UIN: `100000000001`)에게 `examplebucket-1250000000` 버킷의 `examplePrefix` 디렉터리에 있는 객체를 다운로드할 수 있는 권한을 부여하려면 액세스 정책은 다음과 같아야 합니다.

```shell
{
   "version": "2.0",
   "principal":{
      "qcs":[
         "qcs::cam::uin/100000000001:uin/100000000011"
      ]
   },
    "statement": [
        {
            "action":[
                "name/cos:GetObject"
            ],
            "effect": "allow",
            "resource":[
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000.ap-guangzhou.myqcloud.com/examplePrefix/*"
            ]
        }
    ]
}
```

### 버킷 정책 최소 권한 가이드

버킷 정책은 버킷에서 설정한 액세스 정책으로, 지정 사용자가 버킷 및 버킷 내 리소스에 대해 지정된 작업을 할 수 있도록 허용합니다. 버킷 정책 설정은 [버킷 정책 추가](https://intl.cloud.tencent.com/document/product/436/30927) 문서를 참고하십시오.

#### 권한 부여 예시

#### 서브 계정에 지정된 객체에 대한 액세스 권한 부여

UIN이 `100000000011`인 서브 계정(루트 계정 UIN: `100000000001`)에게 `examplebucket-1250000000` 버킷의 `exampleObject.txt` 객체와 `examplePrefix` 디렉터리의 모든 객체를 다운로드할 수 있는 권한을 부여하려면 액세스 정책은 다음과 같아야 합니다.

```shell
{
  "Statement":[
    {
      "Action":[
        "name/cos:GetObject"
      ],
      "Effect": "allow",
      "Principal":{
        "qcs":[
          "qcs::cam::uin/100000000001:uin/100000000011"
        ]
      },
      "Resource":[
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/exampleObject.txt",
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/examplePrefix/*"
      ]
    }
  ],
  "version": "2.0"
}
```
