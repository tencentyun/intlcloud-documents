
고객님께:
안녕하세요. 고객님께서 Tencent Cloud 공식 홈페이지에서 Ubuntu14.04 CVM apt-get을 구매하여 Tomcat 및 Hadoop을 설치할 때 정상적으로 포트를 리슨할 수는 있지만, 요청에는 무응답인 것으로 감지되었습니다. Tecent Cloud에서 관련 해결 조치를 제안해드리오니, 이와 같은 상황이 발생하면 해당 조치에 따라 문제를 해결하시기 바랍니다.

## 문제 원인
Java Runtime Environment의 [기존 문제](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6202721)에 의해 발생했습니다.

### 문제 분석
Tomcat 및 Hadoop은 Java로 개발되어 java.security.SecureRandom API를 사용했습니다.
해당 API는 JRE에서 `/dev/random`을 사용하여 생성되도록 기본 설정되어 있는데, `/dev/random `은 CPU 온도, 키보드 등 하드웨어 노이즈에 따라 엔트로피를 생성합니다. CVM은 가상화 기술이 적용된 환경이므로 CPU 온도와 같은 신호를 감지하기 어려워 엔트로피를 생성할 수 없습니다. 따라서 `cat /dev/random `이 대부분 차단되어 Tomcat 및 Hadoop을 실행할 수 없게 됩니다.

### 해결 조치
#### JRE 설정 변경
기존 `/etc/java-7-openjdk/security/java.security`( URL은 실제 상황에 따라 다름) 중의 ` securerandom.source=file:/dev/urandom `을 `securerandom.source=file:/dev/./urandom `으로 변경하면 위와 같은 문제를 해결할 수 있습니다.




