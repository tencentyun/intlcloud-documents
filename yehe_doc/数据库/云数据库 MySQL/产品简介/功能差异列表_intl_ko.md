본 문서에서는 TencentDB for MySQL의 구성별로 지원하는 기능과 차이점을 소개합니다. 이를 통해 사용자가 구성의 특징을 더 잘 이해함으로써 필요에 따라 인스턴스를 구매할 수 있도록 도와줍니다.

<table>
<thead><tr><th align="left">기능</th><th align="left">이중 노드</th><th align="left">3중 노드</th><th colspan=2 align="left" >단일 노드</th>
</tr></thead>
<tbody><tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/39794" target="_blank">격리 정책</a></td>
<td align="left">범용형</td>
<td align="left">범용형</td>
<td align="left">범용형</td>
<td align="left">기본형</td></tr>
<tr>
<td align="left">버전</td>
<td align="left"><li>MySQL 5.5</li><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td>
<td align="left"><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td>
<td align="left"><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td>
<td align="left">MySQL 5.7</td></tr>
<tr>
<td align="left">노드 수</td>
<td align="left">2</td>
<td align="left">3</td>
<td align="left">1</td>
<td align="left">1</td></tr>
<tr>
<td align="left">메모리/디스크</td>
<td align="left">최대 488GB/6TB</td>
<td align="left">최대 488GB/6TB</td>
<td align="left">최대 488GB/6TB</td>
<td align="left">최대 8GB/1T</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/8126" target="_blank">엔진 버전 업그레이드</a></td>
<td align="left">지원(MySQL 5.5, 5.6만 지원)</td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">지원</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/zh/document/product/236/35986" target="_blank">파이낸스 버전 업그레이드</a></td>
<td align="left">지원</td>
<td align="left">-</td>
<td align="left">-</td>
<td align="left">-</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">읽기 전용 인스턴스</a></td>
<td align="left">지원(MySQL 5.6, 5.7, 8.0만 지원)</td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">-</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/31900" target="_blank">계정 관리</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">-</td>
<td align="left">지원</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/35793" target="_blank">매개변수 설정</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">-</td>
<td align="left">지원</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">백업</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">-</td>
<td align="left">-</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/7276" target="_blank">롤백</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">-</td>
<td align="left">-</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/8463" target="_blank">데이터 마이그레이션</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">-</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/8466" target="_blank">SQL 파일 가져오기</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">-</td>
<td align="left">-</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/14470" target="_blank">보안 그룹</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">-</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/8455" target="_blank">모니터링 및 알람</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">지원</td></tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/236/34588" target="_blank">작업 로그</a></td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">지원</td>
<td align="left">지원</td></tr>
</tbody></table>


>?위 테이블에서 '-' 표시는 지원하지 않는다는 의미입니다.
