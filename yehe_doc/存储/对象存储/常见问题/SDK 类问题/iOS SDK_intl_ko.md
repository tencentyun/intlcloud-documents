### SDK를 수동 통합한 후 QCloudCOSXMLEndPoint 인스턴스에 대해 regionName을 설정한 후 “[__NSCFConstantString matchesRegularExpression:]: unrecognized selector sent to instance xxx” 오류가 발생하면 어떻게 해야 합니까?

**원인**: matchesRegularExpression은 NSString 카테고리의 메소드입니다. Objective-C는 각 메소드에 대한 링커 기호를 정의하지 않고 각 클래스에 대해 정의합니다. SDK는 정적 라이브러리입니다. 정적 라이브러리의 기존 클래스에 대해 카테고리가 정의된 경우 시스템은 클래스가 이미 존재한다고 가정하고 클래스와 카테고리의 코드를 통합하지 않습니다. 결과적으로 카테고리의 메소드는 실행 코드에서 누락됩니다.

**솔루션**:
1. target > Build Settings > All > Other Linker Flags를 클릭하고 `-Objc`와 `-all_load` 매개변수를 추가합니다.
2. `-ObjC`는 정적 라이브러리의 클래스 및 카테고리를 실행 파일로 로딩합니다. 카테고리만 있고 라이브러리에 클래스가 없는 경우 `-ObjC`는 적용되지 않습니다. 이 경우 모든 객체 파일을 실행 파일에 로딩하려면 `-all_load`가 필요합니다.
3. 문제가 지속되면 bitcode를 비활성화합니다.

### SDK를 통합하고 요청을 보낸 후 “기본 OCR 구성이 설정되지 않았습니다. 구성된 후 이 메소드를 호출하십시오. 또는 OCR 구성에서 키가 'xxx'로 설정되지 않았습니다. 구성된 후 이 메소드를 호출하십시오.” 오류가 발생하면 어떻게 해야 하나요?

**원인**: 모든 SDK 요청은 QCloudCOSXMLService 및 QCloudCOSTransferMangerService에 의존합니다(고급 업로드 API는 이 인스턴스에 의존함). 요청이 전송되기 전에 해당 service가 등록되지 않은 경우 이 오류가 발생합니다.

**솔루션**: 다음 코드를 사용하여 요청에 필요한 service 인스턴스를 등록하십시오. 요청을 보내기 전에 인스턴스가 존재하는지 확인하십시오.

```iOS
    QCloudServiceConfiguration *configuration = [QCloudServiceConfiguration new];
    configuration.appID = "AppId";
    configuration.signatureProvider = self;
    QCloudCOSXMLEndPoint *endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    endpoint.regionName = @"region";
    endpoint.useHTTPS = YES;
    configuration.endpoint = endpoint;

    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
```

### SDK 통합 후 “기본 COSXMLService가 이미 존재합니다. 새 구성을 사용하려면 registerCOSXMLWithConfiguration:withKey:를 사용하여 다시 등록하십시오.” 오류가 발생하면 어떻게 하나요?

**원인**: SDK에서 다른 COSXMLService 인스턴스는 다른 구성에 해당합니다(구성에 대해서는 관련 속성 참고). 예를 들어 regionName을 ap-guangzhou와 ap-beijing으로 설정하면 두 가지 service를 등록해야 하는 두 가지 구성을 나타냅니다. 이미 ap-guangzhou를 이용하여 service를 등록한 후 region을 ap-guangzhou로 설정하여 다시 등록하면 이 오류가 발생합니다.

**솔루션**:
1. 기본 service는 `registerDefaultCOSXMLWithConfiguration：`을 사용하며 key를 지정할 필요가 없습니다.
2. 다음 코드를 사용하여 새 service를 등록합니다.
```iOS
//등록할 key가 있는지 판단합니다
    if(![QCloudCOSXMLService hasServiceForKey:@"등록할 key"]){
    //키가 없으면 새로운 service를 등록합니다
        [QCloudCOSXMLService registerCOSXMLWithConfiguration:configuration withKey:@"등록할 key"]
    }
```

