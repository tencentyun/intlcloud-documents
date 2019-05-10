## 소개
Tencent Cloud GME SDK의 사용을 환영합니다. 개발자가 Tencent Cloud GME API를 디버깅하고 연결하는 데 도움이 되도록 여기에 GME Authbuffer의 컴파일 기술 문서를 소개합니다.

## 컴파일링 상세 절차

### 1. 관련 파일 다운로드
[여기를 클릭](https://main.qcloudimg.com/raw/1fdb3269055bacb09695cd6014af1d0b.zip)하여 GME Authbuffer 관련 파일을 다운로드합니다.


### 2. Linux에 관련 파일 가져오기
다운로드한 파일은 zip 파일입니다. 해당 파일은 Linux에 가져옵니다.


### 3. 관련 파일 압축 해제
다운로드한 zip 파일을 압축 해제합니다.


### 4. 프로젝트 디렉터리에 들어가기
관련 코드는 `cd authbuffer/build/linux/`를 참조하십시오.



### 5. make 수행
make를 수행하여 동적 라이브러리를 생성합니다.
경로: `[개인 폴더]/authbuffer/build/linux`
![image](https://main.qcloudimg.com/raw/a97ab83b76f2ea68ce7315828224e99b.png)


### 6. 실행 가능 파일 실행
실행 가능 파일의 경로: `[개인 폴더]/authbuffer/bin/linux/libAuthbuffer.so`
![image](https://main.qcloudimg.com/raw/2f1d265631137955d1ab890790ab8d14.png)
