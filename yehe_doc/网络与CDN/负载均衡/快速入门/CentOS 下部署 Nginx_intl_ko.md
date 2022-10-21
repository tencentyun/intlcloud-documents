본문은 CentOS에 Nginx 프로젝트를 배포하는 방법을 설명합니다. Tencent Cloud의 새로운 개별 사용자에게 적합합니다.
## 소프트웨어 버전
본문에 사용된 소프트웨어 툴의 버전은 다음과 같으며 실제 작업 시 사용자의 소프트웨어 버전과 다를 수 있습니다.
- 운영 체제: CentOS 7.5
- Nginx: Nginx 1.16.1

## Nginx 설치
1. 구매를 완료한 후 CVM 세부 정보 페이지에서 [로그인]을 클릭하여 CVM 인스턴스에 로그인한 다음 사용자 이름과 비밀번호를 입력하여 Nginx 환경을 설정합니다. CVM 인스턴스 생성 방법에 대한 자세한 내용은 [CVM 인스턴스 생성](https://cloud.tencent.com/document/product/213/4855)을 참고하십시오.
```
# Nginx 설치:
yum -y install nginx  
# Nginx 버전 보기
nginx -v
# Nginx 설치 디렉터리 보기
rpm -ql nginx
# Nginx 실행
service nginx start
```
2. CVM 인스턴스의 공중망 IP 주소에 액세스하고 다음 페이지가 나타나면 Nginx가 성공적으로 배포된 것입니다.
![](https://main.qcloudimg.com/raw/8807f9fd819eb93d46c5646ba3572fac.png)
3. Nginx의 기본 root 디렉터리는 `/usr/share/nginx/html`입니다. 이 페이지의 특수성을 표시하기 위해 `html` 디렉터리에서 `index.html` 정적 페이지를 수정하십시오. 관련 작업은 다음과 같습니다.
   1. 다음 명령을 실행하여 html 아래의 index.html 정적 페이지로 이동합니다.
```bash
vim /usr/share/nginx/html/index.html
```
   2. ‘i’를 눌러 편집 모드로 이동하여 `<body></body>` 태그에 다음을 추가합니다.
```bash
# <body> 바로 아래에 입력하는 것을 권장합니다
Hello nginx , This is rs-1!
URL is index.html
```
   ![](https://main.qcloudimg.com/raw/02e833dd08a6873d5d015f4531d24645.png)
   3. ‘Esc’를 누르고 `:wq`를 입력하여 변경 사항을 저장합니다.
4. CLB(이전의 ‘애플리케이션 CLB’)는 실제 서버 경로에 따라 요청을 포워딩하고 `/image` 경로에 정적 페이지를 배포할 수 있습니다. 관련 작업은 다음과 같습니다.
   1. 다음 명령을 실행하여 `image` 디렉터리를 생성하고 디렉터리로 이동합니다.
```bash
mkdir /usr/share/nginx/html/image
cd /usr/share/nginx/html/image
```
   2. 다음 명령을 실행하여 `image` 디렉터리에 `index.html` 정적 페이지를 생성합니다.
```
vim index.html
```
   3. ‘i’를 눌러 편집 모드로 이동하고 페이지에 다음을 추가합니다.
```bash
Hello nginx , This is rs-1!
URL is image/index.html
```
   4. ‘Esc’를 누르고 `:wq `를 입력하여 변경 사항을 저장합니다.
>!Nginx의 기본 포트는 `80`입니다. 포트를 변경하려면 구성 파일을 수정하고 Nginx를 다시 시작하십시오.

## Nginx 서비스 확인
CVM 인스턴스의 공중망 IP + 경로에 액세스합니다. 배포된 정적 페이지가 표시되면 Nginx가 성공적으로 배포된 것입니다.
- rs-1의 index.html 페이지:
![](https://main.qcloudimg.com/raw/ede62fecd2106869d53bf142ad51903e.png)
- rs-1의 /image/index.html 페이지:
![](https://main.qcloudimg.com/raw/f0f87422487177722291c2260cac9d35.png)
