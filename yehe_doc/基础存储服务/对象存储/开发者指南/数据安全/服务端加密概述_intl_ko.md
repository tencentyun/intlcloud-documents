## 개요

COS(Cloud Object Storage)는 데이터가 디스크에 기록되기 전에 객체 레벨에서 데이터를 암호화하고 데이터에 액세스할 때 자동으로 데이터를 해독합니다. 암호화 및 복호화는 서버에서 완료됩니다. 서버 측 암호화는 정적 데이터를 효과적으로 보호할 수 있습니다.

>!
> - 암호화 객체와 비암호화 객체를 액세스할 때 경험적 측면에서는 차이가 없으나 객체에 대한 액세스 권한 보유 여부를 전제로 합니다.
> - 서버 암호화는 객체 데이터 암호화만 지원하며 객체 메타데이터 암호화는 지원하지 않습니다. 서버로 암호화한 객체의 경우에는 반드시 익명 사용자가 아닌 유효한 서명으로 액세스해야 합니다.
> 

## 적용 시나리오

- **기밀 데이터 스토리지 시나리오:** 서버 암호화로 저장할 기밀 데이터를 암호화하여 사용자의 개인 정보를 보호할 수 있습니다. 암호화 데이터는 사용자가 액세스할 때 자동으로 해독됩니다.
- **기밀 데이터 전송 시나리오:** COS는 기밀 데이터를 전송할 때 HTTPS로 SSL 인증서를 배포하여 암호화하는 기능을 제공합니다. 전송 링크 계층에 계층 암호화를 구현함으로써 데이터가 전송 과정에서 도난되거나 조작될 위험을 차단합니다.

## 암호화 방식
COS는 SSE-COS, SSE-KMS, SSE-C와 같은 다양한 서버 암호화 방식을 지원합니다. 사용자에게 적합한 암호화 방식을 채택하여 COS에 저장하는 데이터를 암호화할 수 있습니다.

### SSE-COS 암호화

SSE-COS 암호화는 COS가 키를 호스팅하여 관리하는 서버 암호화 방식입니다. Tencent Cloud COS에서 마스터 키를 호스팅하고 데이터를 관리하며, 사용자는 COS를 통해 데이터를 직접 관리하고 암호화할 수 있습니다. SSE-COS는 여러 요소로 강력한 암호화를 구현함으로써 모든 객체를 고유한 보안키로 암호화합니다. 또한 256비트의 고급 암호화 표준(AES-256)을 채택하여 데이터를 암호화하며, 정기적으로 마스터 키를 교체해 보안키 자체를 암호화합니다.

>!
>- `POST`를 실행하여 객체를 업로드할 경우, `x-cos-server-side-encryption` 헤더가 아닌 테이블 필드에 동일한 정보를 제공해야 합니다. 자세한 내용은 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)를 참고하십시오.
>- 사전 서명한 URL로 업로드한 객체는 SSE-COS 암호화를 적용할 수 없습니다. COS 콘솔이나 HTTP 요청 헤더를 통해 서버 암호화를 실행해야 합니다.

#### COS 콘솔 사용
[객체 암호화 설정](https://intl.cloud.tencent.com/document/product/436/30929) 콘솔 문서를 통해 콘솔에서 객체에 SSE-COS 암호화하는 방법을 확인할 수 있습니다.

#### REST API 사용

>!
>- 버킷의 객체를 나열할 때 객체의 암호화 여부와 관계없이 리스트는 모든 객체의 리스트를 반환합니다.
>- POST를 실행하여 객체를 업로드할 경우, 해당 요청의 헤더가 아닌 테이블 필드에 동일한 정보를 제공하십시오. 자세한 내용은 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)를 참고하십시오.

사용자가 다음의 인터페이스를 요청하면 `x-cos-server-side-encryption` 헤더를 제공하여 서버 암호화를 적용합니다. 자세한 내용은 [공통 요청 헤더 - SSE-COS](https://intl.cloud.tencent.com/document/product/436/7728)를 참고하십시오.

- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)

### SSE-KMS 암호화

SSE-KMS 암호화는 KMS가 키를 호스팅하여 관리하는 서버 암호화 방식입니다. KMS는 Tencent Cloud가 선보인 보안 관리형 서비스로서 3rd party가 인증하는 하드웨어 보안 모듈(HSM, Hardware Security Module)로 보안키를 생성하여 보호합니다. KMS로 보안키를 간편하게 생성하고 관리할 수 있어 다양한 애플리케이션과 작업에 필요한 보안키 관리가 편리할 뿐만 아니라 모니터링과 컴플라이언스 니즈를 충족할 수 있습니다.

