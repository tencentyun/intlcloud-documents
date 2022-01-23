VOD는 브라우저를 통해 오디오/비디오 파일을 업로드하는 시나리오를 위한 Web 업로드 SDK를 제공합니다. SDK 소스 코드가 필요한 경우 [SDK 소스 코드](https://github.com/tencentyun/vod-js-sdk-v6)를 클릭하십시오.

## 간단한 비디오 업로드

### SDK 가져오기

#### script를 사용하여 가져오기
webpack을 사용하지 않는 경우, 다음과 같은 방법으로 script 태그를 가져오기하여 사용할 수 있으며, 이 방법은 전역 변수 `TcVod`를 노출시킵니다. script를 가져오는 방법에는 다음의 두 가지가 있습니다.
- **로컬 파일 시스템으로 다운로드**
	[SDK 소스 코드](https://github.com/tencentyun/vod-js-sdk-v6)를 로컬 파일 시스템에 다운로드하고 다음 명령을 실행하여 가져옵니다.
```html
<script src="./vod-js-sdk-v6.js"></script>
```
>?src 값을 로컬에 저장한 소스 코드의 경로로 변경합니다.
- **CDN으로 가져오기**
	다음과 같은 방법을 통해 CDN으로 가져옵니다.
```html
<script src="https://cdn-go.cn/cdn/vod-js-sdk-v6/latest/vod-js-sdk-v6.js"></script>
```

script를 통해 가져온 Demo를 보려면 [여기를 클릭](https://tencentyun.github.io/vod-js-sdk-v6/)하십시오. Demo의 소스 코드는 [여기](https://github.com/tencentyun/vod-js-sdk-v6/blob/master/docs/index.html)에서 볼 수 있습니다.

#### npm 명령을 사용하여 가져오기
webpack(예: Vue 또는 React)을 사용하는 경우 npm을 사용하여 가져올 수 있습니다.
```js
// npm install vod-js-sdk-v6 실행 후 import를 실행하여 페이지에 직접 가져오기
import TcVod from 'vod-js-sdk-v6'
```

npm을 통해 가져온 Demo의 소스 코드를 보려면 [여기를 클릭](https://github.com/tencentyun/vod-js-sdk-v6/tree/master/docs/import-demo)하십시오.

>!SDK는 Promise에 의존하므로 낮은 버전의 브라우저에서 가져오기하십시오.


###  업로드 서명 가져오기 함수 정의

```js
function getSignature() {
  return axios.post(url).then(function (response) {
    return response.data.signature;
  })
};
```

>? `url`은 서명 배포 서비스의 URL입니다. 자세한 내용은 [클라이언트에서 업로드](https://intl.cloud.tencent.com/document/product/266/33921)를 참고하십시오.
> `signature` 계산 방법에 대한 자세한 내용은 [클라이언트 업로드용 서명](https://intl.cloud.tencent.com/document/product/266/33922)를 참고하십시오.

###  비디오 업로드 예시



```js
// import를 통해 가져오기하는 경우 new TcVod(opts) 실행
// script를 통해 new TcVod.default(opts)를 가져오기
const tcVod = new TcVod.default({
  getSignature: getSignature // 상기 내용에서 설명한 업로드 서명 가져오기 함수
})

const uploader = tcVod.upload({
  mediaFile: mediaFile, // File 형식의 미디어 파일(비디오, 오디오 또는 이미지)
})
uploader.on('media_progress', function(info) {
  console.log(info.percent) // 진행률
})

// 콜백 결과 설명
// type doneResult = {
//   fileId: string,
//   video: {
//     url: string
//   },
//   cover: {
//     url: string
//   }
// }
uploader.done().then(function (doneResult) {
  // deal with doneResult
}).catch(function (err) {
  // deal with error
})


```

>?
>- `new TcVod(opts)`의 opts는 [TcVod API의 매개변수](#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)를 의미하며 자세한 내용은 API 설명을 참고하십시오.
>- 업로드 방법은 파일 크기에 따라 단순 업로드 또는 멀티파트 업로드를 자동으로 선택하므로, 멀티파트 업로드의 모든 단계를 처리할 필요가 없습니다.
>- 지정된 서브 애플리케이션에 업로드하려면 [서브 애플리케이션 시스템 - 클라이언트에서 업로드](https://intl.cloud.tencent.com/document/product/266/33987)를 참고하십시오.

## 고급 기능

### 비디오와 커버 동시 업로드

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.done().then(function (doneResult) {
  // deal with doneResult
})
```

### 업로드 진행률 가져오기

SDK는 콜백 형식으로 현재 업로드 진행률 표시하기를 지원합니다.

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})
// 비디오 업로드 완료 시
uploader.on('media_upload', function(info) {
  uploaderInfo.isVideoUploadSuccess = true;
})
// 비디오 업로드 진행률
uploader.on('media_progress', function(info) {
  uploaderInfo.progress = info.percent;
})
// 커버 업로드가 완료 시
uploader.on('cover_upload', function(info) {
  uploaderInfo.isCoverUploadSuccess = true;
})
// 커버 업로드 진행률 
uploader.on('cover_progress', function(info) {
  uploaderInfo.coverProgress = info.percent;
})

uploader.done().then(function (doneResult) {
  // deal with doneResult
})
```

`xxx_upload` 및 `xxx_progress`의 콜백 값에 대한 자세한 내용은 객체 작업의 [멀티파트 업로드/복제 작업](https://intl.cloud.tencent.com/document/product/436/31538)을 참고하십시오.

### 업로드 취소

SDK는 진행 중인 비디오 또는 커버 업로드 취소를 지원합니다.

```js
const uploader = tcVod.upload({
  mediaFile: mediaFile,
  coverFile: coverFile,
})

uploader.cancel()
```

### 체크포인트 재시작

SDK는 사람의 개입이 필요 없는 자동 체크포인트 재시작을 지원합니다. 업로드가 예기치 않게 종료된 경우(브라우저 종료 또는 네트워크 연결이 끊김 등), 중단된 지점부터 파일을 다시 업로드할 수 있으므로 업로드 시간을 줄이는 데 도움이 됩니다.

## API 설명

### TcVod

| 매개변수 이름         | 필수 입력   | 유형       | 매개변수 설명      |
| ------------ | ---- | -------- | --------- |
| getSignature    | Yes    | Function     | 업로드 서명 가져오기 함수입니다.  |
| appId    | No    | number     | 이 매개변수를 입력하면 내장된 통계 리포트에 자동으로 전달됩니다.  |
| reportId    | No    | number     | 이 매개변수를 입력하면 내장된 통계 리포트에 자동으로 전달됩니다.  |

### TcVod.upload

| 매개변수 이름         | 필수 입력   | 유형       | 매개변수 설명      |
| ------------ | ---- | -------- | --------- |
| mediaFile    | No    | File     | 미디어 파일(비디오, 오디오 또는 이미지).  |
| coverFile    | No    | File     | 커버 파일.  |
| mediaName    | No    | string     | 미디어 파일의 메타데이터를 덮어쓸 파일 이름.  |
| fileId    | No    | string     | 커버가 수정될 때 전달됩니다.  |
| reportId    | No    | number     | 입력되면 이 매개변수는 기본 제공 통계 리포트에 자동으로 전달되고 생성자의 설정을 덮어씁니다.  |

### 이벤트

| 이벤트 이름         | 필수 입력   |  이벤트 설명      |
| ------------ | ---- |  --------- |
| media_upload    | No    |  미디어 파일 업로드 성공.  |
| cover_upload    | No    |  커버 업로드 성공.  |
| media_progress    | No    |  미디어 파일 업로드 진행률.  |
| cover_progress    | No    |  커버 파일 업로드 진행률.  |

## FAQ

1. **`File`객체를 얻는 방법은 무엇입니까?**
`type`이 `file`유형인 `input` 태그를 사용하여 `File` 객체를 가져옵니다.
2. **업로드된 파일은 크기 제한이 있습니까?**
최대 60GB입니다.
3. **SDK는 어떤 브라우저를 지원합니까?**
Chrome, Firefox 등 `HTML5` 및 IE 10 이상을 지원하는 기타 주요 브라우저를 지원합니다.
4. **업로드 일시 중지 또는 재개를 구현하는 방법은 무엇입니까?**
업로드 자동 재개 기능은 SDK 기본 레이어에서 구현됩니다. 일시 중지의 본질은 `uploader.cancel()` 메소드를 호출하는 것입니다. 마찬가지로 일시 중지 후 업로드 재개도 초기 `tcVod.upload` 메소드를 호출하여 수행됩니다. 차이점은 업로드가 재개될 때 이 메소드의 매개변수가 이전에 캐시된 매개변수여야 한다는 점입니다(예를 들어, 업로드가 시작될 때 전역 변수를 사용하여 매개변수를 저장하고, 업로드 완료 후 제거할 수 있습니다).

