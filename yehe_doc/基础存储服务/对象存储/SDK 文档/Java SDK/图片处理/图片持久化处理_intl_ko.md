## 소개

다음 예시는 이미지 업로드 시 자동 이미지 처리 방법입니다.

이미지 업로드 완료 후 COS는 원본과 처리한 이미지를 저장합니다. 이후에 사용자는 일반 다운로드 요청을 통해 처리했던 결과를 불러올 수 있습니다.

## 업로드 시 이미지 영구 처리

#### 예시 코드

[//]: # ".cssg-snippet-upload-with-pic-operation"
```java
  // bucket 이름에는 반드시 appid가 포함됨
// api는 https://cloud.tencent.com/document/product/436/54050 참조
String bucketName = "examplebucket-1250000000";

String key = "test.jpg";
File localFile = new File("E://test.jpg");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PicOperations picOperations = new PicOperations();
picOperations.setIsPicInfo(1);
// 이미지 처리 규칙 추가
List<PicOperations.Rule> ruleList = new LinkedList<>();
PicOperations.Rule rule1 = new PicOperations.Rule();
rule1.setBucket(bucketName);
rule1.setFileId("test-1.jpg");
rule1.setRule("imageMogr2/rotate/90");
ruleList.add(rule1);
PicOperations.Rule rule2 = new PicOperations.Rule();
rule2.setBucket(bucketName);
rule2.setFileId("test-2.jpg");
rule2.setRule("imageMogr2/rotate/180");
ruleList.add(rule2);
picOperations.setRules(ruleList);
putObjectRequest.setPicOperations(picOperations);
try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    CIUploadResult ciUploadResult = putObjectResult.getCiUploadResult();
    System.out.println(putObjectResult.getRequestId());
    System.out.println(ciUploadResult.getOriginalInfo().getEtag());
    for(CIObject ciObject:ciUploadResult.getProcessResults().getObjectList()) {
        System.out.println(ciObject.getLocation());
        System.out.println(ciObject.getEtag());
    }
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```

#### 매개변수 설명

PicOperations 유형은 이미지 작업을 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름  | 설명                                                         | 유형 |
| --------- | ------------------------------------------------------------ | ---- |
| isPicInfo | 원본 이미지 정보 반환 여부. 반환하지 않는 경우: 0 반환하는 경우: 1 기본값: 0 | int |
| rules     | 처리 규칙. 규칙과 결과가 일대일로 대응(현재는 규칙 5개까지 지원). 비워놓을 경우 이미지 처리를 진행하지 않음 | List |

#### 반환 매개변수 설명

CIUploadResult 유형은 이미지 처리 결과 정보 반환에 사용됩니다. 주요 멤버는 다음과 같습니다.

| 멤버 이름       | 설명         | 유형           |
| -------------- | ------------ | -------------- |
| originalInfo   | 원본 이미지 정보     | OriginalInfo   |
| processResults | 이미지 처리 결과 | ProcessResults |

  OriginalInfo 유형은 원본 이미지 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름  | 설명                                                       | 유형      |
| --------- | ---------------------------------------------------------- | --------- |
| key       | 원본 이미지 파일 이름                                                 | String    |
| location  | 이미지 경로                                                   | String    |
| imageInfo | 원본 이미지 정보                                               | ImageInfo |
| etag      | 원본 이미지 ETag 정보(처리한 이미지가 원본 이미지를 덮어쓰는 경우, 처리한 이미지의 ETag 정보) | String    |

ImageInfo 유형은 원본 이미지 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름    | 설명         | 유형    |
| ----------- | ------------ | ------- |
| format      | 포맷         | String  |
| width       | 이미지 폭     | Integer |
| height      | 이미지 높이     | Integer |
| quality     | 이미지 품질     | Integer |
| ave         | 이미지 메인 컬러   | String  |
| orientation | 이미지 회전 각도 | Integer |

ProcessResults 유형은 이미지 처리 결과를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름   | 설명               | 유형 |
| ---------- | ------------------ | ---- |
| objectList | 모든 이미지 처리 결과 | List |

CIObject 유형은 이미지 처리 결과를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름       | 설명                       | 유형    |
| -------------- | -------------------------- | ------- |
| key            | 파일 이름                     | String  |
| location       | 이미지 경로                   | String  |
| format         | 이미지 포맷                   | String  |
| width          | 이미지 폭                   | Integer |
| height         | 이미지 높이                   | Integer |
| size           | 이미지 크기                   | Integer |
| quality        | 이미지 품질                   | Integer |
| etag | 처리한 이미지의 ETag 정보       | String |



## 클라우드 데이터의 이미지 처리

다음 예시는 COS에 저장된 이미지에 알맞은 처리 작업을 하고 결과를 COS에 저장하는 방법입니다.

#### 예시 코드

[//]: # ".cssg-snippet-process-with-pic-operation"
```java
String bucketName = "examplebucket-1250000000";
String key = "test.jpg";
ImageProcessRequest imageReq = new ImageProcessRequest(bucketName, key);

PicOperations picOperations = new PicOperations();
picOperations.setIsPicInfo(1);
List<PicOperations.Rule> ruleList = new LinkedList<>();
PicOperations.Rule rule1 = new PicOperations.Rule();
rule1.setBucket(bucketName);
rule1.setFileId("test-1.jpg");
rule1.setRule("imageMogr2/rotate/90");
ruleList.add(rule1);
PicOperations.Rule rule2 = new PicOperations.Rule();
rule2.setBucket(bucketName);
rule2.setFileId("test-2.jpg");
rule2.setRule("imageMogr2/rotate/180");
ruleList.add(rule2);
picOperations.setRules(ruleList);

imageReq.setPicOperations(picOperations);

CIUploadResult result = cosClient.processImage(imageReq);
result.getProcessResults();
result.getOriginalInfo();

try {
    CIUploadResult ciUploadResult = cosClient.processImage(imageReq);
    System.out.println(ciUploadResult.getOriginalInfo().getEtag());
    for(CIObject ciObject:ciUploadResult.getProcessResults().getObjectList()) {
        System.out.println(ciObject.getLocation());
        System.out.println(ciObject.getEtag());
    }
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
