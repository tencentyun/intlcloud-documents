## 소개
본문은 다음 문제를 빠르게 해결할 수 있는 두 가지 인증 방법을 소개하며, 자세한 작업 단계는 다음과 같습니다. 보다 복잡한 권한 설정 정책은 [CAM > 사용자 정의 정책](https://intl.cloud.tencent.com/document/product/1047/38088)을 참고하십시오.
- 서브 계정이 IM 서비스를 사용하는 경우, 루트 계정에서 [콘솔 액세스](https://console.cloud.tencent.com/im) 및 설정 작업 수행 권한을 부여해야 하며, 그렇지 않은 경우 다음과 같이 콘솔 애플리케이션 목록 표시가 불가능합니다.
![](https://main.qcloudimg.com/raw/0a28018859d63fc6822457021fc1e023.png)
- 서브 계정에 태그 액세스 권한이 있지만, 콘솔 애플리케이션 태그와 서브 계정 태그 권한이 부합하지 않을 경우, 서브 계정은 신규 애플리케이션을 조회 또는 생성할 수 없습니다.


## 방법1. 전체 권한 부여 작업 단계
### 1단계: 권한 부여
루트 계정으로 콘솔 [**CAM**](https://console.cloud.tencent.com/cam) >사용자 목록으로 이동한 후, 서브 계정 좌측의 **권한 부여**를 클릭하면 ‘정책 연결’ 선택창이 팝업됩니다.
![](https://main.qcloudimg.com/raw/9a87638c3298b3e50307e82186eb17ea.png) 

### 2단계: 정책 선택
정책 필터에서 ‘instant messaging’을 검색하고, 권한 부여가 필요한 옵션을 선택한 다음, **확인**을 클릭하여 완료합니다.
![](https://main.qcloudimg.com/raw/9a4b20af40d5800db94c058f6a492175.png)

>?
>- **읽기 및 쓰기 액세스**: 콘솔 액세스 및 설정 변경 가능.
>- **읽기 전용 액세스**: 콘솔 액세스만 가능하며, 다른 작업은 불가능.
### 3단계: 권한 부여 완료
오른쪽 모서리 상단에 ‘정책 연결 완료’ 메시지가 표시되면 연결 작업이 완료된 것입니다.
![](https://main.qcloudimg.com/raw/7c2812137b4afc10dcf3de7072a90761.png)


## 방법2: 태그별 권한 부여 작업 단계
이 방법은 태그 권한 부여를 통해 서브 계정을 관리해야 하는 고객에게 적합하며, 서브 계정은 권한 부여 태그 하위 애플리케이션만 액세스 및 작업할 수 있습니다.
>!
>- 서브 계정에 태그 정책을 적용한 후, 서브 계정은 태그가 비어 있는 애플리케이션을 액세스 또는 작업할 수 없습니다. 서브 계정이 [IM 콘솔](https://console.cloud.tencent.com/im)에서 새로 생성한 애플리케이션은 태그가 비어 있으므로, 루트 계정으로 해당 애플리케이션 태그를 승인 태그로 변경해야 서브 계정이 사용할 수 있습니다.
>- 기존 애플리케이션을 태그별로 서브 계정에 권한 부여하는 경우, 권한 부여하려는 애플리케이션에 해당 태그가 설정되어 있는지 확인하십시오. 그렇지 않으면 태그를 통해 권한 부여할 수 없습니다. 
>- 애플리케이션에 태그가 설정되어 있지 않은 경우, IM 콘솔의 [기본 설정](https://console.cloud.tencent.com/im-detail) 페이지에서 설정합니다. 자세한 내용은 [태그 설정](https://intl.cloud.tencent.com/document/product/1047/34540)을 참고하십시오. 

>- 또는 [태그 리스트](https://console.cloud.tencent.com/tag/taglist)로 이동하여 애플리케이션을 태그에 일괄 바인딩합니다. 자세한 내용은[리소스 바인딩](https://intl.cloud.tencent.com/document/product/651/41575)을 참고하십시오.

### 1단계: 권한 부여
루트 계정으로 콘솔 [**CAM**](https://console.cloud.tencent.com/cam) >**정책**에 진입한 후, 상단의 **사용자 정의 생성**을 클릭하면, ‘정책 생성 방식 선택’ 팝업창이 나타납니다.
![](https://main.qcloudimg.com/raw/289a2def35370b7511625b37f3e798b3.png)

### 2단계: 태그 선택
‘태그별 권한 부여’를 선택하여 ‘태그 정책 생성기’로 이동합니다.
![](https://main.qcloudimg.com/raw/02098a1da180deae9c810b97cb0c453c.png)

### 3단계: 정책 생성
‘태그 정책 생성기’에서 권한이 필요한 서브 계정, 태그 등의 정보를 입력하고 **다음**을 클릭하여 확인 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/e590a9843e852bf9eca22bfc95ffbc13.png)

>?태그 선택 목록이 비어 있는 경우, 먼저 루트 계정으로 [태그 콘솔](https://console.cloud.tencent.com/tag/taglist)로 이동하여 태그를 생성합니다.
>![](https://main.qcloudimg.com/raw/e6d0aeb3a04b9281627805f0cde3d052.png)

### 4단계: 인증 완료
오류가 없는지 확인하고 **완료**를 클릭하여 태그 권한 부여 프로세스를 종료합니다.
![](https://main.qcloudimg.com/raw/3c9e2624f334f9c9820402f579381ae6.png)