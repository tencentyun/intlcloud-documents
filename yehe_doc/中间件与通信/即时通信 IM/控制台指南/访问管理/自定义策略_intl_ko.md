>>!본 문서는 __IM__ CAM 기능에 대한 내용을 소개합니다. 기타 제품의 CAM 관련 내용은 [CAM 지원 제품](https://intl.cloud.tencent.com/document/product/598/10588)을 참고하십시오.
>
>IM CAM에서 [사전 설정 정책](https://intl.cloud.tencent.com/document/product/1047/38087)을 사용하여 권한을 부여하는 것은 편리하지만, 권한 제어 단위가 비교적 커서 IM 애플리케이션 및 [Tencent Cloud API](https://intl.cloud.tencent.com/product/api)까지 세분화되어있지 않습니다. 개발자가 더 세분화된 권한 제어 기능을 필요로 하는 경우, 사용자 정의 정책을 생성해야 합니다.
>
>
>## 사용자 정의 정책 생성 방법
>
>사용자 정의 정책 생성은 여러 가지 방법이 있으며, 하기 표는 여러 방법들의 비교표입니다. 구체적인 작업 프로세스는 다음을 참고하십시오.
>
><table class="table"><thead><tr><th>게이트</th><th>방법</th><th>효과(Effect)</th><th>리소스(Resource)</th><th>작업(Action)</th><th>유연성</th><th>난이도</th></tr></thead>
><tbody><tr><td><a href="https://console.cloud.tencent.com/cam/policy" target="_blank">CAM 콘솔</a></td><td>정책 생성기</td><td>수동 선택</td><td>구문 기술</td><td>수동 선택</td><td>중간</td><td>중간</td></tr>
><tr><td><a href="https://console.cloud.tencent.com/cam/policy" target="_blank">CAM 콘솔</a></td><td>정책 구문</td><td> 구문 기술</td><td> 구문 기술</td><td> 구문 기술</td><td>높음</td><td>높음</td></tr>
><tr><td>CAM 서버 API</td><td><a href="https://intl.cloud.tencent.com/document/product/598/32248" target="_blank">CreatePolicy</a></td><td> 구문 기술</td><td> 구문 기술</td><td> 구문 기술</td><td>높음</td><td>높음</td></tr></tbody></table>
>
>
>>?
>>- IM은 제품 기능별 또는 프로젝트별 사용자 정의 정책 생성을 __지원하지 않습니다__.
>>- __수동 선택__은 사용자가 콘솔에 표시된 후보 목록에서 객체를 선택함을 의미합니다.
>>- __구문 기술__은 [권한 부여 정책 구문](#.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95)을 통해 객체를 기술하는 것을 의미합니다.
>
>## 권한 부여 정책 구문
>
>### 리소스 구문 기술
>
>상기와 같이, IM 권한 관리의 리소스 세분성은 애플리케이션입니다. 애플리케이션의 정책 구문의 기술 방법은 [CAM 리소스 기술 방법](https://intl.cloud.tencent.com/document/product/598/10606)을 따릅니다. 하기 예시 중, 개발자의 루트 계정 ID는 12345678이고 개발자는 SDKAppID가 1400000000, 1400000001, 1400000002인 세 가지 애플리케이션을 생성합니다.
>
>- 모든 IM 애플리케이션의 정책 구문 기술
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/*"
>]
>```
>- 단일 애플리케이션의 정책 구문 기술
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/1400000001"
>]
>```
>- 다수 애플리케이션의 정책 구문 기술
>```
>"resource": [
>  "qcs::im::uin/12345678:sdkappid/1400000000",
>  "qcs::im::uin/12345678:sdkappid/1400000001"
>]
>```
>
>### 작업 구문 기술
>상기와 같이, TRTC 권한 관리 작업 세분성은 Tencent Cloud API입니다. 하기 예시에서는 'DescribeAppStatList'(애플리케이션 목록 가져오기) 및 'DescribeSdkAppInfo'(애플리케이션 정보 가져오기) 등 Tencent Cloud API를 예로 듭니다.
>- IM 모든 Tencent Cloud API 정책 구문 기술
>```
>"action": [
>  "name/im:*"
>]
>```
>- 단일 Tencent Cloud API 작업의 정책 구문 기술
>```
>"action": [
>  "name/im:DescribeAppStatList"
>]
>```
>- 다수 Tencent Cloud API 작업의 정책 구문 기술
>```
>"action": [
>  "name/im:DescribeAppStatList",
>  "name/im:DescribeTrtcAppAndAccountInfo"
>]
>```
>
>## 사용자 정의 정책 사용 예시
>
>### 정책 생성기 사용
>
>다음 예시 중에서는 사용자 정의 정책을 생성합니다. 해당 정책은 IM 애플리케이션인 1400000001에 대해 모든 작업을 허용합니다.
>1. Tencent Cloud [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [**정책**](https://console.cloud.tencent.com/cam/policy)에 접속하여 **사용자 정의 정책 생성**을 클릭합니다.
>2. **정책 생성기로 생성**을 선택하여 정책 생성 페이지로 이동합니다.
>3. 서비스 및 작업을 선택합니다.
>	-**효과(Effect)** 설정 항목에서 **허용**을 선택합니다.
>	-**서비스(Service)** 설정 항목에서 **IM**을 선택합니다.
>	-**작업(Action)** 설정 항목에서 모든 항목을 선택합니다.
>	-**리소스(Resource)** 설정 항목은 [리소스 구문 기술](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0) 설명에 따라 `qcs::im::uin/12345678:sdkappid/1400000001`을 기입합니다.
>	-**조건(Condition)** 설정 항목은 설정할 필요가 없습니다.
>	- **성명문 추가**를 클릭하면 페이지 하단에 ‘IM 애플리케이션 1400000001에 모든 작업 허용’ 문구가 나타납니다.
>4. 같은 페이지에 다른 성명문을 계속 추가합니다.
>	-**효과(Effect)** 설정 항목에서 **거부**를 선택합니다.
>	-**서비스(Service)** 설정 항목에서 **IM**을 선택합니다.
>	-**작업(Action)** 설정 항목에서 `RemoveUser`를 선택합니다(검색 기능을 통해 빠른 찾기 가능).
>	-**리소스(Resource)** 설정 항목은 [리소스 구문 기술](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0) 설명에 따라 `qcs::im::uin/12345678:sdkappid/1400000001`을 기입합니다.
>	-**조건(Condition)** 설정 항목은 설정할 필요가 없습니다.
>	- **성명문 추가**를 클릭하면 페이지 하단에 ‘IM 애플리케이션 1400000001에 `RemoveUser` 작업 금지’ 문구가 나타납니다.
>5. **다음**을 클릭하고 필요에 따라 정책 이름을 수정합니다(또는 수정하지 않음).
>6. **완료**를 클릭하여 사용자 정의 정책 생성을 완료합니다.
>
>
>이 정책을 다른 서브 계정에 부여하는 방법은 [기존 서브 계정에 IM 읽기/쓰기 액세스 권한 부여](https://intl.cloud.tencent.com/document/product/1047/38087)와 동일합니다.
>
>
>### 정책 구문 사용
>
>하기 예시에서는 1400000001 및 1400000002 IM 애플리케이션에 대해 모든 작업을 허용하는 사용자 정의 정책을 생성합니다.
>
>
>1. Tencent Cloud [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [**정책**](https://console.cloud.tencent.com/cam/policy)에 접속하여 **사용자 정의 정책 생성**을 클릭합니다.
>2. **정책 구문으로 생성**을 선택하여 정책 생성 페이지로 이동합니다.
>3. **템플릿 유형 선택** 상자에서 **빈 템플릿**을 선택합니다.
> >?정책 템플릿은 기존 정책(사전 설정 또는 사용자 지정 정책)을 복사한 다음 정책을 수정하여 신규 정책을 생성하는 데 사용됩니다. 상황에 따라 적절한 정책 템플릿을 사용하여 정책 정의의 난이도와 작업량을 줄일 수 있습니다. 
>4. **다음**을 클릭하고 필요에 따라 정책 이름을 수정합니다(또는 수정하지 않음).
>5. **정책 내용 편집**  상자에 정책 내용을 입력합니다. 본 예시의 정책 내용은 다음과 같습니다.
>```
>{
> "version": "2.0",
> "statement":[
>     {
>         "effect": "allow",
>         "action": [
>             "name/im:*"
>         ],
>         "resource": [
>             "qcs::im::uin/12345678:sdkappid/1400000001",
>             "qcs::im::uin/12345678:sdkappid/1400000002"
>         ]
>     },
>     {
>         "effect": "deny",
>         "action": [
>             "name/im:RemoveUser"
>         ],
>         "resource": [
>             "qcs::im::uin/12345678:sdkappid/1400000001"
>         ]
>     }
> ]
>}
>```
>>? 정책의 내용은 [CAM 정책 구문 로직](https://intl.cloud.tencent.com/document/product/598/33415)을 따라야 하며, 리소스 및 작업의 두 요소의 구문은 상기 [리소스 구문 기술](#.E8.B5.84.E6.BA.90.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0) 및 [작업 구문 기술](##.E6.93.8D.E4.BD.9C.E8.AF.AD.E6.B3.95.E6.8F.8F.E8.BF.B0)을 참고하십시오.
>6. **정책 생성**을 클릭하여 사용자 정의 정책 생성을 완료합니다.
>이 정책을 다른 서브 계정에 부여하는 방법은 [기존 서브 계정에 IM 읽기/쓰기 액세스 권한 부여](https://intl.cloud.tencent.com/document/product/1047/38087)와 동일합니다.
>
>### CAM에서 제공하는 서버 API 사용
>
>대부분의 개발자는 콘솔에서 권한 관리 작업을 수행하여 서비스 요구 사항을 충족할 수 있습니다. 그러나 권한 관리 기능을 자동화하고 체계화해야 하는 경우, 서버 API를 통해 실현할 수 있습니다.
>정책 관련 서버 API는 CAM에 속하며, 자세한 사항은 [CAM 공식 홈페이지 문서](https://intl.cloud.tencent.com/document/product/598)를 참고하시기 바랍니다. 다음은 몇 가지 주요 인터페이스 입니다.
>
>- [정책 생성](https://intl.cloud.tencent.com/document/product/598/32248)
>- [정책 삭제](https://intl.cloud.tencent.com/document/product/598/32247)
>- [사용자에 정책 바인딩하기](https://intl.cloud.tencent.com/document/product/598/32249)
>- [사용자에 정책 바인딩 해제하기](https://intl.cloud.tencent.com/document/product/598/32245)
