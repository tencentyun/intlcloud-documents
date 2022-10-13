키잉 기능을 사용하려면 SDK 초기화 시 키잉 모듈을 활성화해야 합니다. 자세한 내용은 [Custom Stream or Image](https://intl.cloud.tencent.com/document/product/1143/50102) 및 [Built-in Camera](https://intl.cloud.tencent.com/document/product/1143/50101)를 참고하십시오.
**이 기능은 Web SDK에서만 사용할 수 있습니다**.

[](id:set)
## 배경 설정
- SDK를 사용하면 배경을 흐리게 하거나 이미지를 배경으로 설정할 수 있습니다. 초기화 중에 키 매개변수를 전달할 수 있습니다.
```javascript
const config = {
	module: {
		beautify: true, // 스티커는 물론 뷰티 및 메이크업 효과를 제공하는 효과 모듈 활성화 여부
		segmentation: true // 배경을 변경할 수 있는 키잉 모듈 활성화 여부
	},
	auth: authData, // 인증 매개변수
	input: stream, // input 스트림
	beautify: { // 초기화를 위한 효과 매개변수(선택 사항)
		whiten: 0.1,
		dermabrasion: 0.3,
		eye: 0.2,
		chin: 0,
		lift: 0.1,
		shave: 0.2
	},
	background: {
		type: 'blur' // 배경 흐림 처리
	}
}
const sdk = new ArSdk(
	// sdk를 초기화하기 위해 config 객체를 전달합니다.
	config
)
```
- 배경을 동적으로 변경할 수도 있습니다.
```javascript
sdk.setBackground({
	type: 'image', // 배경 이미지
	src: 'https://webar-static.tencent-cloud.com/assets/background/1.jpg'
})
```

[](id:open)
## 투명 배경 사용
SDK는 일부 브라우저에서 투명한 배경을 지원합니다.
```javascript
sdk.setBackground({
	type: 'transparent'
})
```

>! 브라우저 호환성 문제 관련 다음 사항에 주의하십시오.
>- 키잉은 모바일 및 데스크톱 브라우저 모두에서 지원됩니다.
>- WebRTC는 알파 채널을 지원하지 않기 때문에 투명 배경은 로컬에서만 사용할 수 있습니다. 게시 후에는 배경 투명도가 작동하지 않습니다.
>- 배경 투명도는 데스크톱 Chrome/Firefox에서 지원되지만 데스크톱 또는 모바일 Safari에서는 지원되지 않습니다.
