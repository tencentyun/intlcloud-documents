본문은 License를 사용할 때 발생할 수 있는 몇 가지 질문에 대한 답변입니다.

[](id:q1)
### License는 SDK와 어떤 관련이 있습니까?
License는 SDK 기능에 대한 승인을 얻는 데 필요한 키 및 경로로 이해될 수 있으며, SDK는 전체 서비스의 특정 소프트웨어 패키지, 소프트웨어 프레임워크 및 운영 체제를 더 잘 사용하기 위해 제공되는 소프트웨어 개발 키트입니다. Tencent Effect SDK의 License 정보는 Key와 LicenseURL의 쌍으로 구성됩니다. 이를 가져와서 SDK에 입력한 후 SDK 기능을 활성화할 수 있습니다.

[](id:q2)
### 프로덕션 Tencent Effect SDK License는 어떻게 얻나요?
비즈니스에서 Tencent Effects SDK 기능을 사용하려면 과금 개요를 참고하여 필요에 따라 SDK 패키지를 선택 및 구입할 수 있습니다. SDK 패키지를 구입하고 License 잠금 해제 권한을 획득합니다. 해당 패키지 구입 완료 후 비즈니스 매니저에게 연락주시면 빠른 시일 내에 정식 SDK 버전을 발급해 드립니다.

[](id:q3)
### License의 유효 기간은 어떻게 됩니까? 만료 후 어떻게 갱신합니까?
- **평가판 License**: 유효기간은 승인 후 License 발급일로부터 1개월(28일)입니다. 예를 들어 평가판 License를 2022년 01월 01일에 신청하고 승인 시 2022년 01월 02일에 자동으로 발급되는 경우 2022년 01월 31일 00:00:00에 만료됩니다.
- **프로덕션 License**: 유효기간은 승인 후 License 발급일로부터 1년(365일)입니다. 예를 들어 프로덕션 License를 2022년 01월 01일에 신청하고 승인 시 2022년 01월 02일에 자동으로 발급되는 경우 2023년 01월 03일 00:00:00에 만료됩니다.

[](id:q4)
### 발급된 License의 패키지 이름을 수정할 수 있습니까?
평가판 License의 Android용 Package Name 및 iOS용 Bundle ID를 수정할 수 있습니다.

프로덕션 License가 바인딩되면 Package Name 및 Bundle ID를 수정할 수 없습니다.

[](id:q5)
### License는 몇 개의 패키지 이름과 장치를 지원합니까?
License가 추가될 때마다 두 개의 패키지 이름(Bundle ID 및 Package Name)을 지원할 수 있습니다. 계정에 추가할 수 있는 License의 수나 승인된 기기의 수에는 제한이 없습니다.

[](id:q6)
### Tencent Effect SDK를 어떻게 업그레이드 또는 다운그레이드합니까?
Tencent Effect SDK는 [과금 개요](https://intl.cloud.tencent.com/document/product/1143/45371)에 자세히 설명된 대로 10가지 버전을 제공합니다. 프로덕션 License가 만료된 후 사용 사례에 더 적합한 버전을 구입할 수 있습니다. License 유효 기간 중에는 SDK를 업그레이드 또는 다운그레이드할 수 없습니다.

평가판 License는 최종 버전 S1 - 04의 인증을 발급하며 모든 SDK 기능을 테스트할 수 있습니다. 만료되기 전에 사용 사례와 일치하는 프로덕션 SDK 및 License로 전환할 수 있습니다.
