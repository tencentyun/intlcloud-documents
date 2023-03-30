>>!본 문서는 __IM__ CAM 기능에 대한 내용을 소개합니다. 기타 제품의 CAM 관련 내용은 [CAM 지원 제품](https://intl.cloud.tencent.com/document/product/598/10588)을 참고하십시오.
>
>IM CAM은 기본적으로 서브 계정을 정책과 바인딩하거나 정책을 서브 계정에 부여하는 것입니다. 개발자는 콘솔에서 사전 설정된 정책을 직접 사용하여 간단한 권한 작업을 구현할 수 있으며, 복잡한 권한 작업은 [사용자 정의 정책](https://intl.cloud.tencent.com/document/product/1047/38088)을 참고하십시오. .
>IM은 현재 다음과 같은 사전 설정 정책을 제공합니다.
>
><table class="table"><thead><tr><th>정책 이름</th><th>정책 설명</th></tr></thead>
><tbody><tr><td>QcloudAVCFullAccess</td><td>IM 전체 읽기/쓰기 액세스 권한</td></tr>
><tr><td>QcloudIMReadOnlyAccess</td><td>IM 읽기 전용 액세스 권한</td></tr></tbody></table>
>
>## 사전 설정 정책 사용 예시
>
>### IM 권한이 있는 서브 계정 만들기
>
>
>1. Tencent Cloud [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [**사용자 목록**](https://console.cloud.tencent.com/cam)에 접속하여 **사용자 생성**을 클릭합니다.
>2. ‘사용자 생성’ 페이지에서 **사용자 지정 생성**을 선택하여 ‘서브 계정 생성" 페이지로 이동합니다.
>>? CAM [서브 계정 사용자 정의 생성](https://intl.cloud.tencent.com/document/product/598/13674)의 가이드를 따라 ‘사용자 권한 설정’ 이전 단계를 완료하십시오.
>3. ‘사용자 권한 설정’ 페이지에서 다음을 진행합니다.
>  1. 사전 설정 정책 'Instant Messaging’을 검색 및 선택합니다.
>  2. **다음**을 클릭합니다.
>4. ‘정보 및 권한 검토’ 열 아래의 **완료**를 클릭하여 서브 계정 생성을 완료합니다. 완료 페이지에서 서브 사용자의 로그인 링크와 보안 자격 증명을 다운로드하여 보관합니다. 이에 포함된 정보는 아래 표와 같습니다.
><table class="table"><tbody><tr><td>정보</td><td>출처</td><td>기능</td><td>필수 저장 여부</td></tr>
><tr><td>로그인 링크</td><td>페이지에서 복사</td><td>루트 계정 입력 단계를 생략하고 편리하게 콘솔에 로그인</td><td>아니요</td></tr>
><tr><td>사용자 이름</td><td>보안 자격 증명 CSV 파일</td><td>콘솔 로그인 시 입력</td><td>예</td></tr>
><tr><td>비밀번호</td><td>보안 자격 증명 CSV 파일</td><td>콘솔 로그인 시 입력</td><td>예</td></tr>
><tr><td>SecretId</td><td>보안 자격 증명 CSV 파일</td><td>서버 API 호출 시 사용. 상세 정보는 <a href="https://intl.cloud.tencent.com/document/product/598/32675" target="_blank"> 액세스 키 참고</a></td><td>예</td></tr>
><tr><td>SecretKey</td><td>보안 자격 증명 CSV 파일</td><td>서버 API 호출 시 사용. 상세 정보는 <a href="https://intl.cloud.tencent.com/document/product/598/32675" target="_blank">액세스 키 참고</a></td><td>예</td></tr></tbody></table>
>5. 상기 로그인 링크 및 보안 자격 증명을 권한 수여자측에 제공하고, 수여자측은 해당 서브 계정을 사용하여 IM에 IM 콘솔 액세스 및 IM 서버 API 요청을 포함한 모든 작업을 진행할 수 있습니다.
>
>### 기존 서브 계정에 IM 권한 부여
>
>
>1. Tencent Cloud [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [**사용자 목록**](https://console.cloud.tencent.com/cam)에 접속하여 권한을 부여할 서브 계정을 클릭합니다.
>2. ‘사용자 세부 정보’ 페이지의 권한 열에서 **정책 추가**를 클릭하고, 서브 계정의 권한이 비어 있지 않은 경우 **정책 연결**을 클릭합니다.
>3. **정책 목록에서 정책 연결 선택**을 선택하고, 사전 설정된 정책 'Instant Messaging'을 검색 및 선택합니다. 페이지 안내에 따라 권한 부여 프로세스를 완료하십시오.
>
>
>### 서브 계정의 IM 권한 해제
>
>
>1. Tencent Cloud [루트 계정](https://intl.cloud.tencent.com/document/product/598/32633)으로 CAM 콘솔의 [**사용자 목록**](https://console.cloud.tencent.com/cam)에 접속하여 권한을 부여할 서브 계정을 클릭합니다.
>2. ‘사용자 세부 정보’ 페이지의 권한 열에서 사전 설정된 정책 'Instant Messaging'을 찾아 오른쪽의 **해제**를 클릭합니다. 페이지의 안내에 따라 권한 해제 프로세스를 완료합니다.
