본문은 Tencent Effect Web SDK를 사용할 때 발생할 수 있는 질문에 대한 답변입니다.

[](id:q1)
### Chrome으로 Demo 프로젝트를 실행할 때 동영상이 뒤집히고 끊기면 어떻게 해야 합니까?
SDK는 GPU 가속을 사용합니다. 브라우저 설정에서 **하드웨어 가속**을 활성화해야 합니다.

[](id:q2)
### Web 스트리밍 애플리케이션이 있습니다. Tencent Effect Web SDK를 사용하여 애플리케이션으로 게시한 이미지를 아름답게 꾸밀 수 있습니까?
예, SDK를 렌더로 사용할 수 있습니다. 다양한 입력 및 출력 유형을 지원합니다.

[](id:q3)
### 서명 서비스가 자주 호출되지는 않습니까?
그렇지 않습니다. SDK에는 서명 캐시 메커니즘이 있습니다. `getSignature`에 대한 고유한 응답 로직을 설계할 수도 있습니다. 메소드 서명 규칙을 준수하는지 확인하십시오.

[](id:q4)
### 내가 콘솔에서 만든 사용자 지정 효과는 SDK에서 적용한 실제 효과와 다릅니까?
그렇지 않습니다. SDK에서 제공하는 실제 렌더링 효과는 콘솔에서 미리 볼 때와 동일합니다.

[](id:q5)
### 데모 프로젝트의 예시는 로컬에서 프로젝트를 실행하기 위해 localhost:8090을 사용합니다. 다른 localhost 포트를 사용할 수 있습니까?

사용할 수 있습니다. 콘솔의 Web License 관리 페이지에서 License의 Domain을 사용하려는 도메인과 포트로 설정하고 `package.json` 파일에서 `dev` 명령의 포트 번호를 수정합니다.
예를 들어 `localhost:9999`를 사용하여 데모 프로젝트를 실행하려면 Domain을 `localhost:9999`로 설정합니다.

[](id:q6)
### LEB 퍼블리싱에 실패했습니다. 브라우저 console을 열었을 때 ‘streamurl authentication failed’ 메시지가 표시되었습니다. 어떻게 해야 합니까?
이 문제는 일반적으로 서명이 만료되었기 때문입니다. 게시를 위해 새 서명을 생성하십시오. 게시 URL 형식에 대한 자세한 내용은 [라이브 스트리밍 URL 스플라이싱](https://intl.cloud.tencent.com/document/product/267/38393)을 참고하십시오.

[](id:q7)
### 효과를 쿼리하기 위해 getEffectList 를 호출할 때 오류가 발생했습니다. 어떻게 해야 합니까?
일반적으로 적시에 API를 호출하지 않았기 때문일 수 있습니다. **`getEffectList`는 `created` 콜백 후에 호출해야 합니다**.

[](id:q8)
### Web 페이지에서 SDK의 내장 카메라 모드를 사용했습니다. 효과를 미리보기할 때 에코가 들렸습니다. 어떻게 해야 하나요?
효과를 미리보기할 때 오디오를 활성화하고 스피커를 사용하면 스피커에서 재생되는 오디오가 내장 카메라에 캡처되어 에코가 발생합니다. 이 문제를 해결하려면 효과를 미리보기 할 때 오디오를 비활성화하십시오.
```
const output = await sdk.getOutput()
const video = document.createElement('video')
document.body.appendChild(video)

video.setAttribute('muted', '')
video.volume = 0
video.srcObject = output
```

[](id:q9)
### 인증에 실패하여 코드 401이 반환되었습니다. 어떻게 해야 합니까?
SDK는 통과 매개변수와 함께 `getSignature`를 사용하여 서명을 요청하고 백엔드에서 서명을 인증합니다. 서명이 만료된 경우 다시 시도합니다. 인증이 다시 실패하면 오류가 발생하고 모든 후속 작업이 금지됩니다. getSignature 로직을 확인하십시오. 서명이 만료되지 않았는지(5분 동안 유효) 올바른 서명 생성 로직이 사용되었는지 확인하십시오.