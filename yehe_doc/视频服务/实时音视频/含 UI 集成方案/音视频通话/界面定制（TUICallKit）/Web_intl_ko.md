본문은 TUICallKit의 UI를 사용자 정의하는 방법을 설명하고 사용자 정의를 위한 두 가지 방식(약간의 UI 조정 및 사용자 정의 UI 구현)을 제공합니다.

## 방법1: 약간의 UI 조정

[Github](https://github.com/tencentyun/TUICallKit)의 `Web/` 폴더에 있는 UI 소스 코드를 직접 수정하여 TUICallKit의 UI를 조정할 수 있습니다.

### 아이콘 교체

`src/icons` 폴더의 아이콘을 직접 교체하여 애플리케이션에 있는 모든 아이콘의 색조와 스타일을 사용자 지정할 수 있습니다. 아이콘을 바꿀 때 파일 이름이 원래 아이콘과 동일한지 확인하십시오. 아이콘을 미리 보려면 `src/assets`로 이동하십시오.
![img](https://qcloudimg.tencent-cloud.cn/image/document/63512402ae3cee72786afcc919a988ce.png)

### UI 레이아웃 조정

src/components/ 폴더에서 UI를 수정하여 음성/영상 통화 UI를 수정할 수 있습니다.

```bash
- components/
    - Calling-C2CVideo.vue          일대일 영상 통화
    - Calling-Group.Vue             그룹 음성/영상 통화
    - ControlPanel.vue              제어판
    - ControlPanelItem.vue          제어판 항목
    - Dialing.vue                   발신 UI, 착신 UI, 일대일 음성통화 UI
    - MicrophoneIcon.vue            볼륨 레벨의 변화를 표시할 수 있는 마이크 Icon
    - TUICallKit.vue                전체 TUICallKit 컴포넌트
```

### 양식 수정

양식 파일은 `src/style.css`입니다. 원하는 UI 양식을 구현하도록 조정할 수 있습니다.

## 방법2: 사용자 정의 UI 구현

TUICallKit의 전체 호출 기능은 UI가 없는 SDK TUICallEngine을 기반으로 구현됩니다. 전적으로 TUICallEngine을 기반으로 자신만의 UI를 구현할 수 있습니다. 자세한 내용은 [API 주소](https://www.tencentcloud.com/document/product/647/51016)를 참고하십시오.