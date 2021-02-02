COS 종량제 가격에 관한 내용은 다음과 같습니다.

[과금 실제 사례](https://intl.cloud.tencent.com/document/product/436/6241)를 참조하면 실제 사례를 통해 COS 과금에 관해 파악할 수 있습니다.

COS 공유 클라우드의 리전 구분 사항은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참조하십시오.

## 종량제 가격

>- COS 과금과 관련한 자세한 사항은 [과금 방식](https://intl.cloud.tencent.com/document/product/436/16871#billing-modes), [과금 항목](https://intl.cloud.tencent.com/document/product/436/33776), [과금 주기](https://intl.cloud.tencent.com/document/product/436/16871#billing-cycle)를 참조하십시오.
>- 종량제 관련 예시 설명은 [종량제(후불)](https://intl.cloud.tencent.com/document/product/436/32534)을 참조하십시오.
>- 다음 가격표에 명시된 CAS 및 DEEP ARCHIVE의 요청 과금, 외부 네트워크 다운스트림 트래픽 과금은 표준 스토리지로 복구해야 관련 과금이 발생합니다. CAS 및 DEEP ARCHIVE 관련 사항은 [스토리지 유형](https://intl.cloud.tencent.com/document/product/436/30925)을 참조하십시오.

<table>
   <tr>
      <th rowspan="3" width="75px">이용 리전</th>
      <th rowspan="3">스토리지 유형</th>
	<th colspan="6"><center>과금 항목</center></th>
   </tr>
   <tr>
      <th rowspan="2">스토리지 용량 과금(달러/GB/월)</th>
      <th rowspan="2" width="150px">요청 과금<br>(달러/만 회)</th>
      <th rowspan="2">데이터 검색 과금(달러/GB)</th>
      <th colspan="3">트래픽 과금(달러/GB)</th>
   </tr>
   <tr>
      <th>외부 네트워크<br>다운스트림 트래픽</th>
      <th>CDN Origin-pull 트래픽</th>
      <th>리전 간<br>트래픽 복제</th>
   </tr>
   <tr>
      <td rowspan="3">청두, 충칭</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.0045</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px" nowrap="nowrap">빠른 검색: 0.03   <br>일반 검색: 0.01<br>대량 검색: 0.0025</td>
      <td>0.1(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="1">베이징, 광저우, 청두</td>
      <td>DEEP ARCHIVE</td>
      <td>0.002</td>
      <td>읽기 쓰기 요청: 0.14<br>일반 검색 요청: 1<br>대량 검색 요청: 0.29<br>(복구 후 요청 가능)</td>
      <td>일반 검색: 0.02<br>대량 검색: 0.0026</td>
      <td rowspan="1">0.1(복구 후 적용 가능)</td>
      <td rowspan="1">미적용</td>
      <td rowspan="1">미적용</td>
   </tr>
   <tr>
      <td rowspan="3">베이징, 난징, 상하이, 광저우</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS(난징 임시 미지원)</td>
      <td>0.005</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.03<br>일반 검색: 0.01<br>대량 검색: 0.0025</td>
      <td>0.1(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">중국홍콩</td>
      <td>표준 스토리지</td>
      <td>0.022</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.016</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.005</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.036<br>일반 검색: 0.012<br>대량 검색: 0.003</td>
      <td>0.08(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">싱가포르</td>
      <td>표준 스토리지</td>
      <td>0.022</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.016</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.005</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.036<br>일반 검색: 0.012<br>대량 검색: 0.003</td>
      <td>0.072(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">프랑크푸르트</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.0045</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.03<br>일반 검색: 0.01<br>대량 검색: 0.0025</td>
      <td>0.07(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">토론토</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.0045</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.03<br>일반 검색: 0.01<br>대량 검색: 0.0025</td>
      <td>0.07(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">뭄바이</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.018</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.005</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.036<br>일반 검색: 0.012<br>대량 검색: 0.003</td>
      <td>0.1(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">서울</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.005</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.036<br>일반 검색: 0.012<br>대량 검색: 0.003</td>
      <td>0.12(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">실리콘밸리</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.0045</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.03<br>일반 검색: 0.01<br>대량 검색: 0.0025</td>
      <td>0.07(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">버지니아주</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.0045</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.03<br>일반 검색: 0.01<br>대량 검색: 0.0025</td>
      <td>0.07(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">방콕</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.005</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.036<br>일반 검색: 0.012<br>대량 검색: 0.003</td>
      <td>0.18(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">모스크바</td>
      <td>표준 스토리지</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.0045</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.03<br>일반 검색: 0.01<br>대량 검색: 0.0025</td>
      <td>0.07(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
   <tr>
      <td rowspan="3">도쿄</td>
      <td>표준 스토리지</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>표준IA 스토리지</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.005</td>
      <td>0.0147(복구 후 요청 가능)</td>
      <td width="150px">빠른 검색: 0.036<br>일반 검색: 0.012<br>대량 검색: 0.003</td>
      <td>0.12(복구 후 적용 가능)</td>
      <td>미적용</td>
      <td>미적용</td>
   </tr>
</table>


## 관리 기능 가격


>!
>[인벤토리 기능](https://intl.cloud.tencent.com/zh/document/product/436/30622) 과금, [인덱스 기능](https://intl.cloud.tencent.com/zh/document/product/436/32472) 과금, [배치](https://intl.cloud.tencent.com/zh/document/product/436/32958) 과금, [객체 태그](https://intl.cloud.tencent.com/zh/document/product/436/31509) 과금은 모두 **일별**로 결제됩니다.


<table>
   <tr>
	 <th rowspan=3 ><center>적용 리전</center></th>
      <th colspan=5 ><center>관리 과금</center></th>
   </tr>
   <tr>
      <th rowspan=2>인벤토리 기능<br>(달러/객체 백만 개당</th>
      <th>인덱스 기능<br>(달러/GB)</th>
      <th colspan=2>배치 기능</th>
      <th rowspan=2>객체 태그 과금<br>(달러/태그 만 개당</td>
   </tr>
   <tr>
      <th>표준 스토리지<br>표준IA 스토리지</td>
      <th>작업 과금<br>(달러/개)</th>
      <th>객체 처리 과금<br>(달러/객체 처리 만 개당</th>
   </tr>
   <tr>
      <td>청두, 충칭</td>
      <td>0.0027</td>
      <td>0.0018</td>
      <td>0.2022</td>
      <td>0.0081</td>
      <td>0.01</td>
   </tr>
   <tr>
      <td>베이징, 난징, 상하이, 광저우</td>
      <td>0.0027(난징 임시 미지원)</td>
      <td>0.0018</td>
      <td>0.2022</td>
      <td>0.0081</td>
      <td>0.01</td>
   </tr>
   <tr>
      <td>중국홍콩</td>
      <td>0.0028</td>
      <td rowspan=11>임시 미지원</td>
      <td rowspan=11>임시 미지원</td>
      <td rowspan=11>임시 미지원</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>싱가포르</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>뭄바이</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>서울</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>방콕</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>도쿄</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>실리콘밸리</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>버지니아주</td>
      <td>0.0025</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>토론토</td>
      <td>0.0025</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>프랑크푸르트</td>
      <td>0.0027</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>모스크바</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
</table>

## 글로벌 가속 가격

> [글로벌 가속](https://intl.cloud.tencent.com/document/product/436/33409) 기능은 모두 운영 중이며, 중국 내외의 공유 클라우드 리전을 지원합니다.
>- 글로벌 가속 가격은 **일별**로 결제됩니다.

| 리전 간 전송 방향              | 수신/발신 방식| 글로벌 가속 트래픽 과금<br>(달러/Gb) |
| ----------------------------------- | -------- | ----------------------------- |
| 중국대륙 - 중국대륙 리전             | 업스트림     | 0.07                          |
| 중국대륙 - 중국대륙 리전             | 다운스트림     | 0.07                           |
| 중국대륙 - 중국홍콩 및 해외 리전       | 업스트림     | 0.18                        |
| 중국대륙 - 중국홍콩 및 해외 리전       | 다운스트림     | 0.18                           |
| 중국홍콩 및 해외 - 중국홍콩 및 해외 리전 | 업스트림     | 0.18                          |
| 중국홍콩 및 해외 - 중국홍콩 및 해외 리전 | 다운스트림     | 0.18                         |
| 중국홍콩 및 해외 - 중국대륙 리전       | 업스트림     | 0.18                            |
| 중국홍콩 및 해외 - 중국대륙 리전       | 다운스트림     | 0.18                       |