### SDK 실행 후 “- (void)signatureWithFields:(QCloudSignatureFields *)fileds request:urlRequest:compelete:” 프록시가 호출되지 않으면 어떻게 하나요?

**원인**: 이 프록시 메소드는 키/서명을 얻습니다. 키 유효성을 최대한 활용하기 위해(서명을 더 일찍 호출하면 서명이 더 빨리 만료됨) SDK는 요청이 `task resume`로 전송되기 전에만 키를 호출합니다.

**솔루션**:
1. 프록시 메소드가 속한 클래스가 요청을 보내기 전에 폐기되지 않았는지 확인하십시오. 싱글톤 클래스에서 프록시 메소드를 구현하는 것이 좋습니다.
2. `QCloudServiceConfiguration` 인스턴스가 생성된 후 `signatureProvider` 구성 여부를 확인합니다. 예시: `configuration.signatureProvider = self로 구성(여기서 self는 프록시 메소드가 속한 클래스임)`
3. 위의 두 가지 사항을 확인한 후 요청이 전송되는지 확인하십시오.

### SDK가 키를 캐시하거나 재사용할 수 있습니까? 키가 만료되면 어떻게 새 키를 요청할 수 있습니까?

SDK는 키를 캐시하거나 재사용하기 위해 QCloudCredentailFenceQueue를 제공합니다. 자세한 내용은 [시작하기](https://intl.cloud.tencent.com/document/product/436/11280)를 참고하십시오.

### SDK 고급 API “QCloudCOSXMLUploadObjectRequest”에서 “이 유형의 body는 지원되지 않습니다. 지원되는 유형은 NSData, QCloudFileOffsetBody, NSURL입니다.” 오류가 발생했을 때 어떻게 해야 하나요?

현재 SDK는 다음 세 가지 유형의 body를 지원합니다.
1. NSURL: 파일 로컬 경로입니다. URL은 `[NSURL fileURLWithPath:@"로컬 내 파일 경로"]`를 통해 초기화됩니다.
2. NSData: 이진법 데이터
3. QCloudFileOffsetBody: 멀티파트 body. SDK 고급 API에서 내부적으로 사용하기 위한 body 유형이므로 대부분의 경우 이 유형을 무시할 수 있습니다.

### SDK 고급 API “QCloudCOSXMLUploadObjectRequest”를 사용하여 시스템 사진 라이브러리에서 비디오 또는 파일을 업로드했지만 체크포인트 재시작에 실패하고 “The specified Content-Length is zero” 오류가 발생하면 어떻게 해야 합니까?

SDK는 샌드박스의 파일에 대해서만 체크포인트 다시 시작을 지원합니다. 체크포인트 재시작 기능을 사용하려면 먼저 파일을 샌드박스로 이동하십시오.

### SDK 통합 후 API로 업로드한 파일의 크기가 로컬 파일의 크기와 다른 경우 어떻게 해야 하나요?

body를 설정한 후 로컬 파일이 수정되지 않았는지 확인하십시오. 예를 들어, 파일이 아직 압축 중이거나 파일 쓰기가 아직 완료되지 않은 상태에서 업로드 API가 호출되면 SDK는 업로드 시점의 크기에 따라 파일을 업로드(멀티파트 업로드 사용)하므로 cos 파일과 로컬 파일 간에 파일 크기 불일치가 발생합니다.

### SDK를 통합하여 업로드 API를 호출했는데 "body 의 URL이 로컬 URL이 아닙니다!" 오류가 발생하면 어떻게 하나요?

**솔루션:**
URL이 file://로 시작하는지 확인하십시오. 다음 두 가지 방법 중 하나로 초기화할 수 있습니다.
1. `[NSURL URLWithString:@"file:////var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]`
2. `[NSURL fileURLWithPath:@"/var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]`


### SDK를 통합하여 업로드 API를 호출했는데 정상적으로 업로드된 파일의 크기가 0인 경우 어떻게 해야 하나요?

**솔루션:**
1. 시스템 사진 라이브러리의 경로를 사용하는 경우 파일에 대한 읽기 권한이 있는지 확인하십시오. 예를 들어 `file:///var/mobile/Media/DCIM/101APPLE/` 경로는 직접 액세스할 수 없습니다. 이 경로의 사진은 Photos 프레임워크의 request 메소드를 통해서만 얻을 수 있습니다.
2. App이 iOS11과 호환되도록 하려면, `[[PHImageManager defaultManager] requestPlayerItemForVideo:asset options:option resultHandler:^(AVPlayerItem *playerItem, NSDictionary *info) {
    //시간에 맞춰 파일을 샌드박스로 이동하거나 playerItem을 저장합니다.
    }]`; 획득한 playerItem을 저장하거나 콜백하는 동안 원하는 파일을 App 샌드박스로 이동하는 메소드를 사용할 수 있습니다. 이 오류의 원인은 iOS11의 경우 playerItem이 해제되면 playerItem에 지정된 파일에 대한 읽기 권한이 만료되어 업로드된 파일의 크기가 0이 되기 때문입니다.
3. 업로드한 파일이 App 샌드박스에 있다면 tmp 디렉터리에 파일이 저장되어 있는지 확인합니다(예시: ` /var/mobile/Containers/Data/Application/0BFBB3FE-0FD0-46CB-ADDE-DDE08F6D62C3/tmp/`). tmp의 파일은 시스템에서 언제든지 삭제됩니다. 업로드 중에 파일이 삭제된 경우 파일을 안전한 디렉터리로 옮길 수 있습니다. 샌드박스에 대한 자세한 내용은 [File System Basics](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html)를 참고하십시오.

### 업로드에 SDK 고급 API를 사용하는데 “MD5 체크섬이 로컬 파일과 일치하지 않습니다. 업로드 시 파일 수정 여부를 확인하십시오. 멀티파트 업로드 중에 업로드된 각 파트의 MD5 체크섬이 로컬 파일과 비교하여 확인됩니다. 일치하지 않으면 오류가 발생합니다.” 오류가 보고되면 어떻게 해야 하나요?

**원인:** SDK를 사용하여 1MB보다 큰 파일을 업로드하면 파일이 여러 1MB 부분으로 분할되고 다중 부분 업로드를 사용하여 업로드됩니다. 모든 부분이 업로드된 후 백엔드에서 반환된 etag의 값을 로컬 부분의 값과 비교합니다. 불일치가 있으면 이 오류가 발생합니다.

**솔루션:** 파일을 업로드하는 과정에서 수정된 부분이 있는지 확인해주십시오.


### CDN 가속 엔드포인트로 SDK에 액세스할 수 있나요?

예. 자세한 지침은 프로그래밍 언어에 대한 SDK 설명서를 참고하십시오.

### SDK에서 요청 제한 시간을 어떻게 설정할 수 있습니까?

**솔루션:** SDK 5.7.0 이상 버전은 다음과 같이 요청 제한 시간 사용자 정의를 지원합니다.
1. `QCloudServiceConfiguration *config = [QCloudServiceConfiguration new]`를 초기화합니다.
2. config의 `timeoutInterval` 속성을 설정합니다. 예시: `config의.timeoutInterval = 30;`


### iOS SDK에 crash가 발생하였습니다. 처리 방법은 무엇입니까?

최신 버전을 사용하고 있는지 확인하십시오. 그렇지 않은 경우 최신 SDK 버전으로 업데이트하는 것이 좋습니다. 최신 iOS SDK는 [qcloud-sdk-ios](https://github.com/tencentyun/qcloud-sdk-ios)를 참고하십시오.

### “Undefined symbols for architecture arm64: "_ne10 init dsp", referenced from:” 오류가 보고되면 어떻게 해야 하나요?

[컴파일 오류: Undefined symbols for architecture arm64](https://github.com/LiteAVSDK/Player_iOS/issues/277)를 참고하십시오.
