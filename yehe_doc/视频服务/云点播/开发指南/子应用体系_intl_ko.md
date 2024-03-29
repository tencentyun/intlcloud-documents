## 개요
VOD는 리소스를 분리할 수 있는 **서브 애플리케이션** 기능을 제공합니다. 이 기능은 VOD 내부의 리소스 분배 방식에 대한 개념입니다. 서브 애플리케이션은 독립 VOD 계정과 유사합니다. 서브 애플리케이션이 생성된 후 VOD 리소스의 소유권은 다음과 같습니다.
<img src="https://main.qcloudimg.com/raw/58880e642525a040fc3bcd5e5c6d12b9.png" width="595">
>? 본문에서 언급된 **리소스**에는 VOD의 미디어 파일과 그 속성, 파생 파일, 구성, CDN 도메인 이름 및 VOD 서비스 사용 통계가 포함됩니다.

### 응용 시나리오
다음은 VOD 서브 애플리케이션의 몇 가지 일반적인 사용 사례입니다.

- **다중 부서/다중 비즈니스 격리**: 회사는 Tencent Cloud를 기반으로 자체 제품을 개발하려고 합니다. A 부서는 VOD를 사용하여 UGSV 애플리케이션을 개발하고 B 부서는 영화 및 텔레비전 웹 사이트를 개발할 계획입니다. 이 두 VOD 사업은 서로 격리되어야 합니다. 다만, 재무상의 이유로 부서별로 독립적인 Tencent Cloud 계정을 생성할 수는 없습니다. 이 경우 VOD의 서브 애플리케이션 기능을 사용하여 부서별로 서브 애플리케이션을 할당할 수 있습니다. 
- **권한 제어**: 위의 다중 부서/다중 비즈니스 격리 시나리오에서 개발자는 각 부서에 자체 비즈니스와 연결된 서브 애플리케이션에만 액세스 권한을 부여하고 다른 서브 애플리케이션에는 액세스 권한을 부여하지 않는 것과 같은 추가 권한 제어 요구 사항이 있을 수 있습니다. 이 경우, 계정 관리자는 각 부서(A, B)에 서브 사용자를 할당하고 해당 VOD 서브 애플리케이션에 대한 접근 권한을 부여할 수 있습니다. 자세한 설명은 [액세스 관리](https://intl.cloud.tencent.com/document/product/266/33970)를 참고하십시오.
- **프로덕션 환경과 테스트 환경 간의 분리**: 프로덕션 환경의 운영에 영향을 주지 않고 일부 VOD 기능(예: [이벤트 알림](https://intl.cloud.tencent.com/document/product/266/33948) 방법 수정 또는 [링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33984) 활성화)을 테스트하려는 경우 프로덕션 환경과 하나는 테스트 환경용입니다. 새로운 기능은 먼저 테스트 환경에서 테스트한 다음 성공적인 검증 후에 프로덕션 환경에서 사용할 수 있습니다.

### 역할 정의 및 식별
VOD 서브 애플리케이션 시스템의 역할에는 관리자, 기본 애플리케이션 및 서브 애플리케이션이 포함됩니다. 그 정의는 아래와 같습니다.
<img src="https://main.qcloudimg.com/raw/c873e8cdb0eb762df5d899efc13aa7cc.png" width="724" >

1. VOD 서비스를 활성화하면 모든 VOD 리소스가 속한 **기본 애플리케이션**의 기본 역할이 됩니다. 기본 애플리케이션 ID는 콘솔의 [[계정 정보]](https://console.cloud.tencent.com/developer)에서 볼 수 있는 Tencent Cloud APPID입니다.
2. VOD 서브 애플리케이션 기능을 활성화하면 VOD 리소스를 소유하지 않는 **관리자** 역할이 생성되며 모든 리소스는 여전히 기본 애플리케이션에 속합니다.
3. 관리자 역할로 **서브 애플리케이션**을 생성하면 새 서브 애플리케이션에 별도의 VOD 리소스가 생깁니다. 기본 애플리케이션(특수 서브 애플리케이션으로 볼 수 있음)과 동일하고 기본 애플리케이션과 분리되어 있습니다. 서브 애플리케이션을 만들 때 VOD는 서브 애플리케이션 ID라고 하는 전역 고유 ID를 할당합니다. ID를 보는 방법에 대한 자세한 내용은 [콘솔 사용 설명 - 애플리케이션 관리](#p1)를 참고하십시오. 
4. 관리자 역할에서 다른 **서브 애플리케이션**을 생성하는 경우 새 서브 애플리케이션에도 별도의 VOD 리소스가 있습니다. 새 서브 애플리케이션, 기본 애플리케이션 및 기타 모든 서브 애플리케이션은 서로 동일하고 격리되는 식입니다.

>?개별적으로 명시되지 않는 한 기본 애플리케이션과 서브 애플리케이션은 다음 섹션에서 구분되지 않으며 통일적으로 **서브 애플리케이션**이라고 합니다.

### 기능
VOD 서브 신청 시스템은 다음과 같은 기능을 제공합니다.

- 서브 애플리케이션 생성 및 설정: VOD 서브 애플리케이션 기능을 활성화한 후 콘솔에서 관리자로 서브 애플리케이션을 생성하고 각 서브 애플리케이션의 이름과 설명을 설정할 수 있습니다.
- 서브 애플리케이션 비활성화: 기본 애플리케이션을 제외한 모든 서브 애플리케이션을 비활성화할 수 있습니다. 서브 애플리케이션이 비활성화되면 해당 VOD 리소스가 지워지지 않으며 비디오 업로드 및 트랜스코딩과 같은 다른 기능은 영향을 받지 않습니다. 대신 해당 도메인 이름만 비활성화됩니다.
- 리소스 격리: 서로 다른 서브 애플리케이션의 VOD 리소스가 서로 격리됩니다.
- 콘솔 또는 서버 API를 통해 모든 서브 애플리케이션의 VOD 리소스를 조작할 수 있습니다.
- 스토리지 사용량, 대역폭/트래픽, 트랜스코딩 기간, 지능형 비디오 인식 기간 및 재생 데이터와 같은 각 서브 애플리케이션에 대해 독립적인 통계가 생성됩니다.
- 모든 서브 애플리케이션에 대한 집계된 통계가 제공됩니다.

<span id ="p4"></span>
### 제한
VOD 서브 신청 시스템에는 다음과 같은 제한 사항이 있습니다.

- 기본 애플리케이션의 이름과 설명은 수정할 수 없습니다.
- 서브 애플리케이션은 삭제할 수 없습니다.
- 하나의 VOD 계정으로 최대 50개의 서브 애플리케이션을 생성할 수 있습니다.
- 서브 애플리케이션에 대해 별도의 청구 로직(예: 청구 모드 및 별도 청구 생성)을 설정할 수 없습니다. VOD 계정의 모든 서브 애플리케이션은 동일한 계정에 속하며 모든 VOD 사용 데이터(저장, 트래픽, 트랜스코딩 지속 시간 및 지능형 비디오 인식 지속 시간과 같은 VOD 청구 가능 항목을 포함하되 이에 국한되지 않음)는 요금 계산 및 통합 청구를 위해 집계됩니다.

<span id="p3"></span>
## 콘솔 사용 설명

### 서브 애플리케이션 기능 활성화

1. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인합니다.
2. 왼쪽 사이드바에서 [서브 애플리케이션 활성화]를 클릭하여 서브 애플리케이션 활성화 페이지로 이동합니다.
3. [시작하기]를 클릭하여 VOD의 서브 애플리케이션 기능을 활성화합니다.

>? 서브 애플리케이션 기능이 이미 활성화된 경우 왼쪽 사이드바의 [서브 애플리케이션 활성화]가 표시되지 않습니다.

### 역할 선택
서브 애플리케이션 기능이 활성화되면 역할을 선택할 수 있는 VOD 콘솔의 왼쪽 상단 모서리에 드롭다운 목록이 표시됩니다. 방금 서브 애플리케이션 기능을 활성화한 경우 드롭다운 목록에는 [관리자]와 [기본 애플리케이션]의 두 가지 역할만 있습니다. 서브 애플리케이션을 만든 후에는 드롭다운 목록에 역할로 표시됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0dc90b954520c36cddac7a9d78c24cf8.png)

### 관리자
관리자 역할 아래의 왼쪽 사이드바에는 [서비스 개요], [애플리케이션 관리] 및 [UGSV License] 항목이 표시됩니다.

- 서비스 개요: 이 페이지는 VOD 청구 모드, 모든 서브 애플리케이션의 집계된 주요 비즈니스 데이터 및 각 서브 애플리케이션의 주요 비즈니스 데이터를 표시합니다.
- <span id = "p1"></span>애플리케이션 관리: 이 페이지에서 서브 애플리케이션을 보거나 생성, 편집 또는 비활성화할 수 있습니다. 서브 애플리케이션 ID도 이 페이지에 표시됩니다.

### 서브 애플리케이션
서브 애플리케이션 역할에서 VOD 콘솔의 사용은 기본적으로 서브 애플리케이션 기능이 활성화되기 전과 동일하며 서브 애플리케이션의 VOD 리소스를 보고 조작할 수 있습니다. 주요 차이점은 서브 애플리케이션 자체에 별도의 청구 구성이 없다는 것입니다. 

## 서버 API 사용 설명
서브 애플리케이션 기능을 활성화한 후 VOD 서버 API를 사용할 때 액세스하려는 리소스가 있는 서브 애플리케이션을 지정해야 합니다.

<span id = "p2"></span>
### 서버 API에서 서브 애플리케이션 지정
VOD 서버 API가 [TencentCloud API 3.0](https://intl.cloud.tencent.com/product/api) 으로 업그레이드되었습니다. 각 API에서 ```SubAppId``` 매개변수를 사용하여 액세스하려는 서브 애플리케이션을 지정할 수 있습니다. 기본 애플리케이션에 액세스하려면 기본 애플리케이션 ID를 입력하거나 이 매개변수를 비워 둘 수 있습니다. 

### 서버 API 2017에서 서브 애플리케이션 지정
서버 API 2017은 서브 애플리케이션도 지원합니다. 사용 시 요청에 `SubAppId` 매개변수(대소문자 구분)를 추가해야 합니다. 이 매개변수는 서버 API 2017의 공통 요청 매개변수와 동일한 수준이며 그 값은 서브 애플리케이션 ID입니다. 기본 애플리케이션에 액세스하려면 기본 애플리케이션 ID를 입력하거나 이 매개변수를 비워 둘 수 있습니다.

>?
>- 서버 API 2017 설명서에는 `SubAppId` 매개변수가 공개되어 있지 않으므로 사용에 영향을 미치지 않습니다.
>- `SubAppId` 매개변수는 동일한 계산 규칙의 서버 API에 대한 서명 계산에도 관여합니다.

## 파일 업로드 설명
VOD 서브 애플리케이션 기능을 활성화한 후 미디어 파일을 업로드할 서브 애플리케이션을 지정해야 합니다.

### 라이브 방송 녹음
[라이브 방송 녹화](https://intl.cloud.tencent.com/document/product/267/31563)를 사용하면 `vod_sub_app_id=xxx`(`xxx`는 서브 애플리케이션 ID 참고)를 라이브 방송 푸시 매개변수에 추가하여 지정된 서브 애플리케이션에서 녹음 파일을 생성할 수 있습니다. 기본 애플리케이션에서 녹음 파일을 생성하려면 이 매개변수를 비워 두십시오.

### 서버에서 업로드
[서버에서 업로드](https://intl.cloud.tencent.com/document/product/266/33912)는 지정된 서브 애플리케이션에 대한 파일 업로드를 지원합니다. 매개변수 설정 방법에 대한 자세한 내용은 아래 링크를 참고하십시오. 기본 애플리케이션에 파일을 업로드하려면 기본 애플리케이션 ID를 입력하거나 해당 매개변수를 비워 둘 수 있습니다.

#### SDK 방식
* [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)
* [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916)
* [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
* [Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918)
* [Golang SDK](https://intl.cloud.tencent.com/document/product/266/33919)

#### 서버 API 방식
[ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120) 및 [CommitUpload](https://intl.cloud.tencent.com/document/product/266/34119) API는 업로드에 사용됩니다. 자세한 내용은 [서버 API에서 서브 애플리케이션 지정](#p2)을 참고하십시오.
업로드에는 SDK를 사용하는 것이 좋습니다.

### 클라이언트에서 업로드
[클라이언트에서 업로드](https://intl.cloud.tencent.com/document/product/266/33921)를 사용하면 [클라이언트에서 업로드할 서명](https://intl.cloud.tencent.com/document/product/266/33922)에 `vodSubAppId=xxx`(`xxx`는 서브 애플리케이션 ID 참고)를 추가하여 지정된 서브 애플리케이션에 파일을 업로드할 수 있습니다. 기본 애플리케이션에 파일을 업로드하려면 기본 애플리케이션 ID를 입력하거나 이 매개변수를 비워 둘 수 있습니다.

>?`vodSubAppId` 매개변수는 동일한 계산 규칙에서 클라이언트에서 업로드할 서명 계산에도 관여합니다.

### URL에서 업로드
URL에서 업로드를 사용하면 지정된 서브 애플리케이션에 파일을 업로드할 수 있습니다.

* 콘솔을 통해: 자세한 내용은 [콘솔 사용 설명](#p3)을 참고하십시오.
* 서버 API를 통해: [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118) API를 사용합니다. 자세한 내용은 [서버 API에서 서브 애플리케이션 지정](#p2)을 참고하십시오.

## 권한 관리
VOD는 CAM에 연결되어 서브 애플리케이션 수준에서 권한 부여를 지원합니다. 자세한 내용은 [액세스 관리](https://intl.cloud.tencent.com/document/product/266/33970)를 참고하십시오.

## FAQ
#### 서브 애플리케이션 기능이 활성화된 후 프로덕션 환경의 기존 비즈니스 로직에 영향을 줍니까?
아니요. 서브 애플리케이션 시스템은 호환성을 염두에 두고 설계되었습니다. 서브 애플리케이션 ID를 지정하지 않으면 모든 서버 API가 기본적으로 기본 애플리케이션을 조작합니다.

#### 서브 애플리케이션 기능을 활성화하는 데 요금이 부과됩니까?
서브 애플리케이션 기능 자체는 무료입니다. 그러나 각 서브 애플리케이션에서 사용하는 리소스는 VOD [과금 규칙](https://intl.cloud.tencent.com/document/product/266/2838)에 따라 VOD 계정으로 청구됩니다.

#### 우리 회사는 서브 애플리케이션 기능을 사용하여 비즈니스 격리를 구현합니다. 사업별 내부 정산/비용 배분은 어떻게 이루어지나요?
위의 [한도](#p4)에 설명된 대로 VOD는 전체 계정에 대해 하나의 집계된 청구서를 생성합니다. 비용 할당이 필요한 사업이 여러 개인 경우 VOD에서 제공하는 서브 애플리케이션 수준 통계를 기반으로 할당 비용을 정의하고 계산할 수 있습니다.

#### VOD 서비스가 중단되면 서브 애플리케이션은 어떻게 됩니까?
연체로 인해 VOD 서비스가 중단되는 경우, 귀하 계정의 모든 서브 애플리케이션이 비활성화됩니다.

#### 한 서브 애플리케이션에서 다른 서브 애플리케이션으로 비디오를 마이그레이션할 수 있습니까?
다른 서브 애플리케이션의 리소스는 격리되므로 한 서브 애플리케이션의 리소스를 다른 서브 애플리케이션으로 마이그레이션할 수 없습니다.
