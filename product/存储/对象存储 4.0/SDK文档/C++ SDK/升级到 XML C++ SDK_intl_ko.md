JSON C++ SDK와 비교해 보면 XML C++ SDK의 문서는 간단한 업그레이드가 아님을 아셨을 것입니다. XML C++ SDK는 아키텍처, 가용성 및 안전성 면에서 상당히 향상되었을 뿐만 아니라 사용 편의성, 강력함 그리고 전송 성능에서도 많은 개선을 이루었습니다. XML C++ SDK로 업그레이드하려면 아래 지침에 따라 C++ SDK의 업그레이드 작업을 완료하십시오.

## 기능 비교

XML C++ SDK와 JSON C++ SDK 기능 비교는 다음 표를 참조하십시오.

| 기능           |                              XML C++ SDK                              |                              JSON C++ SDK                              |
| -------------- | :----------------------------------------------------------: | :----------------------------------------------------------: |
| 파일 업로드       | 로컬 파일, 바이트 스트림, 입력 스트림 업로드 지원<br>같은 이름 파일 덮어쓰기<br>간편 업로드 최대 5G 지원<br>멀티파트 업로드 최대 48.82TB(50,000GB) 지원 | 로컬 파일 업로드 지원, 8M 이상의 파일은 파일 콘텐츠에 대해 멀티파트 업로드를 진행해야 함<br>같은 이름 파일 덮어쓰기 여부의 수동 구성이 필요<br>간편 업로드 최대 20MB 지원<br>멀티파트 업로드 최대 64GB 지원 |
| 버킷 기본 작업 |            버킷 생성<br>버킷 획득<br>버킷 삭제            |                            지원되지 않음                            |
| 버킷 ACL 작업  |   버킷 ACL 설정<br>버킷 ACL 설정 획득<br>버킷 ACL 설정 삭제    |                            지원되지 않음                            |
| 버킷 수명 주기 | 버킷 수명 주기 생성<br>버킷 수명 주기 획득<br>버킷 수명 주기 삭제 |                            지원되지 않음                            |
| 디렉터리 작업       |                            API가 별도로 제공되지 않음                             |               디렉터리 생성<br>디렉터리 조회<br>디렉터리 삭제               |

## 업그레이드 절차

아래 4단계를 수행하여 C++ SDK를 업그레이드하십시오.

**1. C++ SDK 업데이트**

