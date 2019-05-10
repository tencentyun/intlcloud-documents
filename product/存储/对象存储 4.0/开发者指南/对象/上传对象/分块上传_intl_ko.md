## 적용 시나리오

멀티파트 업로드는 약한 네트워크 또는 높은 대역폭 환경에서 대형 객체를 업로드하는 데 적합합니다. COS 콘솔 및 SDK는 단일 객체를 일련의 멀티파트로 나뉘어 업로드할 수 있게 하며, 객체를 자체로 분할하고 API를 호출하여 각 멀티파트를 업로드할 수도 있습니다. 멀티파트 업로드에는 다음과 같은 이점이 있습니다.

- 약한 네트워크 환경에서 멀티파트 크기가 작으면 네트워크 오류로 인한 중단 영향을 낮춰 객체 업로드 재개를 구현합니다.
- 높은 대역폭 환경에서 다중 객체 파트 업로드는 대역폭을 충분히 이용할 수 있으며 순서가 엇바뀌어 업로드해도 최종 결합 객체에는 영향을 주지 않습니다.
- 멀티파트 업로드를 사용하면 언제든지 단일 대형 객체의 업로드를 일시 중지 및 복구할 수 있습니다. 멀티파트 업로드를 중단하지 않는 한 모든 미완료 객체는 언제든지 업로드를 재개할 수 있습니다.
- 멀티파트 업로드는 객체 볼륨을 알 수 없는 상황에서도 업로드할 수도 있습니다. 업로드를 시작한 다음 객체를 재결합하여 전체 볼륨을 가져올 수 있습니다.

업로드 시 이 멀티파트는 연속적인 번호로 매겨집니다. 단일 멀티파트로 업로드하거나 순서에 관계없이 업로드할 수 있습니다. COS는 최종으로 멀티파트를 번호 순서에 따라 해당 객체로 다시 결합해냅니다. 임의의 멀티파트의 업로드가 실패하면, 다른 멀티파트와 내용 무결성에 영향을 주지 않고 해당 멀티파트를 다시 업로드할 수 있습니다. 일반적으로 약한 네트워크 환경에서 20 MB를 초과하는 객체를 우선적으로 멀티파트 업로드될 수 있으며 높은 대역폭 환경에서 100 MB를 초과하는 객체를 멀티파트 업로드합니다.

## 사용 방법

### REST API 사용

REST API를 사용하여 직접 멀티파트 업로드 요청을 보낼 수 있으며 아래 API 문서를 참조할 수 있습니다.

- [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746)
- [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742)
- [Upload Part](https://cloud.tencent.com/document/product/436/7750)
- [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740)

### C++ SDK 사용

이 방법은 COS의 C ++ SDK에서 제공됩니다. [C ++ SDK API 문서의 멀티파트 업로드 조작 섹션](https://cloud.tencent.com/document/product/436/12302#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C)을 참조하십시오.

#### 절차 설명

1. 구성 파일 경로를 전달하여 CosConfig 및 CosAPI 객체를 초기화합니다.
2. InitMultiUpload()를 호출하여 멀티파트 업로드를 초기화하고 업로드 ID를 가져옵니다.
3. UploadPartData () 방법을 반복적으로 호출하여 멀티파트를 업로드합니다. 그중 UploadPartDataReq는 업로드할 버킷 이름, 객체 키 이름, 업로드 ID, 멀티파트 번호 및 파일 내용이 필요합니다.
4. CompleteMultiUpload() 방법을 실행하여 멀티파트 업로드를 완료합니다. 버킷 이름, 객체 키 이름, UploadID 및 모든 파트 정보가 필요합니다.

#### 예제 코드

아래 예제 코드는 객체를 어떻게 멀티파트 업로드하는지를 보여줍니다.

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";
std::string upload_id = "";
std::vector<std::string> etags;
std::vector<int64_t> part_nums;

// 1. InitMultiUpload를 호출하여 uploadId를 가져옵니다.
qcloud_cos::InitMultiUploadReq init_req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp init_resp;
qcloud_cos::CosResult init_result = cos.InitMultiUpload(init_req, init_resp);

if (init_result.IsSucc()) {
    upload_id = init_resp.GetUploadId();
} else {
    // do sth
}

// 2.1 첫 번째 멀티파트를 업로드합니다.
{
    std::fstream is("demo_5M.part1");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(1);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // 업로드가 완료되면 멀티파트 번호와 반환된 etag를 기록합니다.
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_nums.push_back(1);
    }
    is.close();
}

// 2.2 두 번째 멀티파트를 업로드합니다.
{
    std::fstream is("demo_5M.part2");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(2);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // 업로드가 완료되면 멀티파트 번호와 반환된 etag를 기록합니다.
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_nums.push_back(2);
    }
    is.close();
}

