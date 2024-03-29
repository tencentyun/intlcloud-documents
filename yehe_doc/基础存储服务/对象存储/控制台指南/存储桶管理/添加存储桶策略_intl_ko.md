## 소개

Cloud Object Storage(COS) 콘솔을 통해 버킷 정책을 추가함으로써 임의의 계정이나 출처 IP(또는 IP 필드)가 정책이 설정된 COS 리소스에 액세스하는 것을 허용 또는 금지할 수 있습니다. 버킷 정책 개요 및 정책 예시 관련 정보는 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023) 및 [버킷 정책 예시](https://intl.cloud.tencent.com/document/product/436/45235)를 참고하십시오. 다음은 버킷 정책 추가 방법에 대한 자세한 소개입니다.

>! 루트 계정당 버킷 ACL 규칙은 최대 1,000개까지 생성할 수 있습니다.
>

## 전제 조건

생성된 버킷에 대한 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참고하십시오.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. 버킷 정책을 추가할 버킷을 찾고 해당 버킷 이름을 클릭하여 버킷 설정 페이지로 이동합니다.
3. 왼쪽 사이드바에서 **권한 관리 > Policy 권한 설정**을 클릭합니다. COS가 제공하는 버킷 ​​정책을 추가하는 아래의 방법으로 버킷 정책을 추가할 수 있습니다. 구성 항목에 대한 자세한 내용은 [개요](https://intl.cloud.tencent.com/document/product/436/18023)를 참고하십시오.

<dx-tabs>
::: 비주얼 에디터(Visual Editor)
비주얼 에디터 탭 페이지에서 **정책 추가**를 클릭합니다. 팝업 창에서 템플릿을 선택하고 정책을 구성하는 두 단계로 정책을 구성합니다.

(1) 템플릿 선택

COS는 버킷 정책을 신속하게 구성하는 데 도움이 되도록 선택한 리소스 범위 및 승인된 사용자(권한 부여자)의 조합에 따라 다양한 템플릿을 제공합니다.

- 피부여자
 - **모든 사용자(익명 액세스 허용)**: 익명 사용자에게 작업 권한을 부여하려면 이 옵션을 선택합니다. 이 옵션을 선택하면 2단계의 정책 구성 중에 모든 사용자(`*`로 표시)가 자동으로 선택됩니다. 익명 사용자에게 버킷 리스팅(ListBucket) 및 버킷 구성 권한 구성과 같은 작업에 대한 권한을 부여하는 것은 위험하기 때문에 COS는 이 옵션을 선택할 때 해당 템플릿을 제공하지 않습니다. 필요한 경우 2단계에서 ‘정책을 구성’하는 동안 정책을 추가할 수 있습니다.
 - **지정된 사용자**: 지정된 서브 계정, 루트 계정 또는 클라우드 서비스에 작업 권한을 부여하려면 이 옵션을 선택합니다. 2단계의 정책 구성 중에 특정 계정 UIN을 추가로 지정해야 합니다.

 **Note:**
  - 권한이 부여된 사용자가 지정된 계정인 경우 요청 객체에 본인 확인을 위한 서명이 있어야 하며, 서명 방법은 [서명 요청](https://intl.cloud.tencent.com/document/product/436/7778)을 참고하십시오.
  - 권한이 부여된 사용자를 전체 사용자로 지정하면 객체 요청 시 서명이 필요 없으며, 모든 사용자가 링크를 통해 객체에 직접 액세스할 수 있어 데이터가 유출될 리스크가 있으니 신중하게 설정하십시오.

- 리소스 범위
 - **전체 버킷**: 버킷 구성 권한을 구성하거나 리소스 범위를 전체 버킷으로 설정하려는 경우 이 옵션을 선택하면 2단계의 정책 구성 중에 전체 버킷을 리소스로 자동 추가할 수 있습니다.
 - **지정된 디렉터리**: 리소스 범위를 지정된 폴더로 제한하려는 경우 이 옵션을 선택합니다. 2단계에서 정책을 구성하는 동안 특정 디렉터리를 추가로 지정해야 합니다. 이 옵션을 선택하면 COS는 버킷 구성과 관련된 정책 템플릿을 제공하지 않습니다. 이러한 권한의 경우 전체 버킷을 리소스로 지정해야 하기 때문입니다.

- 템플릿: 권한을 부여할 작업 그룹입니다.
 - **사용자 정의 정책(사전 설정 미제공)**: 템플릿을 사용할 필요가 없는 경우 이 옵션을 선택하고 2단계 ‘정책 설정’에서 필요에 따라 정책을 추가할 수 있습니다.
 - **기타 템플릿**: 인증된 사용자 및 리소스 범위의 다양한 조합 선택에 따라 COS는 다양한 정책 템플릿을 제공합니다. 해당 템플릿을 선택한 후, 2단계 정책 설정에서 COS가 자동으로 해당 작업을 추가합니다.
 **Note:** 템플릿에서 제공하는 권한 부여 작업이 요구 사항을 충족하지 않는 경우 2단계 ‘정책 설정’에서 권한 부여 작업을 추가하거나 삭제할 수 있습니다.

템플릿 설명은 아래 표를 참고하십시오.

<table>
   <tr>
      <th style="width:10%">피부여자</td>
      <th style="width:5%">리소스 범위</td>
      <th style="width:15%">정책 템플릿</td>
      <th style="width:20%">설명</td>
   </tr>
   <tr>
      <td colspan=2>모든 조합</td>
      <td>사용자 정의 정책</td>
      <td>인증된 사용자 및 리소스 범위의 조합에 대해 이 템플릿을 선택하면 사전 설정된 정책이 제공되지 않습니다. 2단계 정책 설정에서 정책을 직접 추가할 수 있습니다.</td>
   </tr>
   <tr>
      <td rowspan=4>모든 사용자(익명 액세스 가능)</td>
      <td rowspan=2>전체 버킷</td>
      <td>읽기 전용 객체(객체 리스트 제외)</td>
      <td rowspan=4>COS는 익명 사용자에 대해 파일 읽기(예: 다운로드) 및 파일 쓰기(예: 업로드 및 수정) 권장 템플릿을 제공합니다. <br><br>COS 권장 템플릿에는 데이터 보안을 위해 버킷의 모든 객체 나열, 읽기/쓰기 권한, 버킷 설정 등 민감한 권한이 포함되어 있지 않습니다.<br><br>필요한 경우 후속 단계에서 작업 권한을 추가 또는 삭제할 수 있습니다.</td>
   </tr>
   <tr>
      <td>객체 읽기 및 쓰기(객체 리스트 나열 제외)</td>
   </tr>
   <tr>
      <td rowspan=2>지정된 디렉터리</td>
      <td>읽기 전용 객체(객체 리스트 제외)</td>
   </tr>
   <tr>
      <td>객체 읽기 및 쓰기(객체 리스트 나열 제외)</td>
   </tr>
   <tr>
      <td rowspan=11>지정된 사용자</td>
      <td rowspan=7>전체 버킷</td>
      <td>읽기 전용 객체(객체 리스트 제외)</td>
      <td rowspan=7>COS는 지정된 사용자와 전체 버킷의 조합에 대해 가장 많은 권장 템플릿을 제공합니다. 파일 읽기 및 쓰기, 파일 나열 외에도 COS에는 신뢰할 수 있는 사용자에게 적합한 다음과 같은 민감 권한 템플릿이 포함되어 있습니다. <br>버킷 및 객체 ACL 읽기 및 쓰기: 버킷 ACL 및 객체 ACL 가져오기, 수정. GetObjectACL, PutObjectACL, GetBucketACL, PutBucketACL 포함. <br>버킷 일반 설정 항목: 버킷 태그, 교차 출처, Origin-pull 및 기타 민감하지 않은 권한. <br>버킷 민감 설정 항목: 버킷 정책, 버킷 ACL, 버킷 삭제와 같은 민감한 권한이 포함되므로 신중히 사용해야 합니다.</td>
   </tr>
   <tr>
      <td>읽기 전용 객체(객체 리스트 나열 포함)</td>
   </tr>
   <tr>
      <td>객체 읽기 및 쓰기(객체 리스트 나열 제외)</td>
   </tr>
   <tr>
      <td>객체 읽기 및 쓰기(객체 리스트 나열 포함)</td>
   </tr>
   <tr>
      <td>버킷 및 객체 ACL 읽기 및 쓰기</td>
   </tr>
   <tr>
      <td>버킷에 대한 일반 설정 항목</td>
   </tr>
   <tr>
      <td>버킷에 대한 민감 설정 항목</td>
   </tr>
   <tr>
      <td rowspan=4>지정된 디렉터리</td>
      <td>읽기 전용 객체(객체 리스트 제외)</td>
      <td rowspan=4>COS는 지정된 사용자와 지정된 디렉터리의 조합에 대해 파일 읽기(예: 다운로드) 및 파일 쓰기(예: 업로드, 수정) 외에도 , 객체 리스트 나열 권한을 포함하는 권장 템플릿을 제공합니다.<br>지정된 사용자에 대해 지정된 폴더의 읽기, 쓰기 및 파일 나열 권한을 개방하려면 이 조합을 권장합니다.<br>필요에 따라 후속 단계에서 작업 권한을 추가하거나 삭제할 수 있습니다.</td>
   </tr>
   <tr>
      <td>읽기 전용 객체(객체 리스트 나열 포함)</td>
   </tr>
   <tr>
      <td>객체 읽기 및 쓰기(객체 리스트 나열 제외)</td>
   </tr>
   <tr>
      <td>객체 읽기 및 쓰기(객체 리스트 나열 포함)</td>
   </tr>
</table>

(2) 정책 구성

1단계에서 선택한 권한 부여된 사용자, 지정된 디렉터리 및 템플릿의 조합에 대해, COS는 해당 작업, 권한 부여된 사용자, 리소스 등을 정책 설정에 자동으로 추가합니다. 지정된 사용자 및 지정된 디렉터리를 선택한 경우, 정책 설정 시 특정 사용자 UIN 및 디렉터리를 지정해야 합니다.

COS에서 제공한 권장 템플릿이 요구 사항에 맞지 않을 경우 이 단계에서 권한이 부여된 사용자, 리소스 및 작업 추가 또는 삭제 등 정책 내용을 수정할 수 있습니다. 설정 항목 설명은 다음과 같습니다.
- 유효성: 정책 구문의 ‘허용’ 및 ‘거부’에 해당하는 ‘allow’ 또는 ‘deny’ 선택을 지원합니다.
- 사용자: 모든 사용자(`*`), 루트 계정, 서브 계정 및 클라우드 서비스 등 권한이 부여된 사용자 추가 및 삭제를 지원합니다.
- 리소스: 전체 버킷 또는 지정된 디렉터리 리소스 추가를 지원합니다.
- 작업: 권한을 부여해야 하는 작업을 추가 또는 삭제합니다.
- 조건: 사용자의 IP 액세스 제한 등 권한 부여 시 조건을 지정합니다.

(3) 구성 정보 확인

  설정 정보에 오류가 없는지 확인한 후, **완료**를 클릭합니다. 이 때 서브 계정을 사용해 COS 콘솔에 로그인하면 정책에 설정된 리소스 범위에 한해 액세스할 수 있습니다.

:::
::: 정책 구문
(1) **편집**을 클릭해 정의한 정책 구문을 입력합니다. COS는 다양한 시나리오의 정책 구문을 제공합니다. 자세한 내용은 [COS API 권한 부여 정책 사용 가이드](https://intl.cloud.tencent.com/document/product/436/30580)를 참고하십시오.
(2) 정책 구문이 올바른지 확인한 후 저장을 클릭합니다. 이때 서브 계정을 이용하여 COS 콘솔에 로그인하면 정책에서 설정한 리소스 범위에만 액세스할 수 있습니다.
:::
</dx-tabs>


