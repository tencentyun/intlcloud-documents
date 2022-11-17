본문은 License를 사용할 때 발생할 수 있는 몇 가지 질문에 대한 답변입니다.

[](id:q1)

### License, License Key 및 Tencent Effects SDK는 어떤 관계인가요?

Tencent Effects SDK를 합법적으로 사용하려면 Tencent Cloud에서 발급한 License가 필요합니다. License 없이 Tencent Effect를 사용하는 것은 권리 침해에 해당합니다. 사용 가능한 License에는 평가판 License와 공식 License의 두 가지 유형이 있습니다.

SDK는 특정 소프트웨어 패키지, 소프트웨어 프레임워크 또는 운영 체제용 애플리케이션 생성을 용이하게 하는 소프트웨어 개발 툴 모음입니다. Tencent Cloud에서 License를 발급받으면 License Key와 License URL이 제공되며, 이 URL이 SDK에 입력되어야 Tencent Effect SDK의 기능을 사용할 수 있습니다.

[](id:q2)

### Tencent Effect의 공식 License는 어떻게 얻나요?

Tencent Effect 에디션을 구매하고 Tencent Effect SDK를 사용할 수 있는 License 를 얻으려면 가격 개요 문서를 참고하십시오. 에디션을 구매한 후 Tencent Effect 콘솔에서 바인딩해야 해당 기능을 사용할 수 있습니다. 자세한 사용법은 [공식 License 구매하기](https://www.tencentcloud.com/document/product/1143/50266#.E8.B4.AD.E4.B9.B0.E6.AD.A3.E5.BC.8F.E7.89.88-license)를 참고하십시오.

[](id:q3)

### License의 유효 기간은 어떻게 됩니까? 만료 후 어떻게 갱신합니까?

- **평가판 License**: 평가판 License는 발급 후 1개월(28일) 동안 유효합니다. 예를 들어 평가판 License를 2022년 01월 01일에 신청하고 2022년 01월 02일에 발급받은 경우 License는 2022년 01월 31일 00:00:00에 만료됩니다.
- **공식 License**: 공식 License는 콘솔에 바인딩한 후 1년(365일) 동안 유효합니다. 예를 들어, 2022년 1월 1일에 공식 License를 바인딩했다면 2023년 1월 2일 00:00:00(UTC+8)에 만료됩니다.
- 새 패키지를 구입하고 애플리케이션에 바인딩하여 애플리케이션의 공식 License를 갱신합니다. 자세한 안내는 [공식 License 갱신](https://www.tencentcloud.com/document/product/1143/50266#.E6.9B.B4.E6.96.B0.E6.AD.A3.E5.BC.8F.E7.89.88-license-.E6.9C.89.E6.95.88.E6.9C.9F)을 참고하십시오.

[](id:q4)

### License에 바인딩된 Package Name 및 Bundle ID를 수정할 수 있나요?

평가판 License에 바인딩된 Android Package Name 및 iOS Bundle ID를 변경할 수 있습니다.

단, 공식 License에 바인딩된 Package Name 및 Bundle ID는 변경할 수 없습니다.

[](id:q5)

### License를 사용할 수 있는 애플리케이션과 장치는 몇 개입니까?

하나의 Bundle ID와 하나의 Package Name을 각 License에 바인딩할 수 있습니다. 계정이 가질 수 있는 License 수 또는 License를 사용할 수 있는 장치 수에는 제한이 없습니다.

[](id:q6)

### Tencent Effect License를 어떻게 업그레이드하거나 다운그레이드합니까?

Tencent Effect SDK는 14개 버전으로 제공됩니다. 기능에 대한 자세한 내용은 [가격 리스트](https://intl.cloud.tencent.com/document/product/1143/45371)를 참고하십시오. 다른 SDK 버전으로 변경하려면 현재 License가 만료될 때까지 기다렸다가 다른 에디션을 구매하여 애플리케이션에 바인딩하십시오. License가 아직 유효한 경우 SDK 버전을 변경할 수 없습니다.

평가판으로 제공되는 에디션은 모든 기능을 갖춘 S1 - 04입니다. 평가판 License가 만료되기 전에도 공식 License로 업그레이드할 수 있습니다.

### 루트 계정이 서브 계정에 부여한 권한 중 Tencent Effect 관련 권한을 검색할 수 없는 이유는 무엇입니까?
<img src="https://qcloudimg.tencent-cloud.cn/raw/281d3924082074812e3bcf3b33811685.png" style="zoom:50%;" />

vcube를 검색하여 Tencent Effect 관련 작업에 대한 권한을 부여할 수 있습니다.
- 서브 계정에 License 쿼리 권한만 부여하려면 QcloudVCUBEReadOnlyAccess 정책 관련 권한을 부여하십시오.
- 서브 계정에 모든 License 작업 권한을 부여하려면 QcloudVCUBEFullAccess 정책 관련 권한을 부여하십시오.