// 2.x 후속 멀티파트를 업로드합니다.
...

// 3. 멀티파트 업로드를 완료합니다.
qcloud_cos::CompleteMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp resp;
req.SetEtags(etags);
req.SetPartNumbers(part_nums);

qcloud_cos::CosResult result = cos.CompleteMultiUpload(req, &resp);

```

AbortMultiUpload() 방법을 실행하여 멀티파트 업로드 작업을 중단할 수 있습니다. 버킷 이름, 키 이름 및 UploadId가 필요합니다.
```cpp
qcloud_cos::AbortMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::AbortMultiUploadResp resp;
qcloud_cos::CosResult result = cos.AbortMultiUpload(req, &resp);
```

list_parts() 방법을 실행하여 멀티파트 업로드 작업을 나열할 수 있습니다. 버킷 이름, 키 이름 및 UploadId가 필요합니다.
``` cpp
qcloud_cos::ListPartsReq req(bucket_name, object_name, upload_id);
qcloud_cos::ListPartsResp resp;
qcloud_cos::CosResult result = cos.ListParts(req, &resp);
```

### Java SDK 사용

이 방법은 COS의 Java SDK에서 제공됩니다. [Java SDK API 문서 PUT object의 멀티파트 업로드섹션](https://cloud.tencent.com/document/product/436/12263#put-object.EF.BC.88.E4.B8.8A.E4.BC.A0-object.EF.BC.89)을 참조하십시오.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. initiateMultipartUpload를 사용하여 멀티파트 업로드를 초기화하여 새 uploadid를 가져오거나 호출한 listMultipartUploads를 가져오기 전에 미완료한 멀티파트 업로드하여 uploadid를 가져옵니다.
3. 업로드된 멀티파트는 listParts를 사용하여 가져올 수 있습니다. 업로드되지 않은 멀티파트는 uploadPart를 사용하여 멀티파트 데이터를 업로드하거나 copyPart를 사용하여 멀티파트를 다른 파일에서 현재 파일로 copy 할 수 있습니다. 이렇게 하면 중단 점에서 업로드 재개 기능이 구현됩니다. 업로드된 멀티파트에 대해 uploadPart 또는 copyPart가 다시 호출되면 업로드된 멀티파트 데이터를 덮어씁니다.
4. completeMultipartUpload를 사용하여 멀티파트 업로드를 완료하거나 abortMultipartUpload를 호출하여 멀티파트 업로드를 종료합니다.

#### 예제 코드

(1)`InitiateMultipartUploadRequest`는 멀티파트 업로드를 초기화하는 요청으로 멀티파트 업로드의 경로, 스토리지 클래스 등 정보를 포함하고 있습니다. initiateMultipartUpload를 호출하여 새로운 멀티파트 업로드 ID를 가져올 수 있습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";

String key = "aaa/bbb.txt";
InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);
// 스토리지 클래스를 설정합니다. 기본적으로 표준(Standard), 저빈도(standard_ia)입니다.
request.setStorageClass(StorageClass.Standard_IA);
try {
    InitiateMultipartUploadResult initResult = cosclient.initiateMultipartUpload(request);
    // uploadid 가져오기
    String uploadId =  initResult.getUploadId();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

(2)`UploadPartRequest`는 멀티파트 업로드 요청으로 업로드할 데이터와 멀티파트 번호가 포함됩니다. uploadPart를 호출하여 파트를 업로드하고 partEtag를 가져옵니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (initiateMultipartUpload 또는 ListMultipartUploads를 통해 가져옴)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

// 업로드할 데이터를 생성합니다. 이 경우 1M의 데이터를 초기화합니다.
byte data[] = new byte[1024 * 1024];
UploadPartRequest uploadPartRequest = new UploadPartRequest();
uploadPartRequest.setBucketName(bucketName);
uploadPartRequest.setKey(key);
uploadPartRequest.setUploadId(uploadId);
// 멀티파트 데이터 소스의 입력 스트림을 설정합니다.
uploadPartRequest.setInputStream(new ByteArrayInputStream(data));
// 멀티파트 길이를 설정합니다.
uploadPartRequest.setPartSize(data.length); // 데이터 길이를 설정합니다.
uploadPartRequest.setPartNumber(10);     // 업로드 할 part 번호가 10이라고 가정합니다.

try {
    UploadPartResult uploadPartResult = cosclient.uploadPart(uploadPartRequest);
    PartETag partETag = uploadPartResult.getPartETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

(3)`CompleteMultipartUploadRequest`는 멀티파트 업로드를 완료하는 데 사용됩니다. 업로드하기 전에 전체 멀티파트의 partEtag가 필요합니다. completeMultipartUpload를 호출하여 멀티파트 업로드를 완료합니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (initiateMultipartUpload 또는 ListMultipartUploads를 통해 가져옴)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

// 여기서 빈 대기열을 초기화하여 업로드된 멀티파트 정보를 저장하는 데 사용합니다. 이 코드는 직접 실행할 수 없는데 이전의 uploadpart 또는 list parts 결과에서 가져와서 partEtags 대기열에 추가할 수 있습니다.
List<PartETag> partETags = new LinkedList<>();

// 멀티파트 업로드가 완료되면 complete를 호출하여 멀티파트 업로드를 완료합니다.
CompleteMultipartUploadRequest completeMultipartUploadRequest =
        new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
try {
    CompleteMultipartUploadResult completeResult =
            cosclient.completeMultipartUpload(completeMultipartUploadRequest);
    String etag = completeResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

(4)`AbortMultipartUploadRequest`는 멀티파트 업로드 중단 요청이며 미완료한 멀티파트 업로드를 중단하는 데 사용됩니다. 이미 업로드된 멀티파트를 중단하고 폐기하는 것을 표시합니다. abortMultipartUpload를 호출하여 멀티파트 업로드 요청을 중단할 수 있습니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (initiateMultipartUpload 또는 ListMultipartUploads를 통해 가져옴)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
try {
    cosclient.abortMultipartUpload(abortMultipartUploadRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

(5)`ListPartsRequest`는 업로드된 멀티파트의 요청을 나열하는 데 사용되며 중단 점에서 업로드를 재개하는 데 사용될 수 있습니다. 업로드된 멀티파트는 listParts를 호출하여 가져올 수 있습니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);

// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (initiateMultipartUpload 또는 ListMultipartUploads를 통해 가져옴)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

List<PartETag> partETags = new LinkedList<>();      // 업로드된 모든 멀티파트의 정보를 저장하는 데 사용됩니다.
PartListing partListing = null;
ListPartsRequest listPartsRequest = new ListPartsRequest(bucketName, key, uploadId);
do {
    try {
        partListing = cosclient.listParts(listPartsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
    } catch (CosClientException e) {
        e.printStackTrace();
    }
    for (PartSummary partSummary : partListing.getParts()) {
        partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
    }
    listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());

cosclient.shutdown();
```

