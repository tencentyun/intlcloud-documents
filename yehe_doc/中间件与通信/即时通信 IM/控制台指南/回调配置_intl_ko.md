[IM 콘솔](https://console.cloud.tencent.com/im)에 로그인하여 대상 애플리케이션 카드를 클릭하고 왼쪽 사이드바에서 [콜백 설정]을 선택하여 비즈니스 니즈에 따라 콜백 URL을 구성하고 활성화할 콜백을 설정할 수 있습니다.

## 콜백 URL 구성

1. [콜백 설정] 페이지의 콜백 URL 설정 섹션의 [편집]을 클릭합니다.
2. 콜백 URL 구성 팝업 창에서 콜백 URL을 입력합니다.

>?
>- 콜백 URL은 'http://' 또는 'https://'로 시작해야 합니다.
>- 아직 도메인을 신청하지 않았다면 `http://123.123.123.123/imcallback`과 같이 IP를 직접 설정할 수 있습니다.
>- 영문자(`a~z`, 대소문자 구분 안함), 숫자(0~9), 하이픈(-)만 사용할 수 있습니다. 빈칸 및 ! $&? 부호는 지원되지 않습니다. 
>- 하이픈(-)은 연속 사용, 단독 사용할 수 없으며, 시작이나 끝 부분에 사용할 수 없습니다.  
>- 도메인 길이는 63자를 초과할 수 없습니다.
>- 콜백 URL 중, IM은 기본적으로 80/443 포트를 수반합니다. 콜백 URL 교체 시 포트 변경이 수반되므로, 전, 후의 포트가 서로의 접두사가 되는 것을 피해야 합니다. 예: https://xxx:443을 https://xxx:4433으로 변경, 또는 https://xxx를 https://xxx:4433으로 변경하는 것을 피해야 함.

3. [확인]을 클릭하여 설정을 저장합니다.

## 이벤트 콜백 설정
1. [콜백 설정] 페이지의 이벤트 콜백 설정 섹션에서 [편집]을 클릭합니다.
2. 이벤트 콜백 설정 팝업 창에서 원하는 콜백을 선택합니다.
![](https://main.qcloudimg.com/raw/67cb8c9fd2365e3e2014e6940c468aaf.png)
3. [확인]을 클릭하여 설정을 저장합니다.

## HTTPS 상호 인증서 다운로드
콜백 URL을 구성 후, 콘솔에서 HTTPS 상호 인증서를 다운로드하여 추후 사용할 수 있습니다.
>?필요에 따라 상호 인증을 설정할 수 있으며, 구체적인 설정 방법은 [Apache 상호 인증 설정](https://intl.cloud.tencent.com/document/product/1047/34379)을 참고하십시오.

1. [콘솔](https://console.cloud.tencent.com/im-detail/callback-setting)의 [[콜백 설정](https://console.cloud.tencent.com/im-detail/callback-setting)] 페이지 우측 상단의 콜백 URL 설정 섹션에서 [HTTPS 상호 인증서 다운로드]를 클릭합니다.
![](https://main.qcloudimg.com/raw/52a1d6fc283f07e29842da512ba303a3.png)
2. 인증서 다운로드 팝업 창에서 [다운로드]를 클릭합니다.
![](https://main.qcloudimg.com/raw/584dcfbed3a36a691971f6edcca19b43.png)
3. 인증서 파일을 저장합니다.


## 후속 작업
콜백 URL 구성 및 해당 이벤트 콜백 활성화 후, [서드 파티 콜백 소개](https://intl.cloud.tencent.com/document/product/1047/34354)를 참고하여 해당 콜백 기능을 사용하면, 사용자 정보 및 작업을 실시간으로 알아볼 수 있습니다.
