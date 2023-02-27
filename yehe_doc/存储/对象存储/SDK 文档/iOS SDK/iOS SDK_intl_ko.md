### SDK를 수동 통합한 후 QCloudCOSXMLEndPoint 인스턴스를 설정한 regionName에 `[__NSCFConstantString matchesRegularExpression:]: unrecognized selector sent to instance xxx` 오류가 발생할 경우 어떻게 하나요?

원인: matchesRegularExpression는 NSString 카테고리에서 제공하는 방식입니다. Objective-C 링커는 모든 방식이 아닌 클래스에 대해서만 부호표를 생성합니다. sdk는 정적 라이브러리에 해당하며 정적 라이브러리에 존재하는 클래스 카테고리가 정의된 경우 시스템은 클래스가 이미 존재하는 것으로 간주하여 클래스와 클래스 카테고리의 코드 통합을 진행하지 않으며 결국에는 실행 가능 코드에서 카테고리 분류 방식 코드가 누락될 수 있습니다.

해결 방법:
1. target->Build Settings->All->Other Linker Flags에 -Objc와 -all_load 매개변수 2개를 추가합니다.
2. -ObjC는 정적 라이브러리 클래스와 카테고리를 마지막 실행 가능 파일에 로딩하지만, 라이브러리에 카테고리만 있고 클래스가 없는 경우, 유효하지 않은 매개변수가 되므로 -all_load가 필요합니다. 해당 매개변수는 찾아낸 모든 타깃 파일을 실행 가능 파일에 로딩합니다.

### SDK 통합 요청 전송 후 `기본 OCR 구성이 설정되지 않았습니다. 설정한 후 이 방식으로 다시 호출하십시오. 또는 OCR 서비스 설정에서 키가 'xxx'로 설정되지 않았습니다. 설정 후 이 방식으로 다시 호출하십시오.` 오류가 발생하면 어떻게 해야 하나요?

원인: sdk의 모든 요청은 QCloudCOSXMLService와 QCloudCOSTransferMangerService(업로드된 고급 인터페이스는 이 인스턴스에 종속)에 종속되며 요청하기 전 해당 service에 가입되어 있지 않으면 위와 같은 오류를 보냅니다.

해결 방법: 아래 코드로 필요한 service 인스턴스를 요청합니다. 요청을 보내기 전 해당 인스턴스가 있는지 확인합니다.

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


### SDK 통합 후 `기본 COSXMLService가 이미 존재합니다. 새로운 설정이 있으면registerCOSXMLWithConfiguration:withKey:를 통해 다시 등록하십시오.` 오류가 발생하면 어떻게 하나요?

원인: SDK에서는 각각의 COSXMLService 인스턴스가 각각 다른 설정에 대응하기 때문입니다. 설정 정보는 관련 속성을 참고하십시오. 예를 들어 regionName은 ap-guangzhou와 ap-beijing에 대응하는 설정이 다르므로 각각 다른 service에 등록해야 합니다. 만약 ap-guangzhou로 하나의 service에 가입 후 region을 ap-guangzhou로 바꾸어 재등록하면 위와 같은 오류가 발생할 수 있습니다.

해결 방법:
1. 기본 service는 `registerDefaultCOSXMLWithConfiguration：`을 이용하면 key를 지정할 필요가 없습니다.
2. 다음 코드로 하나의 새 service를 등록합니다.
```iOS
//등록할 key가 있는지 확인
    if(![QCloudCOSXMLService hasServiceForKey:@"등록할 key"]){
    //없으면 새 service에 등록
        [QCloudCOSXMLService registerCOSXMLWithConfiguration:configuration withKey:@"등록할key"]
    }
```

### SDK 통합 후 실행했을 때 `- (void)signatureWithFields:(QCloudSignatureFields *)fileds request:urlRequest:compelete:` 프록시가 호출되지 않으면 어떻게 하나요?

원인: 프록시는 키/서명을 얻는 방식입니다. 키의 유효성을 최대한 보장하기 위해(너무 이르게 서명 호출 시 쉽게 만료됨) SDK에서 요청 전송 전, 즉 `[task resume]` 전에 서명을 호출할 수 있습니다.

해결 방법:
1. 프록시 방식이 속한 클래스가 요청 전송 전에 폐기되지 않았는지 확인합니다. 프록시 방식은 단일 항목의 클래스에서 구현하는 것을 권장합니다.
2. `QCloudServiceConfiguration` 인스턴스 생성 후 `signatureProvider` 설정 여부를 확인합니다. 예시: `configuration.signatureProvider = self(self는 프록시 방식에 속한 클래스를 뜻함)`
3. 위 방법으로 문제가 해결되지 않으면 요청이 전송되었는지 확인하십시오.

### SDK에서 키를 캐시하여 재사용하거나 키가 만료된 후 새로운 키를 다시 요청할 수 있나요? 어떻게 해야 하나요?

