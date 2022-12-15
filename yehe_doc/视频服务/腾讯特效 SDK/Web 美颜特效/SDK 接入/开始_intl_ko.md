[Tencent Effect Web SDK](https://www.tencentcloud.com/document/product/1143/51226)를 사용하면 Tencent Effect 기능을 프로젝트에 빠르고 안전하게 통합할 수 있습니다.

## 워크플로
**Tencent Effect web SDK**는 간단하고 최소 침습적인 API를 제공합니다. 인스턴스를 통합하고 해당 기능을 사용하려면 인스턴스를 초기화하고 웹 페이지에 렌더링 노드를 추가하기만 하면 됩니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a691e17a2a028c9fa00a92f37091465b.jpg" style="zoom:50%;" />

## 설치
Tencent Effect Web SDK는 npm 패키지로 제공됩니다.
```
npm install tencentcloud-webar
```

## SDK 액세스

- Web SDK를 위한 내장 Camera와 사용자 지정 스트림의 두 가지 초기화 모드를 제공합니다.
	- [내장 카메라](https://intl.cloud.tencent.com/document/product/1143/50101): 기기에 내장된 카메라 및 플레이어를 사용합니다. API 호출은 풍부한 대화형 기능으로 쉽고 빠릅니다.
	- [사용자 정의 스트림 및 이미지](https://intl.cloud.tencent.com/document/product/1143/50102): 자신의 스트림에 효과를 적용하거나 더 큰 유연성과 제어를 원하는 경우 이 모드를 사용할 수 있습니다.

## 필터 및 효과 구성
[필터 및 효과 구성](https://intl.cloud.tencent.com/document/product/1143/50104)을 참고하십시오.

## 키잉(v0.2.0의 새로운 기능)
키잉 기능을 사용하면 배경을 변경할 수 있습니다. Web SDK에서만 사용할 수 있습니다. 자세한 내용은 [키잉 구성](https://intl.cloud.tencent.com/document/product/1143/50105)을 참고하십시오.

## 3D 효과(v0.3.0의 새로운 기능)
다른 효과를 구성하는 것과 같은 방식으로 3D 효과를 구성할 수 있습니다. 자세한 내용은 [필터 및 효과 구성](https://www.tencentcloud.com/document/product/1143/50104)을 참고하십시오.

## Animoji 및 가상 아바타(v0.3.0의 새로운 기능)
이 기능은 WebGL2 환경에 의존합니다. 자세한 내용은 [Animoji 및 가상 아바타 사용](https://www.tencentcloud.com/document/product/1143/51231)을 참고하십시오.


## 매개변수 및 API
[매개변수 및 API](https://intl.cloud.tencent.com/document/product/1143/50106)를 참고하십시오.

## 호환성 처리

| 브라우저   | 플랫폼 |
| -----   | --- |
| Chrome  | 데스크톱, Android, iOS |
| Safari  | 데스크톱, iOS |
| FireFox | 데스크톱, Android, iOS |
| QQ webview | Android |
| WeChat webview | Android/iOS (WeChat 8.0.16 이상)|


>? **SDK 0.2.1에 하드웨어 가속 테스트 지원이 추가되었습니다.**
Tencent Effect Web SDK는 부드러운 렌더링을 위해 하드웨어 가속에 의존합니다. SDK를 사용하면 브라우저가 하드웨어 가속을 지원하는지 확인할 수 있습니다. 하드웨어 가속을 지원하지 않는 브라우저는 차단할 수 있습니다.
```javascript
import {ArSdk, isWebGLSupported} from 'tencentcloud-webar'

if(isWebGLSupported()) {
	const sdk = new ArSdk({
		...
	})
} else {
	// 브라우저 차단 로직
}
```


## 코드 예시
[데모 프로젝트 실행](https://cloud.tencent.com/document/product/616/71371)을 참고하십시오.
