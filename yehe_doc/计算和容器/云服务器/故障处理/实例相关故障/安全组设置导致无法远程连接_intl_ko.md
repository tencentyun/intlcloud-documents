
본 문서는 CVM이 보안 그룹 설정 문제로 인해 원격 연결할 수 없는 경우의 문제 해결 및 솔루션을 소개합니다.

## 점검 툴

Tencent Cloud가 제공하는 [보안 그룹(포트) 진단 툴](https://console.cloud.tencent.com/vpc/helper)을 통해 원격 연결할 수 없는 이유가 보안 그룹 설정과 연관되어 있는지 판단할 수 있습니다.
1. [보안 그룹(포트) 진단 툴](https://console.cloud.tencent.com/vpc/helper)에 로그인합니다.
2. **인스턴스 포트 진단**페이지에서 점검이 필요한 인스턴스를 선택하고 [Quick Check]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/a792a1692e0a21b3f9dfe111d4b86789.png)
해당 인스턴스에 개방하지 않은 포트가 있는 것으로 진단한 경우, [Open all ports] 기능을 통해 서버의 상용 포트를 오픈하고 원격 로그인을 다시 시도할 수 있습니다.
<img src="https://main.qcloudimg.com/raw/a743739b5885874c15a6b5c7869f5acd.png" height="400" width="420">


## 보안 그룹 설정 수정

툴을 통해 점검한 결과, 보안 그룹 포트의 설정 문제로 확인되었으나 [원클릭 오픈] 기능을 통한 모든 CVM 상용 포트의 오픈을 원하지 않거나 원격 로그인 포트의 사용자 정의가 필요한 경우, 보안 그룹의 인바운드 및 아웃바운드 규칙을 사용자 정의로 설정하여 원격 연결할 수 없는 문제를 해결할 수도 있습니다. 자세한 작업 내용은 [보안 그룹 규칙 수정](https://intl.cloud.tencent.com/document/product/213/18197)을 참조 바랍니다.
