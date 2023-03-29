## 응용 시나리오
App이 백그라운드에서 종료되거나 프로세스가 중단된 경우에도 오프라인 푸시 기능을 사용하여 사용자에게 새 메시지를 알릴 수 있으며, iOS 디바이스는 APNs를 사용하여 오프라인 푸시하며, Android 디바이스는 사용자가 오프라인 메시지 콜백을 등록해야 합니다.

## iOS APNs 푸시
### 푸시 형식

![](https://main.qcloudimg.com/raw/8bb11ef0a0ff210c1b0a1ab65da63c2f.png)


상기 이미지는 1:1 채팅과 그룹 채팅의 예시입니다.
iOS APNs 푸시 형식에 대한 자세한 설명은 [푸시 형식](https://intl.cloud.tencent.com/document/product/1047/34347)을 참고하십시오.

### 기본 인터페이스
APNs를 지원하려면 다음 인터페이스를 호출하여야 합니다. 자세한 사항은 [iOS APNs 이벤트 리포트](https://intl.cloud.tencent.com/document/product/1047/34347)를 참고하십시오.
- Token 설정.
- 백그라운드로 전환하여 읽지 않은 메시지 리포트.
- 포그라운드와 푸시 알림으로 전환.

### Ext 확장 설정
리디렉션 클릭 등의 사용자 작업을 용이하게 하기 위해 애플리케이션 푸시용 Ext 확장 필드를 설정해야할 경우, TIMCustomElem의 Ext 필드에 입력할 수 있으며, 푸시하는 동안 IM 백엔드가 필드를 Ext에 입력합니다. 확장 필드의 사용자 정의 작업은 [사용자 정의 오프라인 메시지 속성](https://intl.cloud.tencent.com/document/product/1047/34347)을 참고하십시오.

### 푸시 알림음 설정
사용자에게 특정 메시지에 대한 특별 알림을 진행하기 위해, 애플리케이션 메시지 푸시 사운드를 개별 설정해야할 경우, 오디오를 TIMCustomElem의 sound 필드에 입력할 수 있으며, 푸시하는 동안 IM 백엔드가 필드를 Ext에 입력합니다. [사용자 정의 푸시 알림음 설정](https://intl.cloud.tencent.com/document/product/1047/34347)을 참고하십시오.

## Android 오프라인 푸시
Android는 1.8.0 이후 버전은 프로세스에서 서비스 분리를 지원합니다. App 프로세스가 중단되어도 서비스는 유지되며, 오프라인 푸시를 받아볼 수 있습니다. 관련 설정 및 구성에 대한 자세한 내용은 [오프라인 푸시 설정](https://intl.cloud.tencent.com/document/product/1047/34336)을 참고하십시오.

## 백엔드에서 메시지 보내기
iOS의 경우 [푸시 형식](https://intl.cloud.tencent.com/document/product/1047/34347)을 참고하여 APNs 푸시 표시 형식을 설정할 수 있으며, Android의 경우 [OfflinePushInfo](https://intl.cloud.tencent.com/document/product/1047/33527)를 참고하여 설정할 수 있습니다.

## 관련 문서
- [오프라인 푸시 인증서 관리](https://intl.cloud.tencent.com/document/product/1047/34540)
- [Apple 푸시 인증서 신청](https://intl.cloud.tencent.com/document/product/1047/34346)
- [iOS 오프라인 푸시 설정](https://intl.cloud.tencent.com/document/product/1047/34347)
- [Android 오프라인 푸시 기본 설정](https://intl.cloud.tencent.com/document/product/1047/34336)
