## 작업 시나리오
Tencent Cloud에서 제공하는 공용 이미지 외에도 동일한 구성으로 CVM 인스턴스를 만들 수 있는 사용자 정의 이미지를 만들 수도 있습니다.


<dx-alert infotype="explain" title="">
이미지는 데이터 저장을 위해 CBS 스냅샷 서비스를 사용합니다. 
 - 사용자 정의 이미지를 생성하면 해당 이미지와 연결된 스냅샷이 기본 생성됩니다. 사용자 정의 이미지 보관은 일정 스냅샷 요금이 발생합니다. 자세한 내용은 [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415)를 참고하십시오.
</dx-alert>




## 주의 사항

- 각 리전마다 최대 10개의 사용자 정의 이미지를 지원합니다.
- Linux 인스턴스에 데이터 디스크가 있지만 시스템 디스크의 사용자 정의 이미지만 만드는 경우 /etc/fstab에 데이터 디스크 구성이 포함되어 있지 않은지 확인하십시오. 그렇지 않으면 이 이미지로 생성된 인스턴스를 정상적으로 시작할 수 없습니다.
- 제작 프로세스는 10분 또는 그 이상 시간이 소요되며 구체적인 시간은 인스턴스의 데이터 크기와 연관되므로 서비스에 영향을 주지 않도록 미리 준비하십시오.
- 콘솔에서 또는 API를 통해 Cloud Physical Machine(CPM) 인스턴스를 사용하여 이미지를 생성할 수 없습니다. Cloud Virtual Machine(CVM)을 사용하여 만들 수 있습니다.
- Windows 인스턴스가 도메인에 들어가야 하고 도메인 계정을 사용해야 하는 경우, 사용자 정의 이미지 생성 전에 Sysprep 작업을 실행하여 인스턴스가 도메인에 들어간 후 SID가 고유한지 확인하십시오. 자세한 내용은 [Sysprep을 통해 CVM에 도메인을 입력하여 SID 가 고유성을 갖도록 구현](https://intl.cloud.tencent.com/document/product/213/35876)을 참고하십시오.

## 작업 단계
<dx-tabs>
::: 콘솔을 사용하여 인스턴스에서 생성

#### 인스턴스 종료(옵션)
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm)에 로그인하여 해당 인스턴스를 종료해야 하는지 확인합니다.
<dx-alert infotype="notice" title="">
2018년 7월 이후 공용 이미지를 기반으로 생성된 인스턴스(클라우드 디스크를 시스템 디스크로 사용)는 온라인 이미지 생성이 지원됩니다(즉, 인스턴스가 종료되지 않은 상황에서 이미지 생성). 이러한 인스턴스 이외의 인스턴스는 이미지와 현재 인스턴스의 배포 환경의 완벽한 일치성을 위해 먼저 인스턴스를 종료한 뒤 이미지를 생성하시기 바랍니다.
</dx-alert>
  - 필요한 경우, 단계를 계속 진행합니다.
  - 필요하지 않은 경우, [사용자 정의 이미지 생성](#createOS) 단계를 진행합니다.
2. 인스턴스의 관리 페이지에서 실제 사용된 뷰 모드에 따라 작업합니다.
  - **리스트 뷰**: 인스턴스가 위치한 행의 오른쪽에서 **더 보기** > **인스턴스 상태** > **종료**를 선택합니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/cc0bb1c82b96cca94cb7c1c011b664a7.png)
  - **탭 뷰**: 인스턴스 세부 정보 페이지에서 아래와 같이 **종료**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bd0d10a80c75a653adee564105a9820b.png)


#### 사용자 정의 이미지 생성[](id:createOS)
1. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작동합니다.
   - **리스트 뷰**: **더 보기** > **이미지 생성**을 선택합니다. 아래 이미지와 같습니다.
   ![](https://main.qcloudimg.com/raw/8e3fc28e1a0b1e9e337ff72e34a9fd01.png)
   - **탭 뷰**: 오른쪽 상단에서 **더 많은 작업** > **이미지 생성**을 선택합니다. 아래 이미지와 같습니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/27d7f6f19bc115c501bb1157ebe37cab.png)
2. ‘사용자 정의 이미지 생성’ 팝업 창에서 다음 정보를 참고하여 설정합니다.
  - **이미지 이름** 및 **이미지 설명**: 이름과 설명을 사용자 정의합니다.
  - **태그**: 리소스의 분류, 검색 및 취합을 위해 필요에 따라 태그를 추가할 수 있습니다. 자세한 내용은 [Tag](https://intl.cloud.tencent.com/document/product/651/13334)를 참고하십시오.
<dx-alert infotype="explain" title="">
시스템 디스크 및 데이터 디스크를 포함하는 사용자 지정 이미지를 생성하려면 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 활성화를 신청하십시오. 
</dx-alert>
3. **이미지 생성**을 클릭합니다.
왼쪽 사이드바에서 **[이미지](https://console.cloud.tencent.com/cvm/image)**를 클릭하면 '이미지' 페이지에서 이미지 생성 진행 상황을 볼 수 있습니다.


#### 사용자 정의 이미지를 사용하여 인스턴스 생성(옵션)
이미지 생성 후 이미지 목록에서 생성한 이미지를 선택하고 해당 이미지가 위치한 행 오른쪽의 **인스턴스 생성**을 클릭하면 기존과 동일한 이미지의 서버를 구매할 수 있습니다. 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

:::
::: \sAPI\s로 생성
CreateImage 인터페이스를 이용하여 사용자 정의 이미지를 생성할 수 있습니다. 자세한 내용은 [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276)를 참고하십시오.
:::
</dx-tabs>

## 모범 사례

### 데이터 디스크의 데이터 마이그레이션

기존 인스턴스 데이터 디스크의 데이터를 유지하면서 신규 인스턴스를 실행하고 싶다면, 데이터 디스크의 [Snapshot](https://intl.cloud.tencent.com/document/product/362/31638)을 생성한 다음, 신규 인스턴스를 실행할 때 해당 데이터 디스크의 스냅샷을 이용하여 새로운 클라우드 데이터 디스크를 생성합니다.
보다 자세한 정보는 [Creating Cloud Disks Using Snapshots](https://intl.cloud.tencent.com/document/product/362/5757)를 참고하십시오.