sdk는 QCloudCredentailFenceQueue로 키의 캐시와 재사용을 제공합니다. 자세한 사용 방법은 [시작하기](https://intl.cloud.tencent.com/document/product/436/11280) 문서를 참고하십시오.

### SDK의 고급 인터페이스 `QCloudCOSXMLUploadObjectRequest`에서 `다음 유형의 body 설정을 지원하지 않습니다. 지원 유형은 NSData, QCloudFileOffsetBody, NSURL입니다.` 오류가 발생했을 때 어떻게 해야 하나요?

현재 sdk는 아래 세 가지 body 설정만 지원합니다.
1. NSURL: 파일 로컬 경로입니다. [NSURL fileURLWithPath:@"로컬 내 파일 경로"]로 URL을 초기화합니다.
2. NSData: 이진법 데이터
3. QCloudFileOffsetBody: 블록 body이자 SDK의 고급 인터페이스 내에서 사용하는 body 유형으로 개발자는 일반적으로 무시해도 됩니다.


### SDK의 고급 인터페이스 `QCloudCOSXMLUploadObjectRequest`로 시스템 포토 라이브러리에 있는 비디오나 파일을 업로드했는데 FTP 실패가 발생하면서 `The specified Content-Length is zero` 오류가 발생합니다. 어떻게 해야 하나요?

SDK는 샌드박스에 있는 파일만 지원합니다. FTP 기능을 사용하려면 먼저 샌드박스로 파일을 옮겨주십시오.

### SDK 통합 후 인터페이스로 업로드한 파일과 로컬 파일의 크기가 다를 경우 어떻게 해야 하나요? 

body를 설정한 후 로컬 파일에 수정이 없었는지 확인하십시오. 로컬 파일을 압축하는 도중이나 파일 쓰기가 완료되기 전에 인터페이스를 호출하여 업로드를 트리거할 경우 SDK는 업로드 시간의 파일 크기 기준으로 블록화하여 업로드를 진행합니다. 이로 인해 COS에 업로드된 파일과 로컬 파일의 크기가 달라집니다.

### SDK 통합 후 업로드 인터페이스를 호출했는데 "입력한 body URL이 로컬 URL이 아닙니다. 다시 확인해주십시오!!" 오류가 발생하면 어떻게 해야 하나요?

해결 방법:
URL이 file://로 시작하는지 확인하십시오. 아래 두 가지 방식으로 초기화할 수 있습니다.
1. [NSURL URLWithString:@"file:////var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]
2. [NSURL fileURLWithPath:@"/var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]


### SDK 통합 후 업로드 인터페이스를 호출했는데 업로드에 성공한 파일의 크기가 0인 경우 어떻게 하나요?

해결 방법:
1. 업로드 경로가 시스템 이미지 라이브러리 경로라면 파일 읽기 권한에 문제가 없는지 확인합니다. 예를 들어 `file:///var/mobile/Media/DCIM/101APPLE/` 경로는 직접 액세스할 수 없습니다. Photos 프레임워크 내의 request를 통해 이미지를 가져옵니다.
2. 애플리케이션을 iOS11과 호환하려면, 이미지 라이브러리에 비디오 업로드 시 다음을 재호출 합니다. `[[PHImageManager defaultManager] requestPlayerItemForVideo:asset options:option resultHandler:^(AVPlayerItem *playerItem, NSDictionary *info) {
    //즉시 샌드박스로 파일을 옮기거나 playerItem 저장
    }];`메소드는 playerItem 획득 후 저장, 또는 해당 콜백 중 업로드할 파일을 app의 샌드박스로 옮깁니다. iOS11의 playerItem이 폐기되면 파일의 읽기 권한이 사라지기 때문에 업로드한 파일의 크기가 0이 될 수 있습니다.
3. app 내의 샌드박스의 파일을 업로드할 경우 업로드된 파일이 샌드박스의 tmp 폴더에 있는지 확인합니다. 예를 들어 `/var/mobile/Containers/Data/Application/0BFBB3FE-0FD0-46CB-ADDE-DDE08F6D62C3/tmp/` 목록에 있는 파일들은 시스템에서 언제든지 삭제될 수 있으므로 업로드된 파일을 안전한 목록에 보관하여 업로드하는 과정에서 파일이 삭제되지 않도록 합니다. 샌드박스에 대한 자세한 사항은 [File System Basics](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/FileSystemOverview/FileSystemOverview.html)를 참고하십시오.

### SDK 통합 후 고급 인터페이스를 사용하여 업로드하는 중 `업로드 중 MD5 인증과 로컬이 일치하지 않습니다. 업로드하는 동안 로컬 파일이 수정되었는지 확인하십시오. 멀티파트 업로드 중에는 블록이 업로드될 때마다 MD5 및 로컬 블록과의 일치 여부 검사를 진행하며 일치하지 않으면 오류가 발생합니다.` 오류가 발생하면 어떻게 해야 하나요?

원인: 1MB보다 큰 파일을 업로드한 경우 발생하는 오류로, SDK를 사용하여 1MB가 넘는 파일을 업로드하면 약 1MB의 파일로 분할되어 멀티파트 업로드가 진행됩니다. 각 블록이 업로드 완료될 때마다 백그라운드 반환 etag와 로컬 파일의 블록을 비교해 일치하지 않을 경우 위와 같은 오류를 보냅니다.

해결 방법: 파일을 업로드하는 과정에서 수정된 부분이 있는지 확인해주십시오.



### SDK 요청 초과 시간 설정 방법은 무엇입니까?

해결: SDK 5.7.0 이후 요청 초과 시간을 사용자 정의할 수 있으며 설정 방법은 아래와 같습니다.
1. `QCloudServiceConfiguration *config = [QCloudServiceConfiguration new]`를 초기화합니다.
2. config의 `timeoutInterval` 속성을 설정합니다. 예시: `config의.timeoutInterval = 30;`


### COS iOS SDK에 crash가 발생하였습니다. 처리 방법은 무엇입니까?

현재 버전이 최신 버전인지 확인하시고, 구 버전일 경우 최신 SDK 버전으로 업그레이드 하시는 것을 권장합니다. 최신 버전의 iOS SDK는 [qcloud-sdk-ios](https://github.com/tencentyun/qcloud-sdk-ios)를 참고하십시오.


