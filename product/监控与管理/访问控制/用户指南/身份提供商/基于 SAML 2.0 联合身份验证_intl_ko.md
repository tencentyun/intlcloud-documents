Tencent Cloud는 SAML 2.0(Security Assertion Markup Language 2.0)에 기반한 페더레이션 ID 인증을 지원합니다. SAML 2.0은 많은 ID 공급업체에서 사용되는 일종의 개방형 표준입니다. ID 공급업체를 사용하면 페더레이션된 싱글 사인 온(Federated Single Sign-on, SSO)을 구현할 수 있습니다. 즉, 사용자가 페더레이션 ID 인증을 받은 사용자에게 Tencent Cloud 관리 콘솔에 로그인하거나 Tencent Cloud API를 호출하도록 권한을 부여할 수 있으며 기업 또는 조직의 멤버마다 하나의 CAM 서브 사용자를 생성할 필요가 없습니다. 또한 SAML 2.0은 통용 개방형 프로토콜이기 때문에 사용자 자체가 ID 프록시 코드를 작성할 필요가 없으며 직접 SAML을 사용하여 Tencent Cloud의 페더레이션 ID 인증 과정을 단순화할 수 있습니다.

## SAML ID 공급업체

ID 공급업체는 CAM의 개체이며 외부 신용 계정 모음으로 간주될 수 있습니다. SAML 2.0 페더레이션 ID 인증에 기반한 ID 공급업체는 SAML 2.0(Security Assertion Markup Language 2.0) 표준을 지원하는 ID 공급업체 서비스를 설명합니다. 기업 또는 조직의 멤버가 Tencent Cloud 리소스에 접근할 수 있도록 SAML 2.0 프로토콜이 호환한 ID 공급업체(예: Microsoft Active Directory 페더레이션 ID 인증 서비스)와 Tencent Cloud 간의 신뢰를 구축하려면 SAML ID 공급업체를 생성해야 합니다. SAML ID 공급업체를 생성하려면 [ID 공급업체 생성](https://intl.cloud.tencent.com/document/product/598/30290)을 참조하십시오.

## ID 공급업체 역할

SAML 제공업체를 생성한 후 SAML ID 공급업체를 역할 캐리어로 하는 하나 이상의 ID 공급업체 역할을 생성해야 합니다. 역할은 일련의 권한을 가지는 가상 ID이며 리소스 접근할 때 임시 보안 인증서가 사용됩니다. SAML 2.0 어설션의 컨텍스트에서 역할은 DP에 의해 인증된 페더레이션 ID 사용자에게 할당될 수 있습니다. 이 역할을 통해 ID 공급업체가 임시 보안 인증서를 요청하여 Tencent Cloud 리소스에 접근할 수 있습니다. 이 역할과 연결된 전략은 페더레이션 ID 사용자가 Tencent Cloud 리소스에 대한 접근 범위를 결정합니다. SAML 2.0 페더레이션 ID 인증에 기반한 ID 공급업체 역할 생성에 대해서는 [역할 생성](https://intl.cloud.tencent.com/document/product/598/19381)을 참조하십시오.
![](https://main.qcloudimg.com/raw/db597d52e89473d1a18b46ba150aa233.png)

## SAML 2.0에 기반한 페더레이션 ID 인증을 사용하여 Tencent Cloud API에 접근

![1](https://main.qcloudimg.com/raw/65eb02712b75d7bfcbba509b8f10be7c.png)
1.	기업 또는 조직 사용자는 클라이언트를 사용하여 ID 인증을 위해 기업의 ID 공급업체에 요청합니다.
2.	ID 공급업체는 기업의 ID 인증 시스템에 따라 인증을 실시합니다.
3.	사용자 인증 결과를 리턴합니다.
4.	ID 공급업체는 인증 결과에 따라 표준 SAML 2.0 어설션 문서를 생성하고 이를 클라이언트에 리턴합니다.
5.	클라이언트는 SAML 2.0 어설션, ID 공급업체의 리소스 설명 및 사용하는 ID 공급업체의 리소스 설명을 기반으로 sts: AssumeRoleWithSAML에 임시 보안 키를 신청합니다.
6.	STS는 SAML 2.0 어설션 정보를 검증합니다.
7.	검증 결과를 리턴합니다.
8.	리턴된 결과에 따라 임시 인증서를 신청하고 클라이언트에 리턴합니다.

## SAML 2.0 페더레이션 ID 인증을 기반으로 페더레이션 싱글 사인 온(SSO) 구현
![](https://main.qcloudimg.com/raw/10d90eb5e5f91927e873cec8dc0e5823.png)
1.	기업 또는 조직 사용자가 브라우저를 사용하여 Tencent Cloud 서비스에 접근합니다.
2.	Tencent Cloud 서비스는 인증 요청을 브라우저에 리턴합니다.
3.	브라우저가 기업 또는 조직의 ID 공급업체로 리디렉션됩니다.
4.	기업이 사용자 ID를 검증합니다.
5.	기업 사용자 ID 인증이 성공하고 사용자 정보가 ID 공급업체로 리턴됩니다.
6.	ID 공급업체가 표준 SAML 2.0 어설션을 생성하고 브라우저로 돌아갑니다.
7.	브라우저가 SAML 2.0 어설션을 Tencent Cloud로 리디렉션합니다.
8.	Tencent Cloud SSO 로그인 서비스를 시작하며 cAuth를 요청하고 사용자를 검증합니다.
9.	Tencent Cloud 검증 결과를 리턴합니다.
10.	검증은 성공하고 로그인 상태가 리턴됩니다.
11.	Tencent Cloud 콘솔 서비스로 리디렉션합니다.
