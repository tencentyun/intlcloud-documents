이 문서는 CentOS 시스템에서 nginx 프로젝트를 배포하는 방법을 소개하며, 이제 막 Tencent Cloud를 사용하기 시작한 개인 사용자에게 적용됩니다.
## 소프트웨어 버전
예제 절차 중 이 문서의 소프트웨어 버전은 다음과 같습니다. 실제로 작업하는 과정에서 소프트웨어 버전을 기준으로 하십시오.
- 운영 체제: CentOS 7.5
- Nginx 버전: nginx 1.12.2

## nginx 설치
구매한 후, CVM 세부 정보 페이지에서 [로그인]을 클릭하면 CVM에 바로 로그인할 수 있으며, 사용자 이름과 비밀번호를 입력하면 nginx 환경을 구축할 수 있습니다. CVM 인스턴스 생성 관련 내용은 [CVM 인스턴스 구매 및 시작](https://cloud.tencent.com/document/product/213/4855)을 참조하십시오.

```
# nginx 설치:
yum -y install nginx  

# nginx 버전 확인
nginx -v

# nginx 설치 디렉터리 확인
rpm -ql nginx

# nginx 시작
service nginx start
```
현재 해당 CVM을 액세스하는 공인 IP 주소가 다음 페이지가 나타나면 nginx 배포가 완료된 것입니다.
![](https://main.qcloudimg.com/raw/c3d248fcfdfa45ad40c96cdca6769551.png)
nginx의 기본 루트 디렉터리는 `/usr/share/nginx/html`이며 html의 index.html 정적 페이지를 바로 수정하여 이 페이지의 특수성을 나타냅니다.
```
vim /usr/share/nginx/html/index.html
# 페이지에서 다음 입력
Hello nginx , This is rs-1!
URL is index.html
```

응용형 CLB는 RS의 경로에 따라 요청 포워딩할 수 있습니다. 현재는 /image 경로에서 정적 페이지를 배포하며 관련 명령은 다음과 같습니다.
```
# 디렉터리 이미지 생성
mkdir /usr/share/nginx/html/image
cd /usr/share/nginx/html/image
vim index.html
# 페이지에서 다음 입력
Hello nginx , This is rs-1!
URL is image/index.html
```

> 참고: nginx의 기본 포트는 `80`이며, 포트를 수정하고 싶으면 구성 파일을 수정하고 nginx를 다시 시작하십시오.

## nginx 서비스 인증
CVM의 공인 IP + 경로에 접근하십시오. 배포한 정적 페이지가 보인다면 nginx 배포에 성공하였음을 증명합니다.
rs-1의 index.html 페이지:
![](https://main.qcloudimg.com/raw/02c7524bedbd68ae25a36577a2fcb148.png)
rs-1의 /image/index.html 페이지:
![](https://main.qcloudimg.com/raw/5663e2ee65aede1069a8ecf0d6003cc4.png)

