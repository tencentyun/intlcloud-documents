CLB(Cloud Load Balancer) 인스턴스 유형: CLB(이전의 ‘애플리케이션 CLB’)
- CLB는 TCP/UDP/HTTP/HTTPS 프로토콜을 지원하여 도메인 이름 및 URL 경로를 기반으로 하는 유연한 포워딩 기능을 제공합니다.

제품의 기능과 성능을 감안할 때 CLB를 사용하는 것이 좋습니다. 장점은 다음과 같습니다.

<table>
        <tbody>
               <tr>
            <th style="width: 10%;" rowspan="2">제품 유형</th>
            <th style="width: 45%;" colspan="2" >CLB</th>
            </tr>
        <tr>
            <th>공중망</th>
            <th>사설망</th>
           </tr>
        <tr>
            <td>레이어 7 포워딩(HTTP/HTTPS)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                       </tr>
        <tr>
            <td>레이어 4 포워딩(TCP / UDP)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        </tr>  
        <tr>
            <td>암호화된 레이어 4 포워딩(TCP SSL)</td>
                        <td>&#10003;</td>
                       <td>&#10003;</td>
                       </tr>    
                <tr>
            <td>HTTP/2 및 websocket(secure) 지원</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        </tr>
        <tr>
            <td>로드 밸런싱 정책</td>
                        <td>IP hash(레이어 7)<br>가중 라운드 로빈<br>가중 최소 연결 스케쥴링 </td>
                        <td>IP hash(레이어 7)<br>가중 라운드 로빈<br>가중 최소 연결 스케쥴링</td>
                        </tr>   
         <tr>
            <td>세션 지속성</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                       </tr>   
        <tr>
            <td>상태 확인</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        </tr>   
         <tr>
            <td>사용자 지정 전달 규칙(도메인 이름/URL)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                       </tr>   
        <tr>
           <td>SNI 다중 인증서 지원</td>
                       <td>&#10003;</td>
                       <td>&#10003;</td>
                      </tr>
            <tr>
            <td>다른 실제 포트로 포워딩</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                     </tr>   
        <tr>
           <td>맞춤형 레이어 7 구성</td>
                       <td>&#10003;</td>
                       <td>&#10003;</td>
                     </tr>  
         <tr>
            <td>레이어 7 리디렉션(rewrite)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                      </tr>
             <tr>
            <td>리전 간 바인딩 지원</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                      </tr>   
                <tr>
            <td>CLS에 레이어 7 액세스 로그 저장</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                      </tr>    
</tbody></table>

>?  
>
>- CLB 인스턴스: CLB 인스턴스는 HTTP/2 프로토콜 활성화 또는 비활성화를 지원합니다. 자세한 내용은 [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.85.8D.E7.BD.AE.E7.9B.91.E5.90.AC.E5.99.A8)를 참고하십시오.


