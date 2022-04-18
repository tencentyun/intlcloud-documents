본문은 Tencent Cloud IM Demo(Electron)를 빠르게 실행하는 방법을 소개합니다.

## 환경 요건

| 플랫폼 | 버전 |
|---------|---------|
| Electron | 13.1.5 이상 버전. |
|Node.js|v14.2.0|

## 전제 조건

[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985)된 계정이 있고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)이 완료되어야 합니다.

## 작업 단계
[](id:step1)

### 1단계: 애플리케이션 생성
1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인합니다.
>?이미 애플리케이션이 있는 경우 SDKAppID를 기록하고 [키 정보 가져오기](#step2)를 합니다.
>동일한 Tencent Cloud 계정으로 최대 300개의 IM 애플리케이션을 만들 수 있습니다. 이미 300개의 애플리케이션이 있는 경우 신규 애플리케이션 생성 전에 사용하지 않는 애플리케이션을 [비활성화 및 삭제](https://intl.cloud.tencent.com/document/product/1047/34540)합니다. **애플리케이션 삭제 후에는 SDKAppID에 해당하는 모든 데이터 및 서비스를 복구할 수 없으므로 주의하시기 바랍니다.**
>
2. **애플리케이션 생성**을 클릭하고 **애플리케이션 생성** 대화 상자에 애플리케이션 이름을 입력한 후 **확인**을 클릭합니다.
![](https://main.qcloudimg.com/raw/15e61a874a0640d517eeb67e922a14bc.png)
3. SDKAppID 정보를 저장하십시오. 콘솔 전체보기 페이지에서 새로 생성된 애플리케이션의 상태, 서비스 버전, SDKAppID, 태그, 생성 시간 및 만료 시간을 확인할 수 있습니다.
    ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
4. 생성된 애플리케이션을 클릭한 후, 왼쪽 사이드바의 **보조 툴**>**UserSig 툴**을 클릭하여, UserID 및 UserSig를 생성하고, 로그인에 사용할 UserSig를 복사합니다.
![](https://main.qcloudimg.com/raw/2286644d987d24caf565142ae30c4392.png)

[](id:step2)
### 2단계: 소스 코드 다운로드, 종속성 설치 및 실행
1. IM Electron Demo 소스 코드를 로컬에 클론합니다.
```javascript
git clone https://github.com/tencentyun/im_electron_demo.git
```

2. 프로젝트 종속성을 설치합니다.
```javascript
// 프로젝트의 루트 디렉터리
npm install

// 렌더링 프로세스 디렉터리
cd src/client
npm install
```

3. 프로젝트를 실행합니다.
```javascript
// 프로젝트의 루트 디렉터리
npm start
```

4. 프로젝트를 패키징합니다.
```javascript
// mac 패키징
npm run build:mac
// windows 패키징
npm run build:windows
```



## FAQ

### 어떤 플랫폼이 지원됩니까?
현재 Macos 및 Windows 2가지 플랫폼을 지원합니다.

### 개발 환경 설치 문제 `gypgyp ERR!ERR` 오류를 해결하는 방법은 무엇입니까?
[gypgyp ERR!ERR! ](https://stackoverflow.com/questions/57879150/how-can-i-solve-error-gypgyp-errerr-find-vsfind-vs-msvs-version-not-set-from-c)를 참고하십시오.

### Mac에서 `npm run start`를 실행하면 흰색 화면이 나오는데 어떻게 해결합니까?
Mac에서 `npm run start`를 실행하면 흰색 화면이 나오는 이유는 아직 렌더링 프로세스의 코드가 build 완료되지 않았고, 메인 프로세스가 오픈한 포트 3000번이 빈 페이지이기 때문입니다. 렌더링 프로세스의 코드 build 완료 후 창을 새로고침하면 문제가 해결될 수 있습니다. 또는 `cd src/client && npm run dev:react`, `npm run dev:electron`을 실행하여 렌더링 프로세스와 메인 프로세스를 각각 시작합니다.