처음 SSE-KMS 암호화 방식을 사용할 경우, [KMS 서비스 활성화](https://intl.cloud.tencent.com/pricing/kms?lang=en&pg=)가 필요합니다. KMS 서비스를 활성화하면 마스터 키(CMK)가 기본으로 생성됩니다. [KMS 콘솔](https://console.cloud.tencent.com/kms2)에서도 보안키를 직접 생성하고, 보안키 정책과 사용 방법을 정의할 수 있으며, KMS를 사용하면 키 구성 요소의 출처를 **KMS** 또는 **외부**로 직접 선택할 수 있습니다. 자세한 내용은 [Creating a Key](https://intl.cloud.tencent.com/document/product/1030/31971)와 [Importing External Key](https://intl.cloud.tencent.com/document/product/1030/32795)를 참고하십시오.

>!
> - SSE-KMS는 객체 데이터에 한해 암호화하며, 객체의 메타데이터는 암호화 대상이 아닙니다.
> - 현재 SSE-KMS는 베이징, 상하이, 중국홍콩, 광저우 리전에 한해 지원합니다.
> - SSE-KMS 방식으로 암호화할 경우, KMS에서 부과하는 별도 요금이 발생합니다. 자세한 내용은 [KMS 과금 개요](https://intl.cloud.tencent.com/document/product/1030/31966)를 참고하십시오.
> - SSE-KMS 방식으로 암호화한 객체는 익명 사용자가 아닌 유효한 서명으로 액세스해야 합니다.

#### COS 콘솔 사용

[객체 암호화 설정](https://intl.cloud.tencent.com/document/product/436/30929) 콘솔 문서를 통해 콘솔에서 객체에 SSE-KMS 암호화하는 방법을 확인할 수 있습니다.

#### REST API 사용

>!
>
>- 버킷의 객체를 나열할 때 객체의 암호화 여부와 관계없이 리스트는 모든 객체의 리스트를 반환합니다.
>- POST를 실행하여 객체를 업로드할 경우, 해당 요청의 헤더가 아닌 테이블 필드에 동일한 정보를 제공하십시오. 자세한 내용은 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)를 참고하십시오.

사용자가 다음의 인터페이스를 요청하면 `x-cos-server-side-encryption` 헤더를 제공하여 서버 암호화를 적용합니다. 자세한 내용은 [공통 요청 헤더 - SSE-KMS](https://intl.cloud.tencent.com/document/product/436/7728)를 참고하십시오.

- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)

#### 주의사항
SSE-KMS 암호화에 **COS 콘솔**을 사용한 적이 없고 SSE-KMS 암호화에 **API**만 사용한 경우 먼저 [CAM 역할](https://intl.cloud.tencent.com/document/product/598/19420)을 생성해야 합니다. 자세한 생성 순서는 다음과 같습니다.
1. CAM 콘솔에 로그인하고 [역할](https://console.cloud.tencent.com/cam/role) 페이지로 이동합니다.
2. **역할 생성**을 클릭하고 **Tencent Cloud 제품 서비스**를 역할 엔터티로 선택합니다.
3. 역할을 지원하는 서비스로 **COS**를 선택하고 **다음 단계**를 클릭합니다.
4. **QcloudKMSAccessForCOSRole** 역할 정책을 검색하여 선택한 후 **다음 단계**를 클릭합니다.
![](https://main.qcloudimg.com/raw/b3d8ef7f3c534f33207c47b7fb7725fb.png)
5. 역할 태그 키와 값을 설정하고 **다음 단계**를 클릭합니다.
6. 지정된 역할 이름(COS_QcsRole)을 입력합니다.
7. **완료**를 클릭하여 프로세스를 완료합니다.

### SSE-C 암호화

SSE-C 암호화는 사용자 지정 키로 서버를 암호화하는 방식입니다. 암호화 키는 사용자가 직접 제공하는 것이며, 객체를 업로드할 때 COS는 사용자가 제공한 암호화 키로 사용자의 데이터에 AES-256 암호화를 적용합니다.

>!
>- COS는 사용자가 제공한 암호화 키를 저장하지 않으며, 암호화 키를 저장할 때 임의 데이터의 HMAC 값을 추가합니다. HMAC 값은 사용자의 객체 액세스 요청을 검증하는 데 사용됩니다. COS에서 임의 데이터의 HMAC 값으로 암호화 키 값을 도출하거나 암호화된 객체의 콘텐츠를 복호화할 수 없습니다. 이 때문에 암호화 키를 분실하면 해당 객체를 다시 획득할 수 없습니다.
>- POST를 실행하여 객체를 업로드할 경우, `x-cos-server-side-encryption-*` 헤더가 아닌 테이블 필드에 동일한 정보를 제공해야 합니다. 자세한 내용은 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)를 참고하십시오.
>- SSE-C는 API를 통해서만 사용할 수 있으며, 콘솔에서는 지원하지 않습니다.

#### REST API 사용

사용자가 다음의 인터페이스를 요청할 때, PUT과 POST에 대한 요청은 `x-cos-server-side-encryption-*` 헤더 제공으로 서버를 암호화할 수 있습니다. GET과 HEAD에 대한 요청이 SSE-C로 암호화한 객체일 경우, `x-cos-server-side-encryption-*` 헤더를 제공하여 지정한 객체를 복호화해야 합니다. 자세한 내용은 [공통 요청 헤더 -SSE-C](https://intl.cloud.tencent.com/document/product/436/7728)를 참고하십시오. 다음은 지원하는 헤더 작업 항목입니다.

- [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)
- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)
- [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)
- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750)
- [POST Object](https://intl.cloud.tencent.com/document/product/436/14690)
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)

