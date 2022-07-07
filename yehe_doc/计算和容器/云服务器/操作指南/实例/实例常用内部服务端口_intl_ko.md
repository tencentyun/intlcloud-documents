CVM 인스턴스의 일반적으로 사용되는 포트는 다음과 같습니다.
## Linux 일반 서비스
<table>
<tr>
<th><b>서비스</b></th>
<th><b>기능</b></th>
<th><b>서비스 유형</b></th>
<th><b>서비스 이름</b></th>
<th><b>백엔드 서비스에 액세스하기 위한 도메인 이름</b></th>
<th><b>백엔드 서비스에 액세스하기 위한 포트</b></th>
</tr>
<tr>
<td rowspan="5">인스턴스 초기화 서비스</td> 
<td rowspan="5">인스턴스 초기화 기능 제공</td> 
<td rowspan="5">비상주 서비스, <br>실행 후 종료</td> 
<td rowspan="2">cloud-init</td> 
<td>mirrors.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>tlinux-mirrors.tencentyun.com</td>
<td>443</td>
</tr>
<tr>
<td rowspan="4">공공 서비스</td>    
<td>ntpupdate.tencentyun.com</td>
<td>123</td>
</tr>
<tr>
<td>DHCP Server</td> 
<td>67, 68</td> 
</tr>
<tr>
<td>DNS</td> 
<td>53</td> 
</tr>
<tr>
<td rowspan=3>클라우드 모니터링</td> 
<td rowspan="2">클라우드 모니터링 기능 제공</td> 
<td rowspan="2">상주 서비스</td> 
<td rowspan="2">barad_agent</td> 
<td>receiver.barad.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>eventproxy.tencentyun.com</td>
<td>80</td>
</tr>
<tr>
<td>클라우드 모니터링 서비스 설치 및 <br>업그레이드</td>    
<td>상주 서비스</td>
<td>startgate</td>
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td rowspan="4">Cloud Workload Protection</td> 
<td rowspan="4">클라우드 보안 기능 제공</td> 
<td rowspan="4">상주 서비스</td> 
<td rowspan="4">YDService</td> 
<td>metadata.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>l.yd.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>s.yd.tencentyun.com</td>    
<td>5574</td>
</tr>
<tr>
<td>u.yd.tencentyun.com</td> 
<td>9080, 80</td> 
</tr>
</table>

## Windows 일반 서비스
<table>
<tr>
<th><b>서비스</b></th>
<th><b>기능</b></th>
<th><b>서비스 유형</b></th>
<th><b>서비스 이름</b></th>
<th><b>백엔드 서비스 액세스 도메인 이름</b></th>
<th><b>백엔드 서비스 액세스 포트</b></th>
</tr>
<tr>
<td rowspan="5">인스턴스 초기화 서비스</td> 
<td rowspan="5">인스턴스 초기화 기능 제공</td> 
<td rowspan="5">비상주 서비스, <br>실행 완료 후 종료</td> 
<td rowspan="2">cloudbase-init</td> 
<td>kms.tencentyun.com</td> 
<td>1688</td> 
</tr>
<tr>
<td>kms1.tencentyun.com</td>
<td>1688</td>
</tr>
<tr>
<td rowspan="4">공공 서비스</td>    
<td>ntpupdate.tencentyun.com</td>
<td>123</td>
</tr>
<tr>
<td>DHCP Server</td> 
<td>67, 68</td> 
</tr>
<tr>
<td>DNS</td> 
<td>53</td> 
</tr>
<tr>
<td rowspan=3>클라우드 모니터링</td> 
<td rowspan="2">클라우드 모니터링 기능 제공</td> 
<td rowspan="2">상주 서비스</td> 
<td rowspan="2">BaradAgentSvc</td> 
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>custom.message.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>클라우드 모니터링 서비스 설치 및 <br>업그레이드</td>    
<td>상주 서비스</td>
<td>startgate</td>
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td rowspan="4">Cloud Workload Protection<br></td> 
<td rowspan="4">클라우드 보안 기능 제공</td> 
<td rowspan="4">상주 서비스</td> 
<td rowspan="4">YDService</td> 
<td>metadata.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>l.yd.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>s.yd.tencentyun.com</td>    
<td>5574</td>
</tr>
<tr>
<td>u.yd.tencentyun.com</td> 
<td>9080, 80</td> 
</tr>
</table>



