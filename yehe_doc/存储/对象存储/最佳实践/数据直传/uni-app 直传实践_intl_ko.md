## 소개
본 문서에서는 SDK를 사용하지 않고 uni-app을 통해 직접 COS(Cloud Object Storage) 버킷에 파일을 업로드하는 간단한 코드를 사용하는 방법을 설명합니다.

>? 본 문서는 XML API [PostObject](https://intl.cloud.tencent.com/document/product/436/14690)를 기반으로 합니다.
>

## 솔루션

### 실행 프로세스

1. 프런트엔드에서 파일을 선택하면 프런트엔드가 파일 확장자를 서버로 보냅니다.
2. 서버는 파일 확장자에 따라 시간과 함께 임의의 COS 파일 경로를 생성하고 해당 PostObject policy 서명을 계산하고 URL 및 서명 정보를 프런트엔드에 반환합니다.
3. 프런트엔드는 [PostObject API](https://intl.cloud.tencent.com/document/product/436/14690)를 호출하여 파일을 COS에 업로드합니다.

### 솔루션 장점

- 권한 보안: PostObject policy 서명은 보안 권한 범위를 효과적으로 제한하며 지정된 파일 경로에 업로드하는 데만 사용할 수 있습니다.
- 경로 보안: 서버가 임의의 COS 파일 경로를 결정하므로 기존 파일을 덮어쓰는 문제와 보안 위험을 효과적으로 방지할 수 있습니다.
- 다중 터미널 호환성: uni-app에서 제공하는 파일 선택 및 업로드 API를 사용하여 동일한 코드를 다중 터미널(Web/미니프로그램/App)과 호환되도록 할 수 있습니다.


## 전제 조건

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 버킷을 생성하여 Bucket(버킷 이름)과 Region(리전 이름)을 획득합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참조하십시오.
2. [CAM 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인한 뒤 프로젝트의 SecretId와 SecretKey를 획득합니다.
3. 새로 생성된 버킷의 세부 정보 페이지로 이동하여 **보안 관리 > CORS(Cross-Origin Resource Sharing)**를 선택하고 **규칙 추가**를 클릭합니다. 아래 이미지는 구성 예시입니다. 자세한 내용은 [크로스 도메인 액세스 설정](https://intl.cloud.tencent.com/document/product/436/13318)을 참고하십시오.



## 실행 순서

>! 정식 배포 전에 서버 측에서 웹사이트 자체에 대한 권한 확인 단계를 추가하는 것이 좋습니다.
>

### 프런트 엔드 업로드

1. 서버 API를 구현하여 임의의 파일 경로를 생성하고 서명을 계산하여 프런트엔드로 반환합니다. 구현 세부 정보는 [post-policy 예시](https://github.com/tencentyun/cos-demo/tree/main/server/post-policy/)를 참고하십시오.
2. HBuilderX의 기본 템플릿을 사용하여 uni-app 앱을 만듭니다.
생성된 앱은 Vue 프로젝트입니다.
3. 다음 코드를 복사하여 pages/index/index.vue 파일의 내용을 바꾸고 post-policy API 호출 링크를 수정하여 서버 주소(1단계에서 구현된 서버 API)를 가리키도록 합니다.
```html
<template>
   <view class="content">
      <button type="default" @click="selectUpload">파일 업로드 선택</button>
      <image v-if="fileUrl" class="image" :src="fileUrl"></image>
   </view>
</template>

<script>
   export default {
      data() {
         return {
            title: 'Hello',
            fileUrl: ''
         };
      },
      onLoad() {

      },
      methods: {
         selectUpload() {

            var vm = this;

            // 더 많은 문자열 코드의 url encode 형식
            var camSafeUrlEncode = function (str) {
               return encodeURIComponent(str)
                       .replace(/!/g, '%21')
                       .replace(/'/g, '%27')
                       .replace(/\(/g, '%28')
                       .replace(/\)/g, '%29')
                       .replace(/\*/g, '%2A');
            };

            // 업로드 경로 및 자격 증명 가져오기
            var getUploadInfo = function (extName, callback) {
               // 백엔드가 임의의 COS 객체 경로를 생성하고 업로드 도메인과 PostObject API에 필요한 policy 서명을 반환할 수 있도록 파일 확장자 전달
               // 서버 예시 참고: https://github.com/tencentyun/cos-demo/tree/main/server/post-policy
               uni.request({
                  url: 'http://127.0.0.1:3000/post-policy?ext=' + extName,
                  success: (res) => {
                     callback && callback(null, res.data.data);
                  },
                  error(err) {
                     callback && callback(err);
                  },
               });
            };

            // 업로드 요청을 시작하고 업로드는 PostObject API 및 policy 서명 보호 사용
            // API 문서: https://intl.cloud.tencent.com/document/product/436/14690#.E7.AD.BE.E5.90.8D.E4.BF.9D.E6.8A.A4
            var uploadFile = function (opt, callback) {
               var formData = {
                  key: opt.cosKey,
                  policy: opt.policy, // Base64 policy 문자열
                  success_action_status: 200,
                  'q-sign-algorithm': opt.qSignAlgorithm,
                  'q-ak': opt.qAk,
                  'q-key-time': opt.qKeyTime,
                  'q-signature': opt.qSignature,
               };
               // 서버가 계산을 위해 임시 키를 사용하는 경우 x-cos-security-token 전달 필요
               if (opt.securityToken) formData['x-cos-security-token'] = opt.securityToken;
               uni.uploadFile({
                  url: 'https://' + opt.cosHost, // 실제 API 주소가 아닌 예시
                  filePath: opt.filePath,
                  name: 'file',
                  formData: formData,
                  success: (res) => {
                     if (![200, 204].includes(res.statusCode)) return callback && callback(res);
                     var fileUrl = 'https://' + opt.cosHost + '/' + camSafeUrlEncode(opt.cosKey).replace(/%2F/g, '/');
                     callback && callback(null, fileUrl);
                  },
                  error(err) {
                     callback && callback(err);
                  },
               });
            };

            // 파일 선택
            uni.chooseImage({
               success: (chooseImageRes) => {
                  var file = chooseImageRes.tempFiles[0];
                  if (!file) return;
                  // 업로드할 로컬 파일의 경로 가져오기
                  var filePath = chooseImageRes.tempFilePaths[0];
                  // 업로드할 파일의 확장자를 가져오면 백엔드가 임의의 COS 경로 생성
                  var fileName = file.name;
                  var lastIndex = fileName.lastIndexOf('.');
                  var extName = lastIndex > -1 ? fileName.slice(lastIndex + 1) : '';
                  // 사전 업로드를 위한 도메인 이름, 경로 및 자격 증명 가져오기
                  getUploadInfo(extName, function (err, info) {
                     // 파일 업로드
                     info.filePath = filePath;
                     uploadFile(info, function (err, fileUrl) {
                        vm.fileUrl = fileUrl;
                     });
                  });
               }
            });
         },
      }
   }
</script>

<style>
   .content {
      padding: 20px 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
   }

   .image {
      margin-top: 20px;
      margin-left: auto;
      margin-right: auto;
   }
</style>
```
4. HBuilderX에서 **실행 > 브라우저로 실행 > Chrome**을 선택합니다. 그 다음 브라우저에서 업로드할 파일을 선택할 수 있습니다.
실행 결과는 다음 이미지와 같습니다.

 - 직접 업로드 효과:
![uni-app 직접 업로드 효과](https://qcloudimg.tencent-cloud.cn/raw/ef40cb5ea3ce5a0586dd1a70d6b2d4ad.jpg)

##  Demo 코드 주소

Demo 다운로드 주소: [upload-demo](https://github.com/tencentyun/cos-demo/tree/main/uni-app/upload-demo)

