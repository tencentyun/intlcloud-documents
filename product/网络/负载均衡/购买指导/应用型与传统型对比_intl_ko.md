## 응용형과 전통형 비교
CLB 인스턴스 유형은 응용형과 전통형으로 나뉩니다. 그 중 전통형은 초기 버전이고 응용형은 강화 버전이며, 응용형은 전통형의 모든 기능을 포괄합니다. 제품 기능, 제품 성능 등 여러 측면에서 응용형 CLB를 선택하시길 권장합니다. 두 가지 버전 비교는 다음과 같고 선택 시 참조하십시오.

<table>
        <tbody>
                <tr>
            <th style="width: 10%;" rowspan="2">제품 유형</th>
            <th style="width: 45%;" colspan="2" >응용형 CLB</th>
            <th style="width: 45%;" colspan="2">전통형 CLB</th>
        </tr>
        <tr>
            <th>공중망</th>
            <th>사설망</th>
            <th>공중망</th>
            <th>사설망</th>
        </tr>
        <tr>
            <td>7계층 포워딩(HTTP/HTTPS)</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✖</td>
        </tr>
        <tr>
            <td>4계층 포워딩(TCP/UDP)</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
        </tr>    
                <tr>
            <td>HTTP/2 및 websocket(secure) 지원</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✖</td>
        </tr>
        <tr>
            <td>CLB 전략</td>
                        <td>ip hash(7계층)<br>가중 라운드 로빈<br>가중 최소 연결 수</td>
                        <td>ip hash(7계층)<br>가중 라운드 로빈<br>가중 최소 연결 수</td>
                        <td>ip hash(7계층)<br>가중 라운드 로빈<br>가중 최소 연결 수</td>
                        <td>가중 라운드 로빈</td>
        </tr>   
         <tr>
            <td>세션 유지</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
        </tr>   
        <tr>
            <td>상태 검사</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
        </tr>   
         <tr>
            <td>사용자 지정 포워딩 규칙(도메인 이름/URL)</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✖</td>
                        <td>✖</td>
        </tr>   
            <tr>
            <td>다른 백 엔드 포트에 포워딩</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✖</td>
                        <td>✖</td>
        </tr>   
         <tr>
            <td>리디렉션(rewrite) 지원</td>
                        <td>✔</td>
                        <td>✖</td>
                        <td>✖</td>
                        <td>✖</td>
        </tr>   
             <tr>
            <td>지역 간 바인딩 지원</td>
                        <td>✔</td>
                        <td>✖</td>
                        <td>✖</td>
                        <td>✖</td>
        </tr>   
        <tr>
            <td>로그를 COS에 저장 지원</td>
                        <td>지원 예정</td>
                        <td>지원 예정</td>
                        <td>지원 예정</td>
                        <td>✖</td>
        </tr>   
</tbody></table>
