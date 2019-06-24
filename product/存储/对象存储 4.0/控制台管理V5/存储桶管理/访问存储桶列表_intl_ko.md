## 소개

**서브 계정**은 기본으로 버킷 리스트 풀링 권한이 없으므로 서브 계정을 사용하여 [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하며 버킷 리스트에서 버킷 및 해당 리스트와 통계 데이터에 접근할 수 없습니다. 다음 그림과 같습니다.

**버킷 리스트 접근 제한 예시**:
![6](https://main.qcloudimg.com/raw/a6ccdd6c2929e106811ea7b9743dbb20.png)
**통계 데이터 접근 제한 예시**:
![7](https://main.qcloudimg.com/raw/6d625ef08355eb7a69528d3a4367ab35.png)

**서브 계정**은 **접근 경로 추가**의 방식을 통해 버킷에 접근하거나 서브 계정에 **사전 정의 정책 QcloudCOSGetServiceAccess 추가(즉, 버킷 리스트 접근 권한 획득)**의 방식으로 버킷 리스트에 접근해야 합니다.

>! 이 기능은 서브 계정을 통해 콘솔에 로그인하여 버킷에 접근하는 시나리오에 적용합니다.

## 접근 경로 추가

기본 상황에서 서브 계정은 사전 정의 정책(QcloudCOSGetServiceAccess)을 부여받지 않으며 이 때 서브 계정은 버킷 리스트 풀링 권한이 없습니다. 단, 루트 계정이 서브 계정에 어느 버킷의 사용자 권한(예: 데이터 읽기, 데이터 쓰기 등 사용자 권한)을 부여한 후 서브 계정은 **접근 경로 추가**의 방식을 통해 해당하는 버킷에 접근할 수 있습니다.

### 작업 절차

1. **서브 계정**을 사용하여 COS 콘솔에 로그인하여 [접근 경로 리스트](https://console.cloud.tencent.com/cos5/access_path) 탐색 모음을 한번 클릭한 후, [접근 경로 추가]를 한번 클릭하십시오.
![](https://main.qcloudimg.com/raw/1aaa66cc85e7e7ffeccd0311d026add5.png)
2. **접근 경로 추가** 팝업창에서 버킷 소재 지역을 선택하고 접근 경로를 입력합니다. 구성 설명은 다음과 같습니다.
**지역**: 접근 허용 권한을 부여받은 버킷에 해당하는 지역을 선택합니다.
**접근 경로**: 접근 허용 권한을 부여받은 버킷의 이름(예: examplebucket-1250000000)을 입력합니다. 또한, 객체의 버킷 중의 경로를 입력할 수 있습니다. 예: `examplebucket-1250000000/exampleobject.txt`.
![](https://main.qcloudimg.com/raw/5d49b946e32099852f8493630476cad5.png)

3. 지역과 접근 경로가 정확한지 확인한 후, [확인] 버튼을 한번 클릭하면 권한을 부여받은 버킷 또는 버킷 중의 객체 경로를 추가할 수 있습니다.
![](https://main.qcloudimg.com/raw/07d93e0ab51fbfb51942db2658a6c79e.png)


## 사전 정의 정책 추가
서브 계정에 **사전 정의 정책 QcloudCOSGetServiceAccess 추가(즉, 버킷 리스트 접근 권한 획득)**의 방식으로 버킷 리스트에 접근합니다.

> !
>- 사전 정의 정책 QcloudCOSFullAccess 또는 QcloudCOSReadOnlyAccess는 모두 서브 계정에 버킷 리스트 접근 권한을 부여할 수 있습니다. 그러나, 이 두 정책이 부여하는 권한 범위가 넓기 때문에 **보안성을 고려하여, 사용을 권장하지 않습니다**.
>- 개요의 통계 데이터는 버킷 리스트의 접근 권한에 의존합니다. 서브 계정이 통계 데이터를 풀링해야 할 경우, 루트 계정이 이미 서브 계정에 사전 정의 정책[QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2)을 추가했는지 확인하십시오. 그렇지 않으면 통계 데이터에 접근 권한이 없음을 알립니다.

### 작업 절차

1. 루트 계정을 사용하여 [CAM 콘솔](https://console.cloud.tencent.com/cam)에 로그인하고 생성된 서브 계정을 한번 클릭하십시오.
![](https://main.qcloudimg.com/raw/e849caa03da1b7da2c82976dcbe46f00.png)
2. [연결 정책]을 한번 클릭하여 정책 리스트에서 사전 정의 정책 [QcloudCOSGetServiceAccess](https://console.cloud.tencent.com/cam/policy/detail/2158379&QcloudCOSGetServiceAccess&2)(즉, COS 의 버킷 리스트 접근 권한)을 추가하고 [확인]을 한번 클릭하여 연결 정책을 완료합니다.
![](https://main.qcloudimg.com/raw/3701e6420ded77172a8b0b8ddb3acf53.png)
3. 여기서 이미 추가된 정책을 조회할 수 있습니다. 이 정책을 사용할 필요가 없을 경우, 언바인딩 작업을 진행할 수 있습니다.
![](https://main.qcloudimg.com/raw/da06a4a46a9606e2168d9411861fe843.png)
