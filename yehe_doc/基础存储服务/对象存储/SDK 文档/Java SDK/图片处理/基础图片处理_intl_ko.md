## 소개

Tencent Cloud COS는 [Cloud Infinite(CI)](https://intl.cloud.tencent.com/document/product/1045)의 전문적인 일체형 멀티미디어 솔루션을 통합하여 다음과 같은 이미지 처리 기능을 제공합니다. 자세한 내용은 [이미지 처리 개요](https://intl.cloud.tencent.com/document/product/436/35280)를 참조하십시오.

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


## 기본 이미지 처리

기본 이미지 처리의 예시는 다음과 같습니다.

### 크기 조정

```java
String bucketName = "examplebucket-1250000000";
String key = "qrcode.png";
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// 폭과 높이 50% 축소
String rule = "imageMogr2/thumbnail/! 50p";
getObj.putCustomQueryParameter(rule, null);
cosClient.getObject(getObj, new File("qrcode-50p.png"));
```

### 자르기

```java
String bucketName = "examplebucket-1250000000";
String key = "qrcode.png";
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// 폭과 높이 50% 축소
String rule = "imageMogr2/iradius/150";
getObj.putCustomQueryParameter(rule, null);
cosClient.getObject(getObj, new File("qrcode-cropping.png"));
```

### 회전

```java
String bucketName = "examplebucket-1250000000";
String key = "qrcode.png";
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// 폭과 높이 50% 축소
String rule = "imageMogr2/rotate/90";
getObj.putCustomQueryParameter(rule, null);
cosClient.getObject(getObj, new File("qrcode-rotate.png"));
```








