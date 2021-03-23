본 문서에서는 [CSS 콘솔](https://console.cloud.tencent.com/live)을 통해 워터마크 설정을 생성하는 방법을 소개합니다. 생성 완료 후 해당 푸시 스트리밍 도메인에서 [워터마크 설정](https://intl.cloud.tencent.com/document/product/267/31064)을 연결해야 하며, 연결하고 약 5~10분 후 적용됩니다. API를 통해서도 라이브 방송 채널에 워터마크를 추가할 수 있습니다.


## 워터마크 템플릿 생성
CSS 콘솔에 로그인하여 왼쪽 메뉴바에서 [기능 템플릿]>[워터 마크 설정](https://console.cloud.tencent.com/live/config/watermark)을 선택한 후, [+] 버튼을 클릭해 워터마크 기본 정보를 설정합니다.
워터마크 위치를 선택할 수 있으며, 워터마크 이미지를 드래그하거나 X축과 Y축 방향을 조절하여 워터마크를 원하는 위치로 조정할 수 있습니다.
![](https://main.qcloudimg.com/raw/573023a1d1d6fd921209799edbfa96e8.png)

> 시각적 효과를 위해 워터마크는 투명 이미지 png 포맷을 사용하고, 이미지 크기는 2M 이하여야 합니다.

## 도메인 연결
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 푸시 스트리밍 주소를 선택하고 [관리]를 클릭해 푸시 스트리밍 주소 상세 페이지로 이동합니다.
2. [Template Configuration]을 선택하고 워터마크 설정의 편집에서 설정이 완료된 워터마크 템플릿을 선택하면 해당 도메인 주소로 지정할 수 있습니다.
![](https://main.qcloudimg.com/raw/637ec4e2692c9b1fdd06ccf336e439d8.png)
>
>- 워터마크 설정 바인딩 해제가 필요한 경우, [Template Configuration]에서 [Edit]을 클릭하여 해당 템플릿 선택을 해제한 후 [Save]을 클릭하면 해당 템플릿과 도메인 연결이 해제됩니다.
>- 콘솔의 워터마크 템플릿 관리에서는 현재 도메인 차원에서 연결 인터페이스 생성 규칙을 취소할 수 없습니다. 워터마크 관리 인터페이스를 통해 지정한 스트림과 연결하고 있는 경우, [워터마크 규칙 삭제](https://intl.cloud.tencent.com/document/product/267/30824)를 참조하여 연결을 해제해야 합니다.
