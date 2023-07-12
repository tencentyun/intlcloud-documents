## 소개

본 문서는 객체 삭제 관련 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 객체 삭제   | 버킷에서 객체 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289)	 | 다수의 객체 삭제	| 버킷에서 객체 일괄 삭제  |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 단일 객체 삭제

#### 기능 설명

지정 객체를 삭제합니다(DELETE Object).

#### 예시 코드

[//]: # (.cssg-snippet-delete-object)
```java
String bucket = "examplebucket-1250000000"; //버킷 이름, 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자. 즉, 객체 키.

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket,
        cosPath);
cosXmlService.deleteObjectAsync(deleteObjectRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        DeleteObjectResult deleteObjectResult = (DeleteObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/DeleteObject.java)를 참고하십시오.

## 다수의 객체 삭제

#### 기능 설명

다수의 객체를 일괄 삭제합니다(Delete Multi Objects).

#### 예시 코드

[//]: # (.cssg-snippet-delete-multi-object)
```java
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
List<String> objectList = new ArrayList<String>();
objectList.add("exampleobject1"); //버킷 내 객체 위치 식별자. 즉, 객체 키
objectList.add("exampleobject2"); //버킷 내 객체 위치 식별자. 즉, 객체 키

DeleteMultiObjectRequest deleteMultiObjectRequest =
        new DeleteMultiObjectRequest(bucket, objectList);
// Quiet 모드는 오류가 보고된 Object 정보만 반환합니다. 해당 모드가 아닌 경우 모든 Object의 삭제 결과를 반환합니다.
deleteMultiObjectRequest.setQuiet(true);
cosXmlService.deleteMultiObjectAsync(deleteMultiObjectRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        DeleteMultiObjectResult deleteMultiObjectResult =
                (DeleteMultiObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/DeleteObject.java)를 참고하십시오.

## 디렉터리 삭제

#### 기능 설명

COS의 폴더는 객체 이름이 '/'로 구분되고 파일 시스템과 같은 경로를 생성하여 시뮬레이션됩니다. 따라서 폴더를 삭제하는 작업은 COS에서 동일한 접두사를 가진 객체를 일괄 삭제하는 것과 같습니다. 예를 들어, 'prefix/' 폴더는 접두사가 'prefix/'인 모든 객체를 대표하며 'prefix/' 삭제는 접두사가 'prefix/'인 모든 객체를 삭제한다는 의미입니다.

현재 COS Android SDK는 이러한 작업을 지원하는 인터페이스를 제공하지 않습니다. 그러나 기본 작업을 조합하여 이와 동일한 효과를 볼 수 있습니다.

#### 예시 코드

[//]: # (.cssg-snippet-delete-prefix)
```java
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String prefix = "folder1/"; //접두사 지정

GetBucketRequest getBucketRequest = new GetBucketRequest(bucket);
getBucketRequest.setPrefix(prefix);

// prefix는 삭제할 폴더를 의미
getBucketRequest.setPrefix(prefix);
// 순회할 객체의 최대 수량 설정. listobject 1회당 최대 1000개까지 지원
getBucketRequest.setMaxKeys(1000);
GetBucketResult getBucketResult = null;

do {
    try {
        getBucketResult = cosXmlService.getBucket(getBucketRequest);
        List<ListBucket.Contents> contents = getBucketResult.listBucket.contentsList;
        DeleteMultiObjectRequest deleteMultiObjectRequest = new DeleteMultiObjectRequest(bucket);
        for (ListBucket.Contents content : contents) {
            deleteMultiObjectRequest.setObjectList(content.key);
        }
        cosXmlService.deleteMultiObject(deleteMultiObjectRequest);
        getBucketRequest.setMarker(getBucketResult.listBucket.nextMarker);
    } catch (CosXmlClientException e) {
        e.printStackTrace();
        return;
    } catch (CosXmlServiceException e) {
        e.printStackTrace();
        return;
    }
} while (getBucketResult.listBucket.isTruncated);
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/DeleteObject.java)를 참고하십시오.

