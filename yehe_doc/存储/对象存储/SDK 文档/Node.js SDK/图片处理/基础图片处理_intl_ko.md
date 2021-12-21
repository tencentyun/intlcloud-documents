## 소개

본 문서는 기본 이미지 처리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

<table>
   <tr>
      <th>서비스</td>
      <th>기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td rowspan=11>기본 이미지 처리 서비스</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">크기 조정</a></td>
      <td>동일 비율 조정, 타깃의 가로:세로 비율 설정 등 다양한 방법</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">자르기</a></td>
      <td>일반 자르기, 크기 조정 자르기, 원형 자르기, 스마트 얼굴 자르기</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">회전</a></td>
      <td>자동 회전, 일반 회전</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">포맷 변환</a></td>
      <td>포맷 변환, GIF 포맷 최적화, 점진적 표시</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">품질 변경</a></td>
      <td>JPG 및 WEBP 이미지 품질 변경</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">가우시안 블러</a></td>
      <td>이미지 가우시안 블러 처리</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">샤프닝</a></td>
      <td>이미지 샤프닝 처리</td>
   </tr>
   <tr>
      <td>워터마크 추가</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">이미지 워터마크</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">문자 워터마크</a></td>
   </tr>
   <tr>
      <td>이미지 정보 가져오기</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">기본 정보</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF 정보</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36377">메인 컬러</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">메타 정보 삭제</a></td>
      <td>EXIF 정보 포함</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">빠른 썸네일 템플릿 </a></td>
      <td>이미지의 빠른 포맷 변환, 축소, 자르기 등 기능 구현 및 썸네일 생성</td>
   </tr>
</table>

## 업로드 시 이미지 처리 사용

다음 예시는 이미지 업로드 시 자동 이미지 처리 방법입니다.

이미지 업로드 완료 후 COS는 원본과 처리한 이미지를 저장합니다. 이후에 사용자는 일반 다운로드 요청을 통해 처리했던 결과를 불러올 수 있습니다.

### 예시 코드

```javascript
const filePath = "temp-file-to-upload" // 로컬 파일 경로
cos.putObject({
   Bucket: 'examplebucket-1250000000',
   Region: 'COS_REGION',
   Key: 'exampleobject',
   Body: fs.createReadStream(filePath), // 파일 객체 업로드
   onProgress: function(progressData) {
       console.log(JSON.stringify(progressData));
   },
   Headers: {
	   // imageMogr2 인터페이스를 통해 이미지 크기 조정 기능 사용: 이미지 폭을 200으로 지정하고 폭 비율 압축
	   'Pic-Operations': '{"is_pic_info": 1, "rules": [{"fileid": "desample_photo.jpg", "rule": "imageMogr2/thumbnail/200x/"}]}'
  },
}, function(err, data) {
   console.log(err || data);
});
```

## 클라우드 데이터의 이미지 처리

다음 예시는 COS에 저장된 이미지에 알맞은 처리 작업을 하고 결과를 COS에 저장하는 방법입니다.

### 예시 코드

```javascript
cos.request({
    Bucket: config.Bucket,
    Region: config.Region,
    Key: 'exampleobject',
    Method: 'POST',
    Action: 'image_process',
    Headers: {
	   // imageMogr2 인터페이스를 통해 이미지 크기 조정 기능 사용: 이미지 폭을 200으로 지정하고 폭 비율 압축
      'Pic-Operations': '{"is_pic_info": 1, "rules": [{"fileid": "desample_photo.jpg", "rule": "imageMogr2/thumbnail/200x/"}]}'
    },
}, function (err, data) {
   console.log(err || data);
});
```

## 다운로드 시 이미지 처리 사용

다음 예시는 이미지 다운로드 시 이미지 처리 방법입니다.

### 예시 코드

```javascript
cos.getObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: 'exampleobject',
    QueryString: `imageMogr2/thumbnail/200x/`,
}, function (err, data) {
   console.log(err || data);
   fs.writeFileSync('filepath', data.Body); // 이미지 콘텐츠를 로컬에 저장
});
```

## 이미지 처리 매개변수를 가진 서명 URL 생성

### 예시 코드

```javascript
// 이미지 처리 매개변수를 가진 파일 서명 URL 생성, 만료 시간은 30분으로 설정.
var url1 = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: 'exampleobject',
    Query: {
      `imageMogr2/thumbnail/200x/`: ''
    },
    Expires: 1800,
    Sign: true,
}, function (err, data) {
    if(data){
        console.log(data.Url);
    }
});

// 이미지 처리 매개변수를 가진 파일 URL 생성, 서명은 포함하지 않음
var url2 = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
    Key: 'exampleobject',
    Query: {
      `imageMogr2/thumbnail/200x/`: ''
    },
    Sign: false,
}, function (err, data) {
    if(data){
        console.log(data.Url);
    }
});
```
