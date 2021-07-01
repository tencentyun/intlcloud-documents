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



## SDK API 참조

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참조하십시오.

## 업로드 시 이미지 처리 사용

다음 예시는 이미지 업로드 시 자동 이미지 처리 방법입니다.

이미지 업로드 완료 후 COS는 원본과 처리한 이미지를 저장합니다. 이후에 사용자는 일반 다운로드 요청을 통해 처리했던 결과를 불러올 수 있습니다.

#### 예시 코드

[//]: #	". cssg-snippet-upload-with-pic-operation"

```cs
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);

JObject o = new JObject();
// 원본 이미지는 반환하지 않음
o["is_pic_info"] = 0;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = "desample_photo.jpg";
//처리 매개변수. 규칙은 https://cloud.tencent.com/document/product/436/44879를 참조하십시오.
rule["rule"] = "imageMogr2/thumbnail/400x400";
rules.Add(rule);
o["rules"] = rules;

string ruleString = o.ToString(Formatting.None);
request.SetRequestHeader("Pic-Operations", ruleString);
//실행 요청
PutObjectResult result = cosXml.PutObject(request);
```

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs)를 참조하십시오.

## 클라우드 데이터의 이미지 처리

다음 예시는 COS에 저장된 이미지에 알맞은 처리 작업을 하고 결과를 COS에 저장하는 방법입니다.

#### 예시 코드

[//]: #	".cssg-snippet-process-with-pic-operation"

```cs
JObject o = new JObject();
// 원본 이미지는 반환하지 않음
o["is_pic_info"] = 0;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = "desample_photo.jpg";
//처리 매개변수. 규칙은 https://cloud.tencent.com/document/product/436/44879를 참조하십시오.
rule["rule"] = "imageMogr2/thumbnail/400x400";
rules.Add(rule);
o["rules"] = rules;
string ruleString = o.ToString(Formatting.None);

ImageProcessRequest request = new ImageProcessRequest(bucket, key, ruleString);
ImageProcessResult result = cosXml.ImageProcess(request);
```

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs)를 참조하십시오.

## 다운로드 시 이미지 처리 진행

다음 예시는 COS에 저장된 이미지를 다운로드 시 처리 작업을 진행하는 방법입니다.

#### 예시 코드

[//]: #	".cssg-snippet-download-with-pic-operation"

```cs
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, key, localDir, localFileName);
//처리 매개변수. 다음 인스턴스는 포맷을 TPG 이미지로 변환하는 예시입니다. 규칙은 https://cloud.tencent.com/document/product/436/44879를 참조하십시오.
getObjectRequest.SetQueryParameter("imageMogr2/format/tpg", null);
```

> ?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs)를 참조하십시오.
