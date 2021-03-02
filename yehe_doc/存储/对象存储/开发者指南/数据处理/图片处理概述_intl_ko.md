## 소개

[CI](https://intl.cloud.tencent.com/document/product/1045)(Cloud Infinite)의 전문적인 일체형 멀티미디어 솔루션을 통합한 Tencent Cloud COS는 다음 표와 같은 이미지 처리, 심사, 식별 등 기능을 제공합니다. COS의 업로드 및 처리 인터페이스로 미디어 데이터를 처리할 수 있습니다.

> !
> - 이미지 처리 기능은 중국 공유 클라우드 리전에서만 지원합니다.
> - 이미지 처리 기능은 CI에서 과금하는 과금 항목입니다. 자세한 과금 설명은 [과금 및 가격](https://intl.cloud.tencent.com/document/product/1045/33431)을 참조하십시오.



<table>
   <tr>
      <th>서비스</td>
      <th>기능</td>
      <th>설명</td>
   </tr>
   <tr>
      <td rowspan=12>기본 이미지 처리 서비스</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">크기 조절</a></td>
      <td>동일 비율 조절, 가로:세로 비율 설정 등 다양한 방법</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">자르기</a></td>
      <td>일반 편집, 크기 조절 편집, 원형 자르기, 스마트 얼굴 자르기</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">회전</a></td>
      <td>자동 회전, 일반 회전</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">형식 변환</a></td>
      <td>형식 변환, GIF 형식 최적화, 점진적 표시</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">품질 변경</a></td>
      <td>JPG 및 WEBP 이미지의 품질 변경</td>
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
      <td>이미지 정보 보기</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36375">기본 정보</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36376">EXIF 정보</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36377">주조색</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">메타 정보 삭제</a></td>
      <td>EXIF 정보 포함</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">빠른 섬네일 템플릿 </a></td>
      <td>이미지의 빠른 형식 변환, 축소, 자르기 등 기능 구현 및 섬네일 생성</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">스타일 설정</a></td>
      <td>이미지 스타일 설정으로 다양한 니즈의 이미지를 편리하게 관리</td>
   </tr>
</table>



## 사용 방법

#### COS 콘솔 사용

COS 콘솔을 사용해 이미지 처리 설정을 할 수 있으며, 자세한 내용은 [이미지 처리 활성화](https://intl.cloud.tencent.com/document/product/436/36569)을 참조하십시오.

#### REST API 사용

COS가 제공하는 API로 이미지 처리 설정을 할 수 있으며, 자세한 내용은 [기본 이미지 처리](https://intl.cloud.tencent.com/document/product/436/36365) API 문서를 참조하십시오.

## 제한 설명

- 지원 형식: JPG, BMP, GIF, PNG, WEBP 형식 및 HEIF 형식의 디코딩과 처리를 지원합니다.
- 용량 제한: 원본 이미지의 크기는 20MB, 가로 x 세로는 30000픽셀, 총 픽셀은 1억 픽셀을 초과할 수 없으며, 처리 완료된 이미지의 가로 x 세로는 9999픽셀을 초과해 설정할 수 없습니다. 애니메이션 이미지의 경우 원본 이미지의 가로 x 세로 x 프레임 수는 1억 픽셀을 초과할 수 없습니다.
- 애니메이션 프레임 수 제한: GIF 프레임은 300프레임을 넘을 수 없습니다.

