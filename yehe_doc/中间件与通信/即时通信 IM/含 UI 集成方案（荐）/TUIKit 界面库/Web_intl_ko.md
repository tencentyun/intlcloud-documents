# Web

## chat-uikit-react 소개
chat-uikit-react는 Tencent Cloud IM SDK를 기반으로 하는 UI 컴포넌트 라이브러리로, 세션, 채팅, 관계 체인, 그룹, 음성/영상 통화 등의 기능을 포함한 일부 범용 UI 컴포넌트를 제공합니다.
UI 컴포넌트를 기반으로 블록을 쌓는 것처럼 자신의 비즈니스 로직을 빠르게 구축할 수 있습니다.
chat-uikit-react의 컴포넌트는 UI 기능을 구현하는 동시에 IM SDK에 해당하는 인터페이스를 호출하여 IM 관련 로직과 데이터를 처리하므로 개발자는 UIKit을 사용할 때 자신의 업무에만 집중하거나 필요에 따라 확장할 수 있습니다.

## chat-uikit-react 구성
chat-uikit-react는 크게 TUIKit, TUIConversation, TUIChat, TUIManage와 같은 몇 가지 주요 모듈로 구성되며 각 모듈은 서로 다른 콘텐츠를 담당합니다.

## TUIKit 기능 소개
TUIKit은 Context를 통해 tim, conversation, profile 등의 여러 콘텐츠를 제공하는 최외부 Provider입니다. 자세한 내용은 [오픈 소스 코드](!https://github.com/TencentCloud/chat-uikit-react)를 참고하십시오.

## TUIConversation 기능 소개
TUIConversation은 대화를 상단에 고정하고 대화를 삭제하는 것과 같은 기능을 포함하여 대화 목록의 표시 및 편집을 주로 담당합니다.

## TUIChat 기능 소개
TUIChat은 메시지 전송, 메시지 회수 및 메시지 포워딩과 같은 기능을 포함하여 대화 메시지의 표시 및 편집을 주로 담당합니다.

## TUIManage 기능 소개
TUIManage는 주로 대화 관련 정보 표시 및 대화를 상단에 고정하고 대화를 삭제하는 것과 같은 작업을 담당합니다.
