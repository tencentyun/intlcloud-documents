## 개요

문서 미리보기 기능은 Tencent Cloud CI(Cloud Infinite)를 기반으로 파일을 이미지, PDF 또는 HTML5 페이지로 트랜스 코딩할 수 있는 기능을 제공하여 문서 콘텐츠의 페이지 표시 문제를 해결하고 PC, App 등 여러 클라이언트의 문서의 **온라인 브라우징** 요구를 충족하며 온라인 교육, 기업 OA, 웹사이트 트랜스 코딩 등 비즈니스 시나리오에 적합합니다.

>?
>- 현재 지원되는 입력 파일 형식은 다음 형식과 같습니다:
  - 데모 파일: pptx, ppt, pot, potx, pps, ppsx, dps, dpt, pptm, potm, ppsm.
  - 텍스트 파일: doc, dot, wps, wpt, docx, dotx, docm, dotm.
  - 테이블 파일: xls, xlt, et, ett, xlsx, xltx, csv, xlsb, xlsm, xltm, ets.
  - 기타 형식 파일: pdf, lrc, c, cpp, h, asm, s, java, asp, bat, bas, prg, cmd, rtf, txt, log, xml, htm, html.
>- 현재 상기 파일 형식을 jpg, png, pdf, html 형식으로 트랜스 코딩할 수 있습니다.
>- 입력 파일의 크기는 200MB로 제한되며, 입력 파일의 페이지 수는 5000페이지로 제한됩니다.



## 아키텍처

현재 문서 미리보기 기능은 동기화 트랜스 코딩과 비동기화 트랜스 코딩의 두 가지 방법을 제공합니다.

### 동기화 트랜스 코딩

<img src="https://qcloudimg.tencent-cloud.cn/raw/8841b09bf41ea16ae0f4b58c71dc43ba.png" width="550px"  />

### 비동기화 트랜스 코딩
<img src="https://main.qcloudimg.com/raw/13028a5d31b0f35ae7994e9373f60014.png" width="550px" />

## 적용 시나리오

PC 및 App 등 여러 클라이언트의 문서를 온라인 브라우징 요구에 맞추어, 온라인 교육, 기업 OA 및 웹 사이트 트랜스 코딩과 같은 비즈니스 시나리오에 적합합니다.


## 사용 방법

### COS 콘솔 사용

문서 미리보기 기능을 사용하기 전에 문서 미리보기 서비스를 활성화해야 하며, 자세한 내용은 문서 미리보기 콘솔 활성화 가이드 문서를 참고하십시오.

#### 비동기화 트랜스 코딩

COS 콘솔을 사용하여 비동기화 문서 트랜스 코딩 미리보기 작업을 수행할 수 있으며, 자세한 내용은 [파일 미리보기 작업 생성](https://intl.cloud.tencent.com/document/product/436/46409) 콘솔 가이드 문서를 참고하십시오.

### REST API 사용

#### 동기화 트랜스 코딩

API를 사용하여 버킷에 있는 문서의 실시간 트랜스 코딩을 미리 볼 수 있습니다.

- HTML5가 아닌 미리보기를 사용합니다. 자세한 내용은 동기화 요청 인터페이스 API 문서를 참고하십시오.
- HTML5 미리보기를 사용합니다. 자세한 내용은 문서 전환 HTML 시작하기 API 문서를 참고하십시오.
