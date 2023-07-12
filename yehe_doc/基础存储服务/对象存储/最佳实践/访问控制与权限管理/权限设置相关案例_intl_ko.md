## 버킷 정책(Policy)을 이용한 권한 부여 사례

### 준비 과정

1. 버킷 생성
버킷 정책(Policy)을 통해 특정 버킷에 대해서만 권한을 부여하므로, 먼저 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)이 필요합니다. 계정 차원에서 권한을 부여해야 하는 경우 본 문서의 [CAM을 이용한 권한 부여 사례](#cam)를 참조하십시오.
2. 권한을 부여 받을 계정의 UIN 준비
본 문서는 타깃 버킷의 루트 계정 UIN이 100000000001이고, 해당 계정의 서브 계정이 100000000011이며, 서브 계정이 권한을 받아야만 타깃 버킷에 액세스할 수 있다고 가정합니다.
>?
>- 루트 계정에서 생성한 서브 계정 조회가 필요한 경우 CAM 콘솔에 로그인한 후 [사용자 리스트](https://console.cloud.tencent.com/cam)에서 확인할 수 있습니다.
>- 새로운 서브 계정을 생성해야 하는 경우 [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674) 문서를 확인하십시오.
>
3. **정책 추가** 대화 상자를 엽니다.
타깃 버킷의 **권한 관리**로 이동하여 **Policy 권한 설정 > 그래픽 설정**을 선택한 후, **정책 추가** 대화 상자를 클릭한 다음 본 문서의 권한 부여 사례를 참고하여 설정을 진행합니다. 정책 추가에 대한 자세한 작업 가이드는 [버킷 정책 추가](https://intl.cloud.tencent.com/document/product/436/30927) 문서를 참조하십시오.

다음은 몇 가지 권한 부여 사례 예시로, 사용자의 실제 상황에 따라 참고하여 설정합니다.

### 권한 부여 사례

#### 사례1: 서브 계정에 특정 디렉터리의 모든 권한 부여
설정 정보는 다음과 같습니다.

|설정 항목|설정값|
|------|------|
|효과|허용|
|사용자| 서브 계정을 선택한 후 서브 계정의 UIN을 입력하고, 해당 서브 계정은 반드시 현재 루트 계정의 서브 계정이어야 합니다(예: 100000000011)|
|리소스|지정된 리소스 경로 선택(예: `folder/sub-folder/*`|
|작업|모든 작업 선택|



#### 사례2: 서브 계정에 특정 디렉터리 내 모든 파일의 읽기 권한 부여

설정 정보는 다음과 같습니다.

|설정 항목          |          설정값|
|------|------|
|효과        |       허용|
|사용자| 서브 계정을 선택한 후 서브 계정의 UIN을 입력하고, 해당 서브 계정은 반드시 현재 루트 계정의 서브 계정이어야 합니다(예: 100000000011)|
|리소스|지정된 리소스 경로 선택(예: `folder/sub-folder/*`|
|작업          |       읽기 작업(객체 리스트 나열 포함)|



#### 사례3: 서브 계정에 특정 파일의 읽기 및 쓰기 권한 부여

설정 정보는 다음과 같습니다.

|설정 항목|설정값|
|------|------|
|효과|허용|
|사용자| 서브 계정을 선택한 후 서브 계정의 UIN을 입력하고, 해당 서브 계정은 반드시 현재 루트 계정의 서브 계정이어야 합니다(예: 100000000011)|
|리소스|지정 객체 키 선택(예: `folder/sub-folder/example.jpg`)|
|작업|모든 작업|




#### 사례4: 서브 계정에 특정 디렉터리의 모든 파일에 대한 읽기/쓰기 권한 부여 및 해당 디렉터리의 지정 파일에 대한 읽기/쓰기 금지

해당 사례의 경우 **허용** 정책과 **금지** 정책, 두 가지 정책을 추가해야 합니다.

1. **허용** 정책을 추가합니다. 설정 정보는 다음과 같습니다.

|설정 항목|설정값|
|------|------|
|효과|허용|
|사용자| 서브 계정을 선택한 후 서브 계정의 UIN을 입력하고, 해당 서브 계정은 반드시 현재 루트 계정의 서브 계정이어야 합니다(예: 100000000011)|
|리소스|지정된 디렉터리의 접두사(예: `folder/sub-folder/*`)    |
|작업|모든 작업|




2. **금지** 정책을 추가합니다. 설정 정보는 다음과 같습니다.

|설정 항목|설정값|
|------|------|
|효력|거절|
|사용자| 서브 계정을 선택한 후 서브 계정의 UIN을 입력하고, 해당 서브 계정은 반드시 현재 루트 계정의 서브 계정이어야 합니다(예: 100000000011)|
|리소스|액세스를 금지할 객체 키(예: `folder/sub-folder/privateobject`)|
|작업|모든 작업|




#### 사례5: 서브 계정에 지정 접두사 파일에 대한 읽기/쓰기 권한 부여

설정 정보는 다음과 같습니다.

|설정 항목|설정값|
|------|------|
|효과|허용|
|사용자| 서브 계정을 선택한 후 서브 계정의 UIN을 입력하고, 해당 서브 계정은 반드시 현재 루트 계정의 서브 계정이어야 합니다(예: 100000000011)|
|리소스|지정 접두사(예: `folder/sub-folder/prefix`)|
|작업|모든 작업|




<span id=cam></span>

## CAM을 이용한 권한 부여 사례

계정 차원에서 권한을 부여하는 경우 다음 문서를 참조하여 설정하십시오.


- [Authorizing Sub-account Full Access to Specific Directory](https://intl.cloud.tencent.com/document/product/598/11084)
- [Authorizing Sub-account Read-only Access to Files in Specific Directory](https://intl.cloud.tencent.com/document/product/598/11085)
- [Authorizing Sub-account Read/Write Access to Specific File](https://intl.cloud.tencent.com/document/product/598/11086)
- [Authorizing Sub-account Read-only Access to COS Resources](https://intl.cloud.tencent.com/document/product/598/11087)
- [Authorizing Sub-account Read/Write Access to Specific File](https://intl.cloud.tencent.com/document/product/598/11086)
- [Authorizing Sub-account Read/Write Access to Files with Specified Prefix](https://intl.cloud.tencent.com/document/product/598/11090)
- [Authorizing Another Account Read/Write Access to Specific Files](https://www.tencentcloud.com/document/product/598/11091)

