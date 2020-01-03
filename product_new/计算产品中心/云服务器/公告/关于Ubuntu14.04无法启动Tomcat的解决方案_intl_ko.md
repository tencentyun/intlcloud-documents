
존경하는 고객님
안녕하세요.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tecent Cloud 공식 사이트에서 Ubuntu14.04 CVM apt-get를 구매하고 Tomcat 및 Hadoop를 설치할 때 정상적으로 포트를 리스닝할 수 있지만 요청에 응답할 수 없습니다. 현재 Tecent Cloud는 해당 조치를 제안하고 있으며 이런 상황에 직면할 경우 권장 조치에 따라 문제를 해결하십시오.

**[문제 원인]**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Java Runtime Environment 의 [기존 버그](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6202721) 에 의해 발생하였습니다.
 **[문제 분석]**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Java 개발에 Tomcat 및 Hadoop 을 사용하고 java.security.SecureRandom 의 API 도 사용합니다.
해당 API은 JRE에서 기본적으로 `/dev/random`에 의해 생성되지만 `/dev/random `은 CPU 온도 및 키보드 등 하드웨어로 엔트로피를 생성합니다. CVM은 버츄얼화 기술이 적용된 버츄얼 기기 환경이므로 CPU 온도와 같은 신호를 감지하기 어려워 엔트로피를 생성할 수 없습니다. 때문에 `cat /dev/random `가 대부분 차단되어 Tomcat 및 Hadoop를 시작할 수 없습니다.
**[해결 조치]**
**JRE 구성 수정**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;기존 ` /etc/java-7-openjdk/security/java.security`(URL 의 실제 상황에 따라)의 ` securerandom.source=file:/dev/urandom `을 수정하고 `securerandom.source=file:/dev/./urandom `으로 상기 문제를 해결합니다.


2016-10-14    
Tecent Cloud




