비디오 재생 권한 제어를 지원하기 위해 Tencent Cloud VOD는 Referer를 확인하거나 Key를 생성하여 링크 도용 방지를 할 수 있는 링크 도용 방지 솔루션을 출시했습니다.
>? 링크 도용 방지 설정 후 모든 CDN 노드에 적용되는 데 약 5분이 걸립니다.

## Referer 링크 도용 방지
1. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하여 왼쪽 사이드바의 **애플리케이션 관리**를 클릭한 후 애플리케이션 목록 페이지로 이동합니다.
2. 설정할 애플리케이션 이름을 클릭하여 애플리케이션 관리 페이지로 들어갑니다.
4. 왼쪽 사이드바에서 **배포 및 재생 설정**>**도메인 관리**를 선택합니다.
5. 타깃 도메인이 있는 행에서 **설정**을 클릭하여 도메인 관련 설정 페이지로 들어갑니다.
6. **Referer 링크 도용 방지**의 오른쪽에 있는 **편집**을 클릭합니다. 링크 도용 방지 활성화 후 다음을 설정해야 합니다.
 - 빈 Referer 허용: **예** 또는 **아니오**를 선택합니다.
 - 객체 선택: **블록리스트** 또는 **얼로우리스트**을 선택하고 아래 텍스트 상자에 추가할 도메인 이름을 입력합니다.
6. **확인**을 클릭하여 설정을 저장합니다.

>?자세한 내용은 [Referer 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33985)를 참고하십시오.


## Key 링크 도용 방지
1. [VOD 콘솔](https://console.cloud.tencent.com/vod)에 로그인하여 왼쪽 사이드바의 **애플리케이션 관리**를 클릭한 후 애플리케이션 목록 페이지로 이동합니다.
2. 설정할 애플리케이션 이름을 클릭하여 애플리케이션 관리 페이지로 들어갑니다.
4. 왼쪽 사이드바에서 **배포 및 재생 설정**>**도메인 관리**를 선택합니다.
5. 타깃 도메인이 있는 행에서 **설정**을 클릭하여 도메인 관련 설정 페이지로 들어갑니다.
6. **Key 링크 도용 방지** 오른쪽에 있는 **편집**을 클릭합니다. 링크 도용 방지 활성화 후 링크 도용 방지 Key를 구성해야 합니다.
	1. **랜덤 Key 생성**을 클릭하면 시스템이 자동으로 링크 도용 방지 Key를 생성합니다.
	2. **복사**를 클릭하면 시스템이 링크 도용 방지 Key를 클립보드에 복사합니다.
7. **확인**을 클릭하여 설정을 저장합니다.

>? 
>- 자세한 내용은 [Key 링크 도용 방지](https://intl.cloud.tencent.com/document/product/266/33986)를 참고하십시오.
>- 현재 링크 도용 방지 key의 미리보기 기능은 오디오 형식 파일을 지원하지 않습니다.
