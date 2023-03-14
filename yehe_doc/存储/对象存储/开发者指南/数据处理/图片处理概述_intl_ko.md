## 소개

이미지 처리는 [Cloud Infinite(CI)](https://www.tencentcloud.com/document/product/1045)에서 제공하는 이미지 처리 기능의 세트입니다. 이미지 자르기, 포맷 변환, 스케일링, 워터마크 등의 기본적인 처리 기능과 Guetzli 압축, AVIF 트랜스코딩 및 압축과 같은 이미지 다운사이징 기능, 저작권 보호를 위한 블라인드 워터마크, 이미지 향상, 태그, 평가, 복구 및 이미지 매팅과 같은 AI 기반 인식 및 분석 기능 등을 지원하여 다양한 비즈니스 시나리오에서 이미지 처리 요구 사항을 충족합니다.

> !
> - 이미지 처리 기능은 퍼블릭 클라우드 리전만 지원합니다.
> - 이미지 처리 기능은 CI에서 과금하는 과금 항목입니다. 자세한 과금 설명은 [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431)를 참고하십시오.
> - 현재 다중 AZ 버킷에 대해 이미지 처리가 지원되지 않습니다.
>


<table>
<table>
   <tr>
      <th>서비스</td>
      <th>기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td rowspan=12>기본 이미지 처리 서비스</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">크기 조절</a></td>
      <td>동일 비율 조정, 타깃의 가로:세로 비율 설정 등 다양한 방법</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">자르기</a></td>
      <td>일반 자르기, 크기 조정 자르기, 내접원 자르기, 스마트 얼굴 자르기</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">회전</a></td>
      <td>자동 회전, 일반 회전</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">형식 변환</a></td>
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
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">이미지 워터마크</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">텍스트 워터마크</a></td>
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
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">빠른 섬네일 템플릿</a></td>
      <td>이미지의 빠른 포맷 변환, 축소, 자르기 등 기능 구현 및 썸네일 생성</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">스타일 설정</a></td>
      <td>이미지 스타일 설정으로 다양한 니즈의 이미지를 편리하게 관리</td>
   </tr>
   <tr>
      <td rowspan=11>AI 기반 이미지 인식</td>
      <td>이미지 복구</td>
      <td>이미지에서 LOGO, 객체 및 워터마크와 같은 콘텐츠를 제거하고 그 부분을 배경으로 지능적으로 채워 이미지의 특정 영역을 효과적으로 복구합니다.</td>
   </tr>
   <tr>
      <td>이미지 매트</td>
      <td>이미지에서 신체 부위를 지능적으로 인식하고 나머지 부분은 투명하게 만듭니다.</td>
   </tr>
   <tr>
      <td>Logo 인식</td>
      <td>이미지에서 브랜드 Logo를 인식하고 이미지에서 Logo 문자 및 위치와 같은 정보를 반환합니다.</td>
   </tr>
   <tr>
      <td>QR 코드 인식</td>
      <td>이미지에서 QR 코드를 인식하고 해당 위치와 내용을 반환합니다. 인식된 QR 코드를 픽셀화할 수 있습니다.</td>
   </tr>
   <tr>
      <td>이미지 태그</td>
      <td>이미지에서 장면, 물체, 동물(고양이, 개, 새 포함), 음식(과일 및 채소 포함)과 같은 정보를 지능적으로 인식하고 해당 태그를 추가합니다. 수십 개의 카테고리에서 수천 개의 태그가 지원됩니다.</td>
   </tr>
   <tr>
      <td>이미지 품질 평가</td>
      <td>다양한 차원에서 시각적 이미지 품질을 평가하고 객관적인 해상도 점수와 주관적인 미적 점수를 출력합니다.</td>
   </tr>
   <tr>
      <td>얼굴 인식</td>
      <td>주어진 얼굴 이미지에서 얼굴 위치, 얼굴 특징, 얼굴 품질 정보를 감지하고 뷰티 필터, 인물 사진 키잉, 나이 변경, 성별 전환 등 다양한 특수 효과를 지원합니다.</td>
   </tr>
   <tr>
      <td>페이스 ID</td>
      <td>ID 카드 인식 및 얼굴 생체 인식과 같은 기능을 제공합니다.</td>
   </tr>
   <tr>
      <td>차량 인식</td>
      <td>이미지에서 차량을 감지하고 차량 브랜드, 색상, 위치 및 번호판 번호와 같은 정보를 인식합니다.</td>
   </tr>
   <tr>
      <td>텍스트 인식</td>
      <td>이미지의 단어를 지능적으로 인식하고 편집 가능한 텍스트로 변환합니다.</td>
   </tr>
   <tr>
      <td>이미지로 검색</td>
      <td>버킷에 이미지 라이브러리를 생성하고 지정된 이미지 라이브러리에서 동일하고 유사한 이미지를 빠르게 검색합니다.</td>
   </tr>
   <tr>
      <td rowspan=1>기타</td>
      <td>비정상 이미지 감지</td>
      <td>TS 비디오 스트림이 포함된 이미지와 같이 비정상적이고 의심스러운 정보가 포함된 이미지를 감지합니다.</td>
   </tr>
</table>



## 사용 방법

#### COS 콘솔 사용

COS 콘솔에서 기본 이미지 처리 작업을 수행할 수 있습니다. 자세한 내용은 [기본 이미지 처리](https://intl.cloud.tencent.com/document/product/436/36569)를 참고하십시오.

#### REST API 사용

COS에서 제공하는 API를 이용하여 기본적인 이미지 처리나 AI 기반 인식을 수행할 수 있습니다. 자세한 내용은 [Data Processing APIs](https://www.tencentcloud.com/document/product/436/36364)를 참고하십시오.

## 제한 설명

- 지원 형식: JPG, BMP, GIF, PNG, WEBP 이미지 처리와 HEIF 이미지 디코딩 및 처리가 가능합니다.
- 용량 제한: 원본 이미지의 크기는 32MB, 가로 x 세로는 30000픽셀, 총 픽셀은 2.5억 픽셀을 초과할 수 없으며, 처리 완료된 이미지의 가로 x 세로는 9999픽셀을 초과해 설정할 수 없습니다. 애니메이션 이미지의 경우 원본 이미지의 가로 x 세로 x 프레임 수는 2.5억 픽셀을 초과할 수 없습니다.
- 프레임 수(애니메이션 이미지의 경우): gif의 경우 프레임 수는 300개를 초과할 수 없습니다.
