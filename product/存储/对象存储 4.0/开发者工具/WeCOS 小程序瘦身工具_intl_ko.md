## 기능 설명
미니 프로그램 체험의 유창성을 높이기 위해, 위챗은 컴파일된 코드 패키지의 크기를 최대 1MB까지 제한합니다. 1MB보다 큰 코드 패키지는 업로드에 실패될 것입니다. 실제로 미니 프로그램을 개발하는 과정에서 이미지 리소스는 상대적으로 큰 공간을 차지하여 공식적인 1MB 제한 요구를 초과하기 쉽습니다.

COS의 WeCOS 도구를 사용하면 미니 프로그램의 항목에 있는 이미지 리소스는 자동으로 COS에 업로드되며 WeCOS는 코드에서 이미지 리소스 주소의 인용을 온라인 주소로 자동으로 교체하여 프로젝트 디렉터리에 있는 이미지 리소스를 제거함으로써 코드 패키지 크기를 줄입니다.

WeCOS의 사용에 관련된 준비 작업과 설치 조작 등 구성에 대해 설명합니다.
## 준비 작업
1. [Tencent Cloud 홈페이지](https://cloud.tencent.com/)에 들어가서 Tencent Cloud 계정을 등록합니다. 자세한 내용은 [Tencent Cloud 등록](/doc/product/378/9603) 페이지를 참조하십시오.
2. [COS 콘솔](https://console.cloud.tencent.com/cos4)에 로그인하여 COS 서비스를 활성화하며 [버킷 생성](/doc/product/436/6232)
3. GitHub에서 [WeCOS 도구 획득](https://github.com/tencentyun/wecos)
4. [Node.js 홈페이지](https://nodejs.org/)에서 환경을 다운로드하여 설치합니다.

## 설치 시작
다음 명령을 사용하여 WeCOS 도구를 설치합니다.

```js
npm install -g wecos
```

## 기본 구성
미니 프로그램 디렉터리 동급에서 `wecos.config.json` 파일을 생성하십시오. 파일 구성의 예시는 다음과 같습니다.

```json
{
  "appDir": "./app",
  "cos": {
    "secret_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "secret_key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "bucket": "wxapp-1251902136",
    "region": "ap-guangzhou",
    "folder": "/"
  }
}
```

region: 버킷 생성 시 선택한 지역 약칭입니다.
folder: 리소스는 버킷의 어느 디렉터리에 저장되어 있습니다.

### 구성 항목 설명

| 구성 항목    | 유형           | 설명                                       |
| ------ | ------------ | ---------------------------------------- |
| appDir | String | 기본 `./app`, 미니 프로그램 프로젝트 디렉터리                       |
| cos    | Object | 필수. COS의 버킷, 지역 등 구성 정보는 [버킷 개요](https://cloud.tencent.com/document/product/436/13312) 파일을 참조하십시오. 키 관련 정보는 [클라우드 API 키 콘솔](https://console.cloud.tencent.com/cos4/secret)을 참조하십시오 |


## 시작하기
구성 파일의 동급 디렉터리에서 다음과 같은 사용 명령을 실행합니다.
```
wecos
```

>!명령 실행 전 구성 파일의 동급 디렉터리에서 `wecos.config.json` 파일을 생성해야 합니다.

## 고급 구성

| 구성 항목                 | 유형            | 설명                                      |
| ------------------- | ------------- | --------------------------------------- |
| backupDir           | String  | 기본 `./wecos_backup`, 디렉터리 백업                |
| uploadFileSuffix    | Array  |  기본 `[".jpg", ".png", ".gif"]`, 이미지 업로드 후 접미사 구성  |
| uploadFileBlackList |Array |  기본 `[]`, 이미지 리소스 블랙리스트    |
| replaceHost         | String  |  기본 `''`, 지정 도메인 이름을 targetHost로 교체   |
| targetHost          | String | 기본 `''`, 사용자 지정 도메인 이름 사용    |
| compress            | Boolean |  기본 `false`, 이미지 압축을 시동 여부       |
| watch               | Boolean | 기본 `true`, 항목 디렉터리의 실시간 모니터링 시동 여부   |

#### 백업 디렉터리 설정
WeCOS 실행 시 자동으로 항목 아래의 이미지를 COS로 업로드하여 삭제하므로 소스 파일을 분실할 위험이 있습니다. 따라서 소스 파일 백업 기능을 제공합니다. 이미지 업로드 시 자동으로 항목 동급의 디렉터리 아래에 해당 파일을 백업합니다. 다음을 통해 백업 경로를 수정할 수 있으며 이 기능을 사용할 필요가 없는 경우 빈 값으로 설정하면 됩니다.
```
  "backupDir": "./wecos_backup"
```
#### 이미지 접미사 설정
업로드할 이미지의 포맷(예를 들어 `jpg` 포맷만 허용됨)을 제한해야 할 경우 WeCOS에서 제공하는 이미지 접미사 구성 항목을 통해 정의할 수 있습니다. WeCOS는 기본적으로 jpg, png, gif의 세 가지 포맷을 지원합니다. 다른 포맷(예: webp)을 추가해야 한다면 해당 구성 항목에서 추가할 수 있습니다. 예를 들면 다음과 같습니다.

```
  "uploadFileSuffix": [".jpg",".png",".gif",".webp"]
```

#### 이미지 블랙리스트 설정
개발 과정 중에 특정 이미지를 업로드하는 것을 원하지 않는 경우 WeCOS 블랙리스트를 통해 구현할 수 있으며 구성 후 업로드 프로그램은 자동으로 해당 이미지를 무시합니다. 블랙리스트는 디렉터리 또는 파일 이름까지의 쓰기를 지원합니다.

```
  "uploadFileBlackList": ["./images/logo.png","./logo/"]
```

#### 사용자 지정 도메인 이름
COS 파일 링크가 개인 도메인 이름을 사용하기를 원할 경우 targetHost 구성으로 기본 도메인 이름(구성 시 `http://` 생략 가능)을 교체할 수 있습니다.

```
  "targetHost": "http://example.com"
```

코드에 있는 이미지 링크를 위해 도메인 이름을 교체할 경우 replaceHost targetHost 구성으로 구현할 수 있습니다.

```
  "replaceHost": "http://wx-12345678.myqcloud.com",
  "targetHost": "https://example.com"
```

#### 이미지 압축 시동
이미지가 COS에 업로드된 후 프로그램 패키지의 크기를 크게 줄였지만 이미지 자체 크기로 접근이 지연될 경우 사용자 체험에 영향을 미칠 수 있습니다.
WeCOS는 이미지가 클라우드로 전환하는 기능에 [Tencent Cloud Infinite](https://cloud.tencent.com/product/ci)에 기반한 이미지 압축 기능을 추가로 제공합니다. [Tencent Cloud Infinite 콘솔](https://console.cloud.tencent.com/ci)에서 COS와 같은 이름의 버킷을 생성한 후 버킷에 들어가 양식 페이지에서 이미지 압축 기능을 시동하면 리소스가 압축되어 업로드됩니다.

```
  "compress": true
```

#### 실시간 모니터링 설정
WeCOS는 기본적으로 실시간 모니터링 프로그램 디렉터리가 변화되며 이미지 리소스가 자동으로 처리됩니다. 개발 과정에서 실시간 모니터링이 불편하거나 일회성 처리 후 정지할 필요가 있을 경우에 아래 명령행으로 해당 구성을 수정할 수 있으며 프로그램은 한 번만 실행한 후 퇴출됩니다.

```
  "watch": false
```

## 고급 사용법
위의 사용 방식이 불만족인 경우 WeCOS에서는 사용자 지정 모듈의 구성 조작도 제공할 수 있습니다. 직접 인용하는 방식으로 개성화 수요를 충족시킵니다. 구성 예시는 다음과 같습니다.

```
var wecos = require('wecos');

// option 선택 가능 (String|Object)
// String로 전송, 구성 파일 경로 지정
// Object로 전송, 구성 항목 지정
wecos([option]);

// 구성 파일 경로 지정
wecos('./wecos-config.js');

// 구성 항목 지정
wecos({
    appDir: './xxx',
    cos: {
        ...
    }
});
```

## 관련 리소스
- [WeCOS-UGC-DEMO](https://github.com/tencentyun/wecos-ugc-upload-demo) —— 미니 프로그램 사용자 리소스 업로드 COS DEMO
- [COS-AUTH](https://github.com/tencentyun/cos-auth) —— COS 인증 서버 DEMO
