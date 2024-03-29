## 작업 시나리오
재시작 작업은 CVM 유지 보수에 사용되는 방식으로 인스턴스 재시작은 로컬 컴퓨터의 운영 체제를 재시작하는 것과 같습니다. 본 문서에서는 인스턴스 재시작에 대한 방식을 안내합니다.

## 주의 사항
 - **재시작 준비:** 재시작 시간 중에는 인스턴스가 정상적으로 서비스를 제공할 수 없으므로 재시작하기 전 CVM이 서비스 요청을 중단하였는지 확인하십시오.
 - **재시작 작업 방식:** 인스턴스에서 재시작 명령어를 실행하는 것이 아닌(예를 들면 Windows의 재시작 명령어 및 Linux의 Reboot 명령어), Tencent Cloud에서 제공하는 재시작 작업으로 인스턴스의 재시작을 권장합니다.
 - **재시작 시간:** 일반적으로 재시작 작업은 몇 분 정도 소요됩니다.
 - **인스턴스 물리적 특성:** 인스턴스 재시작은 인스턴스의 물리적 특성을 변경하지 않습니다. 인스턴스의 공인 IP, 개인 IP 및 스토리지의 어떤 데이터도 변경하지 않습니다.
 - **과금 관련:** 인스턴스를 재시작해도 새 인스턴스에 대한 과금이 시작되지 않습니다.

## 작업 단계
사용자는 다음과 같은 방식을 통해 인스턴스를 재시작할 수 있습니다.
<dx-tabs>
::: 콘솔을 통한 인스턴스 재시작

#### 단일 인스턴스 재시작
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 인스턴스의 관리 페이지에서 실제 사용된 뷰 모드에 따라 작업합니다.
  - **리스트 뷰**: 아래 이미지와 같이 재시작할 행에서 **더보기** > **인스턴스 상태** > **재시작**을 선택합니다.
 ![단일 인스턴스 재시작](https://qcloudimg.tencent-cloud.cn/raw/fa35600ee1e53b77d9f0abafbef162bc.png)
  - **탭 뷰**: 아래 이미지와 같이 재시작할 인스턴스 페이지에서 오른쪽 상단의 **재시작**을 선택합니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/d5384873a89471914f97df0b22230d7a.png)


#### 다수의 인스턴스 재시작
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 아래 이미지와 같이 재시작할 인스턴스를 선택하고 리스트 상단의 **재시작**을 클릭하면 일괄 재시작할 수 있으며, 재시작할 수 없는 경우 원인이 표시됩니다.
![다수의 인스턴스 재시작](https://qcloudimg.tencent-cloud.cn/raw/c887966def1c1d83e837ae18b855d45f.png)
<dx-alert infotype="explain" title="">
단일 인스턴스는 다음 방식으로 재시작할 수 있습니다.
</dx-alert>


:::
::: \sAPI\s를 사용하여 인스턴스 재시작
[RebootInstances 인터페이스](https://intl.cloud.tencent.com/zh/document/product/213/33243)를 참고하십시오.
:::
</dx-tabs>