(6)`CopyPartResult`는 멀티파트 copy 요청이며 멀티파트 데이터는 다른 파일의 일부에서 생성된 것을 나타냅니다. 복사할 소스 파일의 경로, bucket 정보 및 바이트 범위를 통해 copyPart를 호출하여 멀티파트 copy를 구현할 수 있습니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
// uploadid (initiateMultipartUpload 또는 ListMultipartUploads를 통해 가져옴)
String uploadId = "1512380198aecfed004aeaaca195d08232f718f7b52a91b8f6e9d36c7dfead2b3d1c917a6f";

CopyPartRequest copyPartRequest = new CopyPartRequest();
// 복사할 소스 파일이 있는 region
copyPartRequest.setSourceBucketRegion(new Region("ap-beijing-1"));
// 복사할 소스 파일의 bucket 이름
copyPartRequest.setSourceBucketName(bucketName);
// 복사할 소스 파일의 경로
copyPartRequest.setSourceKey("aaa/ccc.txt");
// 복사할 소스 파일의 데이터 범위 지정 (content-range 유사)
copyPartRequest.setFirstByte(0L);
copyPartRequest.setLastByte(1048575L);
// 대상 bucket 이름
copyPartRequest.setDestinationBucketName(bucketName);
// 대상 경로 이름
copyPartRequest.setDestinationKey(key);

