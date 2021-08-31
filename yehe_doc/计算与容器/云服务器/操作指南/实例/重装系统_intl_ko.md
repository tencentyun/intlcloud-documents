## 작업 시나리오

시스템 재설치 작업을 통해 인스턴스를 초기 상태로 복구할 수 있습니다. 인스턴스에 시스템 장애가 발생했을 때 사용하는 중요한 복구 수단입니다.

CVM이 제공하는 두 가지 재설치 유형은 다음과 같습니다.
 - **동일한 플랫폼 재설치**: 리전에 상관없이 CVM을 동일한 플랫폼으로 재설치할 수 있습니다.
 예를 들어 Linux는 Linux로 재설치, Windows는 Windows로 재설치합니다. 
 - **다른 플랫폼 재설치**: 중국대륙 지역에서만 가능합니다(중국홍콩 제외).
 예를 들어 Linux는 Windows로, Windows는 Linux로 재설치합니다.
>? 
> - 현재 새로 추가된 모든 CBS 인스턴스 및 로컬 디스크 인스턴스는 다른 플랫폼의 시스템을 재설치할 수 있습니다. 일부 인벤토리의 20GB 로컬 디스크 인스턴스는 현재 콘솔에서 플랫폼 간 재설치가 불가하므로 로컬 디스크 인스턴스 사용자는 [티켓 제출](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM)을 통해 신청 바랍니다.
> - 스팟 인스턴스는 시스템을 재설치할 수 없습니다.

## 주의 사항
 - **재설치 준비**: 재설치 시 시스템 디스크의 콘텐츠가 손실되므로, 재설치 전에 중요한 정보를 백업해야 합니다. 시스템에서 실행되는 데이터를 보관해야 하는 경우, 시스템 재설치 전에 [사용자 정의 이미지를 생성](https://intl.cloud.tencent.com/document/product/213/4942)하고 해당 이미지를 선택하여 재설치하시기 바랍니다.
 - **이미지 선택 권장**: Tencent Cloud가 제공하는 이미지 및 사용자 정의 이미지를 사용하여 재설치할 것을 권장합니다. 출처가 불명확한 이미지나 다른 출처의 이미지를 사용하지 마시고, 시스템 디스크를 재설치할 때는 다른 작업을 진행하지 마시기를 바랍니다.
 - **인스턴스의 물리적 특성**: 인스턴스의 공인 IP는 변경할 수 없습니다.
 - **과금 관련**: 시스템 디스크의 크기를 조정할 경우(CBS만 지원), CBS의 표준 요금에 따라 요금을 청구합니다. 자세한 내용은 [디스크 가격](https://intl.cloud.tencent.com/document/product/213/2255)을 참조 바랍니다.
 - **후속 작업**: 시스템 디스크를 재설치한 후 데이터 디스크의 데이터는 보존되어 영향을 받지 않지만, 다시 마운트해야만 사용할 수 있습니다.

## 작업 순서

다음과 같은 방식을 통해 운영 체제를 재설치할 수 있습니다.
- [콘솔을 사용하여 시스템 재설치](#consoleRestart)
- [API를 사용하여 시스템 재설치](#apiRestart)

<span id="consoleRestart"></span>
### 콘솔을 사용하여 시스템 재설치

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 아래 이미지와 같이 시스템 재설치가 필요한 인스턴스 행에서 [더 보기]>[시스템 재설치]를 클릭합니다.
![시스템 재설치](https://main.qcloudimg.com/raw/cf9c32f589a0243d84d6db0b92ccad2e.png)
3. 팝업된 대화 상자에서 [확인, 재설치 시작]을 클릭합니다.
4. 현재 인스턴스가 사용 중인 이미지 또는 다른 이미지를 선택하여 디스크 크기를 조정하고, 비밀번호를 입력한 후 [재설치 시작]을 클릭합니다.
![](https://main.qcloudimg.com/raw/868508ad1ab1e1e2a60ea98d5d936a92.png)

<span id="apiRestart"></span>
### API를 사용하여 시스템 재설치

[ResetInstance API](https://intl.cloud.tencent.com/document/product/213/33242)를 참조 바랍니다.

## 후속 작업
시스템 재설치 전에 CVM이 데이터 디스크에 마운트된 상태에서 다른 플랫폼으로 재설치할 경우 다음 문서를 참조하여 기존 운영 체제의 데이터 디스크 데이터를 가져와야 합니다.
- [Linux를 Windows로 재설치한 후 기존 EXT 유형의 데이터 디스크 가져오기](https://intl.cloud.tencent.com/document/product/213/3856)
- [Windows를 Linux로 재설치한 후 기존 NTFS 유형의 데이터 디스크 가져오기](https://intl.cloud.tencent.com/document/product/213/3857)
