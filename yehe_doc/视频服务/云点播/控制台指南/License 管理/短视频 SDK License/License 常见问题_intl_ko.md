### License 버전에 관한 문제는 무엇인가요?

UGSV SDK는 기본 버전과 엔터프라이즈 버전으로 나뉩니다. 4.5 버전부터는 License가 필요한데, 기본 버전은 UGSV의 License(TXUgcSDK.licence)만 필요하고 엔터프라이즈 버전은 Pitu의 License(YTFaceSDK.licence)도 함께 필요합니다. License를 프로젝트 디렉터리에 넣고 해당 이름으로 수정하면 됩니다.

4.9 버전부터는 License 사용 방법이 변경되었습니다. License를 프로젝트에 패키징 진행 여부를 선택할 수 있습니다. 사용 시 setLicenceURL:key: 인터페이스를 호출하여 License의 url과 key를 설정해야 합니다.

>! 4.5 - 4.7 버전의 SDK는 License 자동 연장을 지원하지 않고 4.9 버전부터 자동 연장을 지원합니다. SDK 4.9는 이전의 License(url과 key는 null을 전송할 수 없고 문자열은 자유롭게 전송할 수 있음)를 호환할 수 있지만 새로운 License는 4.9 이전의 SDK에서 사용할 수 없습니다.



### 테스트용 License 만료 후 연장이 가능한가요?

무료로 베타 버전 License를 신청할 수 있습니다(무료 베타 기간: 기본 14일, 1회 연장 가능, 연장 시 총 28일). 만료 후 바로 [정식 License 구매](https://intl.cloud.tencent.com/document/product/266/42077) 하시기 바랍니다.

>! 베타 기간 내 베타 테스트 연장을 신청한 경우 만료 시점은 베타 테스트 신청 시점을 기준으로 합니다. 베타 기간 종료 후 연장을 신청한 경우, 만료 시점은 베타 테스트 연장 신청 시점을 기준으로 합니다.
>- 베타 테스트 신청 시점이 '2021-08-12 10:28:41'일 경우 14일 후 만료 시점은 '2021-08-26 10:28:41'입니다.
>- 무료 연장 1회 시, 베타 테스트 기간 14일 이내에 연장을 신청한 경우 만료 시점은 '2021-09-09 10:28:41'입니다. 14일 베타 테스트 완료 후 연장을 신청한 경우, 예를 들어 '2021-08-30 22:26:20'에 연장을 신청하면 만료 시점은 '2021-09-13 22:26:20'가 됩니다.



### 테스트용 License는 Android의 PackageName과 iOS의 BundleID를 변경할 수 있나요?

변경할 수 있습니다. [VOD 콘솔](https://console.cloud.tencent.com/vod/license/video)에서 베타 License 정보 우측 상단에 있는 [편집]을 클릭하여 수정할 수 있습니다.



### 정식 License는 Android의 PackageName과 iOS의 BundleID를 변경할 수 있나요?

현재 버전에서 정식 License는 PackageName과 BundleID를 변경**할 수 없습니다**. 후속 버전에서 지원될 예정입니다.



### License는 여러 개의 App을 동시에 지원할 수 있나요?

하나의 License는 하나의 PackageName과 BundleID에만 대응하며 여러 개의 App을 지원하지 않습니다.



### License는 바인딩(Android의 PackageName과 iOS의 BundleID)을 어떻게 확인하나요?

작성할 때 사용자는 정식 출시한 App Store의 iOS에 해당하는 Bundle ID와 App Store에 정식으로 출시된 Android의 Package Name을 확인해야 합니다.



### License 기간 연장 시 “license not exist” 문제가 발생하는데 어떻게 해결하나요?

[VOD 콘솔]>[License 관리] >[[SDK License](https://console.cloud.tencent.com/vod/license/video)]에 로그인하여 하기 방법으로 진단할 수 있습니다.

1. **관리자** 페이지에서 License 바인딩 기간 연장을 할 수 있는지 확인하십시오.
2. 만약 **비관리자** 페이지에서 작업하고 있다면 **관리자**에게 연락하여 License 변경 작업에 대한 도움을 받으십시오.



### License를 추가할 수 없는데 어떻게 해결하나요?

바인딩 페이지가 **관리자** 페이지인지 확인하고 관리자 페이지를 선택하여 바인딩하십시오.



### License 검증 실패는 어떻게 진단하나요?

아래의 몇 가지 사항을 참고하여 진단하는 것을 권장합니다.

- License 유효 기간이 만료되었는지 확인하십시오.
- License 정보의 Package Name이 프로젝트에 있는 패키지 이름과 일치하는지 확인하십시오.
- License에 있는 LicenseUrl 프로토콜이 HTTPS인지 확인하십시오.

>? 위의 방법으로 문제를 해결할 수 없는 경우 **애플리케이션 언마운트 및 재설치** 또는 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 해결할 것을 권장합니다.



### bundleid가 없으면 Android에서 License를 사용할 수 없나요?

bundleid는 Android의 package name과 유사하여 iOS를 통합하지 않으면, 언제든지 입력하고 사용하지 않아도 됩니다.



### 라이트 버전의 UGSV SDK를 기본 버전 License로 업그레이드하려면, 어떻게 작업해야 하나요?

VOD 트래픽 리소스 패키지 50TB, 200TB 또는 1PB를 구매하여 기본 버전 License 사용 권한을 얻습니다.

>? 현재는 UGSV License만 라이트 버전에서 기본 버전으로 업그레이드를 지원하며, 업그레이드된 License는 해당 리소스 패키지에서 제공하는 License 사양입니다.



### 개인이 구매한 UGSV SDK License를 기업용으로 사용할 수 있나요?

현재 UGSV SDK는 구매한 계정에서만 사용할 수 있으며 개인 실명 인증이나 기업 실명 인증에 대한 제한은 없습니다.



### 내 서브 계정에 라이브 방송 및 VOD의 모든 권한을 부여했음에도 불구, 여전히 License 콘솔의 관련 인터페이스에 액세스할 수 없는 이유는 무엇입니까?



새 버전의 SDK License는 인터페이스가 업데이트되었습니다. 루트 계정에서 권한 부여 정책을 재설정해야 License 콘솔 페이지에 액세스할 수 있습니다.

- 서브 계정에 License 쿼리 권한만 부여하려면 QcloudVCUBEReadOnlyAccess 정책 관련 권한을 부여하십시오.
- 서브 계정에 모든 License 작업 권한을 부여하려면 QcloudVCUBEFullAccess 정책 관련 권한을 부여하십시오.

사용자/사용자 그룹에 정책을 연결하여 관련 작업 권한 부여하려면 [정책 권한 관리](https://intl.cloud.tencent.com/document/product/598/10602) 가이드를 참고하십시오.

>?  License 인터페이스의 모든 기능 및 작업은 CSS, VOD 정책과 독립적입니다. 즉, 기존 QcloudVODFullAccess, QcloudLIVEFullAccess 정책에는 더 이상 License 관련 인터페이스가 포함되지 않으며, 상기 설명에 따라 별도로 권한을 부여해야 합니다.