// uploadid
copyPartRequest.setUploadId(uploadId);
try {
    CopyPartResult copyPartResult = cosclient.copyPart(copyPartRequest);
    PartETag partETag = copyPartResult.getPartETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```
### JavaScript SDK 사용

이 방법은 COS의 JavaScript SDK에서 제공됩니다. [JavaScript SDK API 문서 멀티파트 업로드 조작 섹션](https://cloud.tencent.com/document/product/436/12260#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C)을 참조하십시오.

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

아래 예제 코드는 객체를 어떻게 멀티파트 업로드하는지를 보여줍니다.

```html
<script src="dist/cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'test-1250000000'; // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';    // 사용자의 지역으로 대체합니다.

// 인스턴스 초기화
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 비동기 서명 획득
        var url = 'auth.php?method=' + options.Method.toLowerCase() + '&pathname=' + encodeURIComponent('/' + (options.Key || ''));
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            callback(e.target.responseText);
        };
        xhr.send();
    }
});

// 수신자 파일 선택
document.getElementById('file-selector').onchange = function () {

    var file = this.files[0];
    if (!file) return;

    cos.sliceUploadFile({
        Bucket: Bucket,
        Region: Region,
        Key: file.name,
        Body: file,
    }, function (err, data) {
        console.log(err, data);
    });

};
</script>
```
### Node.js SDK 사용

이 방법은 COS의 Node.js SDK에 제공됩니다. [Node.js SDK API 문서의 멀티파트 업로드 조작 섹션](https://cloud.tencent.com/document/product/436/12264#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E6.93.8D.E4.BD.9C)을 참조하십시오.

#### 절차 설명

1. npm 의존 패키지를 설치합니다.
```shell
npm i cos-nodejs-sdk-v5
```

2. 현재 디렉터리에 업로드될 1.jpg 파일을 넣습니다.

3. 테스트 파일 test.js를 생성하고, 명령행에서 `node test.js`를 실행합니다.

#### 예제 코드

아래 예제 코드는 객체를 어떻게 멀티파트 업로드하는지를 보여줍니다.

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretKey로 대체합니다.
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.sliceUploadFile({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg',
    FilePath: '1.jpg'
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDK 사용

이 방법은 COS의 PHP SDK에서 제공됩니다. [PHP SDK API 문서의 멀티파트 파일 업로드 섹션](https://cloud.tencent.com/document/product/436/12267#.E5.88.86.E5.9D.97.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0)을 참조하십시오.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. upload 방법을 실행하여 데이터 스트림을 업로드합니다. 버킷 이름과 객체 키 이름이 필요합니다.
3. fopen을 통해 파일 스트림을 업로드합니다.

#### 예제 코드

다음 예제 코드는 객체를 멀티파트 업로드하는 절차를 보여줍니다.

* 메모리 업로드:
```php
try {
    $result = $cosClient->upload(
                 $bucket='testbucket-125000000',
                 $key = '111.txt',
                 $body = 'HELLO';
    print_r($result);
    } catch (\Exception $e) {
    echo "$e\n";
}
```
* 파일 스트림 업로드:
```php
try {
    $result = $cosClient->upload(
                 $bucket='testbucket-125000000',
                 $key = '111.txt',
                 $body = fopen($pathToFile, 'r+'));
    print_r($result);
    } catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDK 사용

COS의 Python SDK에서 이 방법을 제공하며 Python SDK API 문서의 다음 부분을 참조할 수 있습니다.

- [멀티파트 업로드 생성](https://cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [멀티파트 업로드](https://cloud.tencent.com/document/product/436/12270#.E4.B8.8A.E4.BC.A0.E5.88.86.E5.9D.97)
- [멀티파트 업로드 완료](https://cloud.tencent.com/document/product/436/12270#.E5.AE.8C.E6.88.90.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [멀티파트 업로드 포기](https://cloud.tencent.com/document/product/436/12270#.E6.94.BE.E5.BC.83.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0)
- [멀티파트 업로드 나열](https://cloud.tencent.com/document/product/436/12270#.E5.88.97.E5.87.BA.E4.B8.8A.E4.BC.A0.E5.88.86.E5.9D.97)

#### 절차 설명

1. CosConfig 클래스로 구성하고 클라이언트 CosS3Client를 초기화합니다.
2. create_multipart_upload() 방법을 실행하여 멀티파트 업로드를 초기화합니다. 버킷 이름과 객체 키 이름이 필요합니다.
3. upload_part () 방법을 반복적으로 실행하여 멀티파트를 업로드합니다. 버킷 이름, 객체 키 이름, UploadId 및 단일 멀티파트 내용이 필요합니다.
4. complete_multipart_upload() 방법을 실행하여 멀티파트 업로드를 완료합니다. 버킷 이름, 객체 키 이름, UploadID 및 모든 파트 정보가 필요합니다.

#### 예제 코드

아래 예제 코드는 객체를 어떻게 멀티파트 업로드하는지를 보여줍니다.

```python
secret_id = 'xxxxxxxx'      # 사용자의 SecretId로 대체합니다.
secret_key = 'xxxxxxx'      # 사용자의 secretKey로 대체합니다.
region = 'ap-beijing-1'     # 사용자의 지역으로 대체합니다.
token = ''                  # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'

# 1. 멀티파트 업로드 초기화
response = client.create_multipart_upload(
    Bucket=bucket,
    Key=file_name       
)
uploadid = response['UploadId']

# 2.단일 멀티파트 업로드
lst = list()
part_number = 1
with open('test.txt', 'rb') as fp:
    while True:
        data = fp.read(1024*1024)
        if data == "":
            break
        response = client.upload_part(
            Bucket=bucket,
            Key=file_name,
            UploadId=uploadid,
            PartNumber=part_number,
            Body=data
        )
        lst.append({'PartNumber': part_number, 'ETag': response['ETag']})
        part_number += 1

# 3.멀티파트 업로드 완료.
response = client.complete_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid,
    MultipartUpload={'Part': lst}
)
```

abort_multipart_upload () 방법을 실행하여 멀티파트 업로드를 중단할 수 있습니다. 버킷 이름, 객체 키 이름 및 UploadId가 필요합니다.
```python
response = client.abort_multipart_upload(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid
)
```

list_parts () 방법을 실행하여 멀티파트 업로드를 나열할 수 있습니다. 버킷 이름, 객체 키 이름 및 UploadId가 필요합니다.
```python
response = client.list_parts(
    Bucket=bucket,
    Key=file_name,
    UploadId=uploadid
)
```

list_multipart_uploads () 방법을 실행하여 버킷에 미완료된 멀티파트 업로드를 모두 나열할 수 있습니다. 버킷 이름은 필요합니다.
```python
response = client.list_multipart_uploads(
    Bucket=bucket
)
```
####
