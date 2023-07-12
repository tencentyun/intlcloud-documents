## 장애 현상

- COS API, SDK로 리소스 업로드 및 다운로드 시 403 에러 코드 반환
- 임시 키 또는 서브 계정으로 COS 리소스 액세스 시 403 에러 코드 반환
- COS bucket 설정 수정 시 403 에러 코드 반환

## 장애 분석 방식

COS 요청에 403 에러 코드가 나타나면 다음 절차를 참고하여 문제의 원인을 진단할 수 있습니다.
1. 요청이 CORS 크로스 도메인 액세스 요청인지 확인하십시오. 실패한 크로스 도메인 요청은 ["AccessForbidden"](#message-.E4.B8.BA-.E2.80.9Caccessforbidden.E2.80.9D)을 반환합니다.
2. 요청이 버킷 링크 도용 방지 설정에 히트되었는지 확인하십시오. 링크 도용 방지 규칙으로 인한 403 에러 코드에 대해 COS는 ["You are denied by bucket referer rule"](#message-.E4.B8.BA-.E2.80.9Cyou-are-denied-by-bucket-referer-rule.E2.80.9D)을 반환합니다.
3. 요청이 익명 요청인지 확인하고, 공개 읽기가 아닌 객체에 서명이 없는 요청을 보내면 "Access Denied"를 반환합니다. 버킷 또는 객체에 대한 공개 읽기 설정은 [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315) 또는 [객체의 액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13327)을 참고하십시오.
4. 요청 키와 요청 서명이 올바른지 확인합니다.
   1. SecretId 사용 시 서명이 정확하지 않으면 COS는 ["InvalidAccessKeyId"]를 반환합니다.
   2. 해당 기기의 시간이 정확하지 않거나 요청 시간이 서명의 유효 기간을 초과한 경우 COS는 ["RequestTimeTooSkewed"](#message-.E4.B8.BA-.E2.80.9Crequesttimetooskewed.E2.80.9D) 또는 ["Request has expired"](#message-.E4.B8.BA-.E2.80.9Crequest-has-expired.E2.80.9D)를 반환합니다.
   3. COS는 서명 생성의 계산 방식에 문제가 있는 경우 ["SignatureDoesNotMatch"](#message-.E4.B8.BA-.E2.80.9Csignaturedoesnotmatch.E2.80.9D)를 반환합니다.
5. 요청을 제안한 서브 계정 또는 임시 키에 해당 액세스 권한이 부여되었는지 확인합니다.
   1. 서브 계정의 액세스 권한을 확인하고, 리소스 액세스 권한이 없는 서브 계정 요청은 ["Access Denied."](#message-.E4.B8.BA-.E2.80.9Caccess-denied..E2.80.9D)가 반환됩니다.
   2. 임시 키로 제안된 요청의 경우 임시 키 신청 시 작성하는 정책에 따라 임시 키 요청의 리소스 범위가 제한되며, 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.
6. 요청 객체가 ARCHIVE 유형인지 또는 DEEP ARCHIVE 유형인지 확인합니다. 이러한 요청 COS는 ["InvalidObjectState"](#message-.E4.B8.BA-.E2.80.9Cinvalidobjectstate.E2.80.9D)를 반환합니다.

## 장애 진단 및 처리

### Message가 'Access Denied.'인 경우

COS 액세스 시 아래 정보가 출력되는 경우,
```
<Code>AccessDenied</Code>
<Message>Access Denied.</Message>
```

다음 작업을 진행해야 합니다.

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 선택해 버킷 관리 페이지로 이동합니다.
3. 작업할 버킷을 찾아 버킷 이름을 클릭하여 버킷 설정 페이지로 이동합니다.
4. 왼쪽 사이드바에서 **권한 관리 > 버킷 액세스 권한**을 선택해 버킷 액세스 관리 페이지로 이동합니다.
5. '버킷 액세스 권한'에서 COS에 액세스하는 계정에 액세스 권한을 설정했는지 확인합니다.
 - 예. 다음 단계를 실행합니다.
 - 아니오. **사용자 추가**를 클릭하여 COS에 액세스하는 계정에 필요한 권한을 설정합니다.

6. 액세스 권한이 설정된 계정에 필요한 권한을 부여했는지 확인합니다.
 - 예. 다음 단계를 실행합니다.
 - 아니오. **편집**을 클릭하여 다시 설정하십시오.
7. 'Policy 권한 설정'에서 COS에 액세스하는 계정에 policy 라이선스 정책이 설정되어 있는지 확인합니다.
>! 
> - 버킷 액세스 권한이 개인 읽기이고 Policy 권한이 익명 액세스인 경우, Policy 권한의 우선순위가 버킷 액세스 권한보다 높습니다.
> - Policy 라이선스 정책에서 동일한 서브 계정에 허용 및 금지 정책을 동시에 설정한 경우, 금지 정책의 우선순위가 허용 정책보다 높습니다.
> - Policy 라이선스 정책에서 '모든 사용자' 정책의 우선순위가 '지정 사용자' 정책보다 낮습니다.
> 
 - 예. 다음 단계를 실행합니다.
 - 아니오. **정책 추가**를 클릭하고 실제 서명 액세스 시 계정에 필요한 권한에 따라 설정합니다.

8. Policy 권한을 설정한 계정에 필요한 권한을 부여했는지 확인합니다.
 - 예. 다음 단계를 실행합니다.
 - 아니오. **편집**을 클릭하여 다시 설정하십시오.
9. COS 리소스 액세스 시 사용하는 q-ak 매개변수가 타깃 버킷에 소속된 계정(대소문자 구분)인지 확인합니다.
 - 예. 다음 단계를 실행합니다.
 - 아니요. q-ak 매개변수를 해당 타깃 버킷의 소속 계정으로 수정합니다.
10. COS 리소스 액세스 시 교차 계정으로 액세스했는지 확인합니다.
 - 예. 계정에 대한 교차 계정 인증을 진행하십시오. 자세한 내용은 교차 계정의 서브 계정에 지정된 파일에 대한 읽기/쓰기 권한 인증을 참고하십시오.
 - 해당 오류가 아닌 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.

### Message가 'AccessForbidden'인 경우

COS 액세스 시 아래 정보가 출력되는 경우,
```
<Code>AccessDenied</Code>
<Message>AccessForbidden</Message>
```

다음 작업을 진행해야 합니다.

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 선택해 버킷 관리 페이지로 이동합니다.
3. 작업할 버킷을 찾아 버킷 이름을 클릭하여 버킷 설정 페이지로 이동합니다.
4. 왼쪽 사이드바에서 **보안 관리 > 크로스 도메인 액세스(CORS) 설정**을 선택해 크로스 도메인 액세스 CORS 설정 페이지로 이동합니다.
5. '크로스 도메인 액세스(CORS) 설정'에서 크로스 도메인 요청 여부를 확인합니다.

 - 예. 다음 단계를 실행합니다.
 - 아니요. 규칙을 수정합니다.
6. 다음 명령어를 실행하여 크로스 도메인 요청이 정확하게 설정되어 있는지 확인합니다.
```
curl 'http://bucket-appid.cos.ap-guangzhou.myqcloud.com/object' -voa /dev/null -H 'Origin: 크로스 도메인 액세스(CORS) 설정의 출처 Origin'
```
다음 정보가 반환되면 정확하게 설정되었다는 의미입니다.
![](https://main.qcloudimg.com/raw/67513acee63f2f632b6cba58461fbe3d.png)

### Message가 'You are denied by bucket referer rule'인 경우

COS 액세스 시 아래 정보가 출력되는 경우,
```
<Code>AccessDenied</Code>
<Message>You are denied by bucket referer rule</Message>
```

다음 작업을 진행해야 합니다.

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 선택해 버킷 관리 페이지로 이동합니다.
3. 작업할 버킷을 찾아 버킷 이름을 클릭하여 버킷 설정 페이지로 이동합니다.
4. 왼쪽 사이드바에서 **보안 관리 > 링크 도용 방지 설정**을 선택해 링크 도용 방지 설정 페이지로 이동합니다.
5. '링크 도용 방지 설정'에서 링크 도용 방지를 설정했는지 확인합니다.

 - 예. 다음 단계를 실행합니다.
 - 해당 오류가 아닌 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.
6. 다음 명령어를 실행하여 링크 도용 방지가 정확하게 설정되어 있는지 확인합니다.
```
curl 'http://bucket-appid.cos.ap-guangzhou.myqcloud.com/object' -voa /dev/null -H 'referer: Referer 값'
```
다음 정보가 반환되면 정확하게 설정되었다는 의미입니다.
![](https://main.qcloudimg.com/raw/acc9862c6ffab6fd81c42136b775f2ea.png)


### Message가 'InvalidAccessKeyId'인 경우

COS 액세스 시 아래 정보가 출력되는 경우,
```
<Code>AccessDenied</Code>
<Message>InvalidAccessKeyId</Message>
```

다음 작업을 진행해야 합니다.

1. 요청 서명 Authorization의 q-ak 매개변수를 정확하게 입력했는지 확인합니다.
 - 예. 다음 단계를 실행합니다.
 - 아니요. q-ak 매개변수를 수정합니다. 키의 SecretId는 q-ak 매개변수와 동일해야 하며 대소문자를 구분합니다.
2. [API 키 관리](https://console.cloud.tencent.com/cam/capi)로 이동해 API 키가 활성화되어 있는지 확인합니다.

 - 해당 오류일 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.
 - 아니요. 해당 API 키를 활성화합니다.


### Message가 'InvalidObjectState'인 경우

COS 액세스 시 아래 정보가 출력되는 경우,
```
<Code>AccessDenied</Code>
<Message>InvalidObjectState</Message>
```

다음 작업을 진행해야 합니다.

요청하는 객체가 CAS 또는 DEEP ARCHIVE 유형인지 확인합니다.
- 예. 객체 복구 후 다시 액세스합니다. 자세한 작업 방법은 [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633)를 참조하십시오.
- 해당 오류가 아닌 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.


### Message가 'RequestTimeTooSkewed'인 경우

COS 액세스 시 아래 정보가 출력되는 경우,
```
<Code>AccessDenied</Code>
<Message>RequestTimeTooSkewed</Message>
```

다음 작업을 진행해야 합니다.

1. 운영 체제 유형에 따라 클라이언트의 현재 시간을 확인합니다.
 - Windows 시스템(Windwos Server 2012 기준): ![](https://main.qcloudimg.com/raw/ac22b052ee24273ebeab1139dd7f4d58.png)**> 제어판 > 시간, 언어 및 지역 > 날짜 및 시간**.

 - Linux 시스템: `date -R` 명령어 실행
![](https://main.qcloudimg.com/raw/88288162bd1de8c2ec0b640f0df6799e.png)
2. 클라이언트의 현재 시간과 서버 시간에 오차가 있는지 오차 시간이 15분을 초과하는지 확인합니다.
 - 예. 시간을 동기화합니다.
 - 해당 오류가 아닌 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.


### Message가 'Request has expired'인 경우

COS 액세스 시 아래 정보가 출력되는 경우,
```
<Code>AccessDenied</Code>
<Message>Request has expired</Message>
```

예상 원인은 다음과 같습니다.
- 요청 시작 시간이 서명 유효 시간을 초과한 경우
- 로컬 시스템 시간과 해당 지역 시간이 일치하지 않는 경우

서명 유효시간을 다시 설정하거나 로컬 시스템 시간을 동기화해야 합니다. 해당 방법으로도 해결되지 않는 경우 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하십시오.


### Message가 'SignatureDoesNotMatch'인 경우

COS 액세스 시 아래 정보가 출력되는 경우,
```
<Code>AccessDenied</Code>
<Message>SignatureDoesNotMatch</Message>
```

다음 작업을 진행해야 합니다.

클라이언트가 계산한 서명과 서버가 계산한 서명이 일치하는지 확인합니다.
- 해당 오류일 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.
- 아니요. [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하여 COS 서명 툴을 사용해 직접 구현되는 서명 과정을 확인하십시오.
