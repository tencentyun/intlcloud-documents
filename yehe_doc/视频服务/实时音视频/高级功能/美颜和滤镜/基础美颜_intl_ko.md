TRTC는 뷰티 필터 기능과 뷰티 플러그 인의 통합을 제공하며, 뷰티 필터 또는 플러그 인을 통해 자연스러운 뷰티 효과를 얻을 수 있습니다.

## 뷰티 필터 활성화
[클릭](https://web.sdk.qcloud.com/trtc/webrtc/test/latest/beauty/index.html)하면 Web 뷰티 필터 효과를 경험하실 수 있습니다.

## 전제 조건
Web 플랫폼 뷰티 필터 플러그 인은 다음 브라우저를 지원합니다.
<table>
<tr><th>브라우저</th><th>버전</th></tr>
<tr>
<td>Chrome</td><td>65+</td>
</tr><tr>
<td>Firefox</td><td>70+</td>
</tr><tr>
<td>Safari</td><td>12+</td>
</tr><tr>
<td>Edge</td><td>80+</td>
</tr><tr>
<td>모바일 브라우저</td><td>미지원</td>
</tr><tr>
<td>WeChat 내장 웹페이지</td><td>미지원</td>
</tr></table>

'RTCBeautyPlugin' 사용 시 TRTC Web SDK를 4.11.1 또는 이후 버전으로 업그레이드 하시기 바랍니다.
프로젝트에 [RTCBeautyPlugin](https://www.npmjs.com/package/rtc-beauty-plugin)을 설치합니다.
```shell
npm install rtc-beauty-plugin
```

## 통합 설명
### 1단계: RTCBeautyPlugin 인스턴스 생성

RTCBeautyPlugin의 인스턴스는 로컬 오디오 및 비디오 스트림을 처리하는 데만 사용할 수 있습니다.

```javascript
const beautyPlugin = new RTCBeautyPlugin();

// 뷰티 필터 플러그 인의 뷰티 레벨 조정( 0 - 1 )
beautyPlugin.setBeautyParam({ beauty: 0.5, brightness: 0.5, ruddy: 0.5 });
```

### 2단계: RTCBeautyPlugin 인스턴스를 사용하여 게시해야 하는 스트림 처리

```javascript
// 뷰티 필터 생성 후의 스트림
const beautyStream = beautyPlugin.generateBeautyStream(localStream);

// 뷰티 필터 후 스트림 게시
await client.publish(beautyStream);
```

### 3단계: 통화 종료 후 뷰티 필터 플러그 인 삭제

통화가 끝나면 메모리 사용 및 성능 소모를 방지하기 위해 뷰티 필터 플러그 인을 삭제할 수 있습니다.

```javascript
// 통화 종료
await client.leave();

// 플러그 인을 폐기하고 메모리를 해제합니다.
beautyPlugin.destory();
```

## 주의 사항
1. `RTCBeautyPlugin`의 인스턴스는 하나의 로컬 스트림만 처리할 수 있습니다.
2. 'replaceTrack' 및 기타 작업을 사용하면 'localStream' 뷰티 필터 효과가 사라지므로 적절하게 사용하시기 바랍니다.