[XML C++ SDK ](https://github.com/tencentyun/cos-cpp-sdk-v5)는 Poco 라이브러리를 사용하여 JSON C++ SDK의 curl 라이브러리를 대체합니다. [Poco 공식 웹사이트](https://pocoproject.org/download.html)에서 complete 버전의 Poco를 다운로드하고 다음 명령을 실행하여 Poco의 라이브러리와 헤더 파일을 설치하십시오.

```
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```
아니면, C++ SDK [시작 가이드](https://cloud.tencent.com/document/product/436/12301) 문서를 참고하여 적절한 설치 방식을 선택하십시오.

**2. SDK 구성 파일 변경**

XML C++ SDK와 JSON C++ SDK의 초기화 과정은 동일하지만 해당 구성 파일 "config.json" 내용은 다릅니다. XML C++ SDK 구성 파일에서 다음 변경 사항을 수정하십시오.

-  JSON C++ SDK의 "APPID" 구성 항목을 삭제합니다.
- `ConnectTimeoutInms`는 `CurlConnectTimeoutInms` 및 `CurlGlobalConnectTimeoutInms`를 대체하고, `ReceiveTimeoutInms`를 새로 추가합니다. Request 기본 클래스에도 해당 API를 설정할 수 있어, 서로 다른 작업에 대해서 수정을 진행할 수 있습니다.
- XML C++ SDK의 초기화 기본 매개변수는 "cos_sys_config.cpp"에 상세한 설명이 있습니다.
- JSON C++ SDK 및 XML C++ SDK의 해당 Region 설명은 서로 다르며, 상세한 구별은 아래 “버킷 이름 및 가용 영역 짧은 이름 변경”을 참조하십시오.

**3. 버킷 이름 및 가용 영역 약칭 변경**

XML C++ SDK의 버킷 이름과 가용 지역의 약칭은 JSON C++ SDK과 다르므로 상응하는 변경을 진행해야 합니다.

**버킷 Bucket**

XML C++ SDK 버킷 이름은 두 개의 부분으로 구성됩니다. 즉, 사용자 지정 문자열과 APPID의 두 부분이며 둘 다 대시 "-"로 연결됩니다. 예를 들어 `mybucket1-1250000000`이라면 그 중 `mybucket1`은 사용자 지정 문자열이고 `1250000000`은 APPID입니다.

>?APPID는 Tencent Cloud 계정의 계정 식별자 중 하나이며 클라우드 리소스를 연결하는 데 사용됩니다. 사용자가 Tencent Cloud 계정을 성공적으로 신청한 후 시스템은 자동으로 APPID를 사용자에게 할당합니다. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)의 [계정 정보]에서 APPID를 볼 수 있습니다.

버킷 구성은 다음 예제 코드를 참조하십시오.

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
// JSON C++ SDK의 AppID는 구성 파일에 기록된 것이며, JSON C++ SDK의 버킷 정의는 다음과 같습니다. string bucket = "mybucket1";
string bucket = "mybucket1-1250000000";
qcloud_cos::HeadBucketReq req(bucket_name);
qcloud_cos::HeadBucketResp resp;
qcloud_cos::CosResult result = cos.HeadBucket(req, &resp);
```

**버킷 가용 영역 약칭 Region**

XML C++ SDK의 버킷 가용 지역 약칭에 변화가 생기면, 초기화 시 버킷이 있는 지역의 약칭을 구성 파일의 `Region`으로 설정하십시오. 서로 다른 지역의 JSON C++ SDK 및 XML C++ SDK의 대응 관계는 다음 표와 같습니다.

| 지역             | XML C++ SDK 지역 짧은 이름      | JSON C++ SDK 지역 짧은 이름 |
| ---------------- | ---------------- | ----------- |
| 베이징 1지역(화북) | ap-beijing-1     | tj          |
| 베이징             | ap-beijing       | bj          |
| 상하이(화동)     | ap-shanghai      | sh          |
| 광저우(화남)     | ap-guangzhou     | gz          |
| 청두(서남)     | ap-chengdu       | cd          |
| 충칭             | ap-chongqing     | 없음          |
| 싱가포르           | ap-singapore     | sgp         |
| 홍콩             | ap-hongkong      | hk          |
| 토론토           | na-toronto       | ca          |
| 프랑크푸르트         | eu-frankfurt     | ger         |
| 뭄바이             | ap-mumbai        | 없음          |
| 서울             | ap-seoul         | 없음          |
| 실리콘 밸리             | na-siliconvalley | 없음          |
| 버지니아         | na-ashburn       | 없음          |
| 방콕             | ap-bangkok       | 없음          |
| 모스크바           | eu-moscow        | 없음          |

**4. API 변경**

XML SDK로 업그레이드한 뒤, 일부 작업의 API가 변경되었습니다. 실제 수요에 따라 그에 맞게 변경하십시오. 동시에 API를 캡슐화하여 SDK 사용 간편성을 높였습니다. 구체적인 내용은 예시와 [API 문서](https://cloud.tencent.com/document/product/436/12302)를 참조하십시오.

API의 주요 변경 사항은 다음과 같습니다.

**1)독립적인 디렉터리 API 없음**

XML SDK에서는 별도의 디렉토리 API를 더 이상 제공하지 않습니다. COS 자체가 파일 폴더와 디렉터리 개념이 없으며 COS는 업로드 객체 project/a.txt를 업로드하여 project 폴더를 만들지 않습니다.
사용자의 사용 습관을 충족시키기 위해 COS는 콘솔이나 COS browser와 같은 그래픽 도구에 ‘폴더’ 또는 ‘디렉터리’ 표시 방식을 시뮬레이션합니다. 구체적으로 키 값이 `project /`이고 내용은 비어 있는 객체를 생성하여 구현하며, 표시 방식은 기존 폴더와 유사합니다.

예: 객체 `project/doc/a.txt `를 업로드하고, 구분 기호 `/`는 [폴더]의 표시 방식을 시뮬레이션하여 project와 doc [폴더]fmf 콘솔에서 볼 수 있습니다. 그 중 doc는 project의 하위 폴더이며, a.txt 파일을 포함합니다.

따라서 파일 업로드 시나리오에서 사용하는 경우, 바로 업로드하면 되며, 먼저 폴더를 생성할 필요가 없습니다. 적용 시나리오에 폴더의 개념이 있으면 폴더를 생성하는 기능을 제공해야 합니다. 경로가 '/'로 끝나는 0KB의 파일을 업로드하면 됩니다. 그러면 GetBucket API를 사용할 때 해당 파일을 폴더로 사용할 수 있습니다.

**2) 멀티 스레드 업로드 및 다운로드 작업**

XML C++ SDK에서는 멀티 스레드 멀티파트 업로드 및 다운로드 작업을 캡슐화하고, `MultiUploadObjectReq` 및 `MultiGetObjectReq` API를 위해 API 디자인 및 전송 성능에 대해 최적화를 할 수 있습니다.

주요 특성:

- 파트 크기를 설정하여 멀티 스레드 업로드 및 다운로드 실행
- `MultiUploadObjectReq` API는 Init, Upload, Complete 및 Abort 작업을 포함한 멀티파트 업로드의 모든 API를 캡슐화합니다.

`MultiUploadObjectReq`로 업로드의 예제 코드:

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
string bucket_name = "alangz-1253960400";
string object_name = "object_key";
string local_file = "/data/test";
qcloud_cos::MultiUploadObjectReq req(bucket_name,object_name, local_file);
req.SetRecvTimeoutInms(1000 * 60);
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);
if (result.IsSucc()) {
    std::cout << "MultiUpload Succ." << std::endl;
    std::cout << resp.GetLocation() << std::endl;
    std::cout << resp.GetKey() << std::endl;
    std::cout << resp.GetBucket() << std::endl;
    std::cout << resp.GetEtag() << std::endl;
} else {
    std::cout << "MultiUpload Fail." << std::endl;
    // 어느 단계에서 특정 실패 정보 획득
    std::string resp_tag = resp.GetRespTag();
    if ("Init" == resp_tag) {
        // print result
    } else if ("Upload" == resp_tag) {
        // print result
    } else if ("Complete" == resp_tag) {
        // print result
    }
}
```

`MultiGetObjectReq`로 다운로드의 예제 코드:

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
string bucket_name = "alangz-1253960400";
string object_name = "object_key";
string file_path = "/data/test";
qcloud_cos::MultiGetObjectReq req(bucket_name,object_name, file_path);
qcloud_cos::MultiGetObjectResp resp;
qcloud_cos::CosResult result = cos.GetObject(req, &resp);
```

**3)서명 알고리즘이 다름**

일반적으로 수동으로 서명을 계산할 필요가 없지만, SDK의 서명을 프런트 엔드에 반환하는 경우 서명 알고리즘에 변화가 생겼다는 점에 유의하십시오. 서명은 더 이상 단일 서명과 다중 서명을 구분하지 않으며 서명의 유효 기간을 설정하여 보안성을 보장합니다. 구체적인 알고리즘은 [XML 서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.

**4) API 새로 추가**

XML C++ SDK는 API를 새로 추가하여 필요에 따라 호출할 수 있습니다. 다음을 포함합니다.

- 버킷 작업, PutBucketReq, GetBucketReq 등.
- 버킷 ACL의 작업, PutBucketACLReq, GetBucketACLReq 등.
- 버킷의 수명 주기 작업, PutBucketLifecycleReq, GetBucketLifecycleReq 등.

자세한 내용은 C++ SDK [API 문서](https://cloud.tencent.com/document/product/436/12302)를 참조하십시오.
