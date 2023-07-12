## 소개
[Ghost](https://ghost.org/docs)는 블로그 웹 사이트를 빠르게 구축하기 위한 Node.js 기반 프레임워크입니다. 공식 cli 툴을 사용하여 개인 웹사이트를 빠르게 생성하고 CVM 또는 Docker에 배포할 수 있습니다.

블로그 사이트로서 첨부파일 업로드는 필수 기능입니다. Ghost는 기본적으로 첨부 파일을 로컬에 저장합니다. 이 문서는 플러그인을 통해 [COS(Cloud Object Storage)](https://www.tencentcloud.com/products/cos)에 첨부 파일을 저장하는 방법을 설명합니다. COS에 포럼 첨부 파일을 저장하면 다음과 같은 이점이 있습니다.
- 첨부 파일의 신뢰성이 높아집니다.
- 포럼 첨부 파일을 위해 서버에 추가 스토리지 용량을 준비할 필요가 없습니다.
- 다운스트림 대역폭을 차지하거나 자신의 서버에서 트래픽을 증가시키는 대신 COS 서버를 통해 이미지 첨부 파일에 더 빠르게 액세스합니다.
- [Content Delivery Network(CDN)](https://www.tencentcloud.com/products/cdn)을 통해 이미지 첨부 파일에 대한 포럼 사용자 액세스를 가속화할 수 있습니다.

## 준비 작업

### Ghost 웹사이트 구축

1. [Node.js](https://nodejs.org/en/download/) 환경을 설치합니다.
2. ghost-cli를 설치합니다.
```js
npm install ghost-cli@latest -g
```
3. 프로젝트를 생성하고 프로젝트의 루트 디렉터리에서 다음 명령을 실행합니다.
```js
ghost install local
```
성공적으로 생성된 후 프로젝트 구조는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/76e74eff7779379f2e40c5c9220453fc.jpg)
4. 브라우저를 열고 localhost:2368에 액세스합니다. 가입 페이지에서 계정에 가입하고 관리 백엔드로 이동합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/16c412b34d8d9eda9525d12b7e34f5cf.jpg)


### COS 버킷 생성

1. [COS 콘솔](https://console.cloud.tencent.com/cos/bucket)에서 버킷 생성에 설명된 대로 **공개 읽기/비공개 쓰기** 액세스 권한의 버킷을 생성합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참고하십시오.
2. **보안 관리 > CORS(Cross-Origin Resource Sharing)**를 클릭하고 [CORS 설정](https://intl.cloud.tencent.com/document/product/436/13318)에 설명된 대로 CORS 구성을 추가합니다. 다음 구성을 사용하여 디버깅을 용이하게 할 수 있습니다.




## Ghost를 COS 버킷과 연결

>!리스크를 줄이기 위해 서브 계정 키를 사용하고 [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)을 따르는 것이 좋습니다. 서브 계정 키를 가져오는 방법에 대한 자세한 내용은 [액세스 키](https://intl.cloud.tencent.com/document/product/598/32675)를 참고하십시오.


1. Ghost 프로젝트의 루트 디렉터리에 있는 config.development.json 구성 파일에 다음 구성을 추가합니다.
```json
  "storage": {
    "active": "ghost-cos-store",
    "ghost-cos-store": {      
      "BasePath": "ghost/", // 디렉터리 이름으로 변경할 수 있습니다. 비워두면 기본적으로 루트 디렉터리가 사용됩니다. 
      "SecretId": "AKID*************",
      "SecretKey": "***************",
      "Bucket": "xxx-125********", 
      "Region": "**-*******"
    }
  }
```
매개변수 설명은 다음과 같습니다.
<table>
   <tr>
      <th width="0%" >설정 항목</td>
      <th width="0%" >설정 항목</td>
   </tr>
   <tr>
      <td>BasePath</td>
      <td>파일이 저장되는 COS 경로입니다. 필요에 따라 수정할 수 있습니다. 비워두면 기본적으로 루트 디렉터리가 사용됩니다.</td>
   </tr>
   <tr>
      <td>SecretId</td>
      <td><a href="https://console.cloud.tencent.com/capi">API Key 관리</a>페이지에서 생성 및 획득할 수 있는 액세스 키 정보입니다.</td>
   </tr>
   <tr>
      <td>SecretKey</td>
      <td><a href="https://console.cloud.tencent.com/capi">API Key 관리</a>페이지에서 생성 및 획득할 수 있는 액세스 키 정보입니다.</td>
   </tr>
   <tr>
      <td>Bucket</td>
      <td>examplebucket-1250000000과 같이 버킷 생성 중에 사용자 정의된 이름입니다.</td>
   </tr>
   <tr>
      <td>Region</td>
      <td>버킷 생성 중에 선택한 리전입니다.</td>
   </tr>
</table>
2. 사용자 지정 스토리지 디렉터리를 생성하고 프로젝트의 루트 디렉터리에서 다음 명령을 실행합니다.
```js
mkdir -p content/adapters/storage
```
3. Tencent Cloud에서 제공하는 [ghost-cos-store](https://github.com/tencentyun/ghost-cos-store) 플러그인을 설치합니다.
   1. npm을 통해 설치합니다.
```js
npm install ghost-cos-store
```
   2. storage 디렉터리에 다음 콘텐츠가 포함된 ghost-cos-store.js 파일을 생성합니다.
```js
//  content/adapters/storage/ghost-cos-store.js
module.exports = require('ghost-cos-store');
```
   3. git clone을 통해 실행합니다.
```js
cd content/adapters/storage
git clone https://github.com/tencentyun/ghost-cos-store.git
cd ghost-cos-store  
npm i
```
   4. 설치 후 Ghost를 다시 시작합니다.
```js
ghost restart
```



## 게시물 게시 및 업로드 테스트

1. Ghost 콘솔에서 +를 클릭하여 게시물을 게시합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/27dc54b218009f64bd319707700dba71.jpg)
2. +를 클릭하여 이미지를 업로드합니다. 브라우저에서 캡처한 패킷에서 upload 요청이 성공하고 이미지의 COS URL이 반환되는 것을 확인할 수 있습니다.



